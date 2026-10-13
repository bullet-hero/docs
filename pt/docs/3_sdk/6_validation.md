---
title: Validação
date: 2026-10-01
tags: [developer, level_author]
---

# Validação

Você chama a validação por conta própria via ValidationFacade, ela não está embutida em salvar e carregar. As ocorrências se dividem em Error, Warning e Advice, e ValidateAndFix corrige o que puder

Onde executá-la fica a critério do jogo. Abrir um nível no editor relata problemas, já a reprodução pula a verificação. Assim, o autor espera pela validação, e o jogador nunca

Um autor de níveis encontra a validação ao oferecer um nível a um serviço. Mais - [[7_publish-profiles]]

## Como chamar

`ValidationFacade` é o único ponto de entrada. Quem chama não precisa saber quantas passagens existem:

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| Método | O que faz |
|---|---|
| `Validate(root, settings)` | verifica qualquer raiz: `Level`, `LevelMeta`, `UserSettings`, um `Prefab` ou `EffectData` avulso. A passagem do grafo roda só para `Level` |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | corrige o que puder e relata o que sobrou |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | as três passagens de uma vez, não corrige nada. `level` pode ser `null` para avaliar só os metadados |

`ValidationReport` contém `RuleIssues` e `GraphIssues`:
- `IsValid` - não há nenhuma ocorrência
- `HasErrors` - há pelo menos uma ocorrência no grupo `Error`

## Gravidade

Cada regra pertence a um `RuleGroup`:
- `Error` - o arquivo não pode ser jogado do jeito que está escrito
- `Warning` - ele é jogado, mas não como pretendido (conteúdo que nunca aparece, uma referência quebrada com alternativa). Ou a única correção é destrutiva
- `Advice` - a reprodução não muda

## Três passagens

| Passagem | O que pergunta | Sobre o que trabalha |
|---|---|---|
| `RuleAnalyzer` | se cada valor está no intervalo, não é `null`, é um membro de enum conhecido | qualquer raiz |
| `LevelGraphAnalyzer` | se os objetos concordam entre si | só `Level` |
| `PublishReadinessAnalyzer` | se o nível pode ser entregue a desconhecidos sob o perfil dado | `LevelMeta`, opcionalmente `Level` |

## Regras

Um tipo entra na verificação pelo marcador `[RuleContainer]`. As propriedades dele carregam atributos de regra:
- `[RuleNotNull]`, `[RuleInRange]`, `[RuleMinValue]`, `[RuleEnumValid]`, `[RuleCollectionMaxCount]` e outros
- `[RuleEnumFlagsValid]` - para enums de flags
- `[RuleOptional]` - para um campo que pode estar ausente

Os próprios limites são constantes nas tabelas de `Rules/`: `FrameRules`, `ValueRules`, `LevelRules` e outras. Por exemplo, `LevelRules.MaxObjects` é 262.144

O percurso por todos os contêineres de regras é gerado pelo `BH.SDK.Roslyn`, sem reflexão. Em níveis grandes, isso corta o tempo dele mais ou menos pela metade

## Correções

Cada atributo de regra pode corrigir o próprio valor (`Fix`). `RuleFixer` aplica as correções na ordem inversa do rastro: uma correção pode deslocar ocorrências mais profundas. `ValidateAndFix` repete a passagem até o resultado parar de mudar

A passagem do grafo roda depois das correções. Uma correção pode ela mesma criar um problema no grafo, por exemplo um novo id que coincide com um existente

**As ocorrências do grafo nunca são corrigidas:** `DuplicateObjectId`, `MissingParent`, `ParentCycle`, `PrefabRemapBroken`, `IdCounterNearExhaustion` e as demais. Cada correção dessas é uma decisão sobre o conteúdo (qual de dois objetos fica com o id). Um palpite reescreveria o nível

> [!caution] Cuidado
> `ValidateAndFix` altera o objeto que você passou. Execute-o em uma cópia se precisar do original, por exemplo para mostrar ao autor o que exatamente mudou
