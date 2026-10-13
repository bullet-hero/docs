---
title: Versionamento e migrações
date: 2026-10-02
tags: [developer, level_author]
---

# Versionamento e migrações

Há três versões: gv para o jogo, sv para o SDK, mg para a geração do formato do modelo. Pelo mg, o SDK migra um arquivo antigo e se recusa a ler um com geração mais nova que a da build

## Três versões

| Rótulo | Significa | O que versiona | Onde fica |
|---|---|---|---|
| `gv` | `game version` | o cliente do jogo | o `bundleVersion` do projeto da Unity |
| `sv` | `sdk version` | o SDK como biblioteca, semver sobre a API pública | `SdkVersion.Value` |
| `mg` | `model generation` | o formato do modelo, uma geração por domínio | `[ModelGeneration]` em cada raiz, `ModelGenerations.Current` |

As versões atuais são `gv {{v:version.gv}}`, `sv {{v:version.sv}}`, `mg {{v:version.mg}}`

Os números `gv` e `sv` não precisam acompanhar um ao outro, mas na maioria dos casos coincidem. As versões são aumentadas juntas, e uma atualização conjunta leva a mesma versão

O que cada parte significa:
- `gv`: major é uma atualização global (história, multijogador), minor são novos recursos comuns, patch é um hotfix
- `sv`, quando o SDK passar a prometer estabilidade de API: major é uma mudança de API que quebra compatibilidade (um tipo removido, a assinatura ou o significado de um membro alterado), minor é um acréscimo a que ninguém precisa reagir, patch é uma correção que não muda nenhuma assinatura

**O `mg` importa mais do que os outros.** É por ele que o SDK decide se migra um arquivo ou se recusa a lê-lo

A tela de configurações mostra os três nesta ordem e com rótulos: `gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`. Sem os rótulos, dois números iguais em um relatório de bug não podem ser distinguidos

Uma versão com `b` e um número no final, por exemplo `gv 1.1.0b1`, é um beta: uma build da próxima versão para testes, normalmente em um ramo beta da Steam. O lançamento seguinte sai sem a letra (`gv 1.1.0`). Um arquivo salvo por um beta pode não abrir no lançamento anterior

> [!warning] Aviso
> Até o SDK dizer o contrário, o `sv` acompanha o jogo, e `sv 1.0.0` não promete estabilidade de API. Por enquanto, um major do `sv` não diz nada sobre compatibilidade para o código compilado contra a DLL

## Números que não são versões

Mais dois números parecem uma "versão", mas não são:
- `LevelMeta.LevelVersion` (chave `vrs`) - a versão do nível dada pelo autor, uma string como `"1.0"`
- `BlobFormat.Generation` - a disposição dos bytes do `.blob`. Mais - [[3_blob-format]]

## Geração: um inteiro por domínio

Um domínio é uma raiz que migra como um todo único. Há 21 deles: `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` e outros. Isso inclui as partes dentro de `Level`: `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. Cada domínio grava a sua geração na chave `g` do seu envelope

| Constante | Valor | Significado |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | nenhuma geração |
| `ModelGenerations.Test` | 0 | a estrutura `Versions/V0` que exercita o caminho de migração |
| `ModelGenerations.V1_AlphaRelease` | 1 | o que saiu com o `gv 1.0.0`, a maioria dos domínios ainda está nela |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`, `LevelMeta`, `LevelStatistics`, `GameStatistics` e o novo `Collection` |
| `ModelGenerations.Current` | a mais nova | o que a interface e os relatórios mostram |

**Uma geração é um número só, não `major.minor`.** Uma mudança na forma de um arquivo precisa de migração ou não precisa. Não há meio-termo

**Os números vêm de um contador global único.** Um domínio que mudou recebe `ModelGenerations.Current + 1`, não o próximo número livre dele próprio. É exatamente isso que mantém com sentido o `mg` único na string de versão

## O novo é recusado

Toda mudança de modelo é uma nova geração. Uma mudança de forma, um campo adicionado e um novo valor de enum contam igual. Por isso, uma geração maior do que a build conhece é uma forma que ela certamente nunca viu

Há uma exceção: um modelo totalmente novo que nenhum modelo existente menciona, por exemplo skins de avatar em um arquivo separado. É um novo domínio sem nada de onde migrar, então a geração não aumenta. O que aumenta é a geração do modelo existente que passa a referenciá-lo

Um arquivo assim não é lido de forma alguma: sem valores padrão, sem partes puladas. `NewerGenerationException` carrega `Domain`, `FileGeneration` e `BuildGeneration`, e o host pede ao jogador que atualize

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## O antigo é migrado

Um domínio que muda de forma recebe:
1. uma nova geração do contador global
2. um snapshot congelado da forma antiga em `Versions/V<old>/`: uma classe com `[GenerateModel]` e `[ModelGeneration(domain, <old>)]`
3. uma `ModelMigration<TFrom, TTo>` em `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` encontra os snapshots e os migradores por reflexão e percorre a cadeia até a forma atual. Toda substituição com perda durante a leitura vai para `SerializationReport`, não para o silêncio

## Recusa antes da leitura

`LevelMeta.MinGeneration` (chave `min_generation`) é a maior geração entre os domínios do nível. Ela é calculada ao salvar por `LevelGenerations.Required()` e nunca é digitada à mão

O cliente a compara antes de abrir `level.json`. Assim, um nível do futuro é recusado sem ler megabytes de conteúdo. Um arquivo que não declara nada guarda `-1`

O registro completo das decisões - [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) no repositório do SDK
