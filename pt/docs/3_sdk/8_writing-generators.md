---
title: Como escrever um gerador
date: 2026-10-02
tags: [developer]
---

# Como escrever um gerador

Um gerador é uma classe sobre uma classe base do SDK: BaseLevelGenerator, BaseContentGenerator ou BaseModifier. O host monta sozinho o formulário, a estimativa e o desfazer a partir do contrato

Um gerador cria conteúdo de nível a partir de poucos parâmetros. O autor não precisa posicionar cada objeto à mão

Ninguém escreve uma interface para um gerador, e nenhuma lista é editada

O que os geradores integrados fazem - [[8_generators]]

## Três tipos

| Tipo | Cria | Classe base | Ponto de entrada |
|---|---|---|---|
| `Level` | um novo `Level` e um `LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | novos objetos e recursos no escopo ativo | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | edições em objetos que já existem | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content e Modifier compartilham o ponto de entrada. Eles diferem na intenção e em `GeneratorRequirements`. Por padrão, um modificador precisa de uma seleção

Para geradores que criam objetos existe `BaseSpawnGenerator<TParams>`. Ele cria cada objeto, define o pai dele e o posiciona no tempo. À classe concreta resta só a matemática do posicionamento

## Sem registro

`GeneratorRegistry` encontra todos os geradores por reflexão no primeiro acesso. Dois geradores com o mesmo `NameKey` falham ali mesmo

Só o assembly do próprio SDK é varrido. Por isso um novo gerador fica no repositório do SDK e chega como pull request. Mais - [[9_contributing-sdk]]

## Exemplo

Uma fileira de objetos, construída sobre as mesmas classes do `RadialGenerator` integrado:

```csharp
using BH.SDK.Generators;
using BH.SDK.Generators.Spawn;
using BH.SDK.Rules;

public class RowGenerator : BaseSpawnGenerator<RowGenerator.Parameters>
{
    public override string NameKey => "gen_geometry_row";

    public override GeneratorHints Hints { get; } = new GeneratorHints.Builder()
        .Section(GeneratorSections.Main, SpawnParameters.MainFields)
        .Section(GeneratorSections.Main, nameof(Parameters.Count), nameof(Parameters.Spacing))
        .Section(GeneratorSections.Additional, SpawnParameters.AdditionalFields)
        .Section(GeneratorSections.Additional, nameof(Parameters.StartX), nameof(Parameters.Y))
        .Range(nameof(Parameters.Count), 1, 256)
        .Range(nameof(Parameters.Spacing), 0f, ValueRules.MaxPos)
        .Range(nameof(Parameters.StartX), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(Parameters.Y), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(SpawnParameters.Size), ValueRules.MinSca, ValueRules.MaxSca)
        .Build();

    protected override void Generate(GeneratorContext context, Parameters parameters)
    {
        for (var i = 0; i < parameters.Count; i++)
        {
            var obj = Spawn(context, parameters, $"row_{i}", context.Span);
            AddPosition(obj, parameters.StartX + i * parameters.Spacing, parameters.Y, obj.Span.StartFrame);
        }
    }

    // Spawn adiciona um quadro-chave de tamanho e um de cor, AddPosition adiciona o terceiro
    protected override GeneratorCost EstimateTyped(GeneratorContext context, Parameters parameters)
        => new GeneratorCost(parameters.Count, parameters.Count * 3);

    public class Parameters : SpawnParameters
    {
        public int Count = 8;
        public float Spacing = 2f;
        public float StartX;
        public float Y;
    }
}
```

`NameKey` tem a forma de uma chave de localização. O host mostra o nome pela própria tabela de strings

## Regras obrigatórias

- **Altere o nível só por `GeneratorContext`** (`Create`, `Edit`, `Delete`, `SetValue` e outros). Ele registra cada mudança em `GeneratorChangeLog`, e todo o desfazer se apoia nisso. Uma mudança direta no modelo compila e quebra o desfazer em silêncio
- **Cada campo está listado em uma seção, cada número tem um `Range`.** A ordem dos campos vinda da reflexão não é garantida. Um número sem limites não dá ao host nada para limitar. Os intervalos são verificados por um teste
- **Os parâmetros são campos públicos mutáveis e um construtor sem parâmetros.** O formulário se liga a eles, e uma predefinição os serializa. Não esconda um campo herdado: tudo é endereçado pelo nome do campo
- **A estimativa coincide com a execução.** O host a mostra antes da execução. Se a execução fosse passar de `LevelRules.MaxObjects`, o host recusa
- **A aleatoriedade vem de `context.CreateRandom()`,** não de `System.Random`. A mesma semente dá o mesmo nível em qualquer plataforma
- **Defina `context.Parent` como pai do que você cria.** É assim que o host reúne a execução inteira em um objeto
- **Declare `GeneratorRequirements.LevelScope`** se você mexer em `context.Game` ou `context.Audio`. Os dois são `null` enquanto o escopo ativo é um prefab
- **Sobrescreva `IsDangerousTyped`** se uma combinação de parâmetros excluir ou reescrever conteúdo fora da janela para a qual o autor está olhando. Então o host pede confirmação

## Dados externos

O SDK não tem decodificador de áudio, nem FFT, nem carregador de imagens. Um gerador que precisa desses dados:
1. declara `GeneratorRequirements.ExternalAnalysis`
2. implementa uma interface de `External/`: `IWaveformInput`, `IBeatFramesInput`, `IPixelTextureInput` e outras

O host preenche os dados antes da execução. Se não recebeu nada, o gerador não deve criar nada

O contrato completo - [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
