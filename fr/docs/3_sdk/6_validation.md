---
title: Validation
date: 2026-10-01
tags: [developer, level_author]
---

# Validation

Tu appelles la validation toi-même via ValidationFacade, elle n'est pas intégrée à l'enregistrement ni au chargement. Les problèmes se répartissent en Error, Warning et Advice, et ValidateAndFix répare ce qu'il peut

C'est au jeu de décider où la lancer. Ouvrir un niveau dans l'éditeur signale les problèmes, alors que la lecture saute la vérification. Ainsi, l'auteur attend la validation, et le joueur jamais

Un auteur de niveaux rencontre la validation quand il propose un niveau à un service. Plus - [[7_publish-profiles]]

## Comment l'appeler

`ValidationFacade` est le point d'entrée unique. L'appelant n'a pas besoin de savoir combien de passes existent :

```csharp
var facade = new ValidationFacade();
var report = facade.Validate(level);

if (report.HasErrors)
    Console.WriteLine(report);
```

| Méthode | Ce qu'elle fait |
|---|---|
| `Validate(root, settings)` | vérifie n'importe quelle racine : `Level`, `LevelMeta`, `UserSettings`, un `Prefab` ou un `EffectData` autonome. La passe du graphe ne tourne que pour `Level` |
| `ValidateAndFix(root, analyzerSettings, fixerSettings)` | répare ce qu'il peut et signale ce qui reste |
| `ValidateForPublish(meta, profile, level, now, payload, settings)` | les trois passes à la fois, ne répare rien. `level` peut valoir `null` pour n'évaluer que les métadonnées |

`ValidationReport` contient `RuleIssues` et `GraphIssues` :
- `IsValid` - il n'y a aucun problème
- `HasErrors` - il y a au moins un problème dans le groupe `Error`

## Gravité

Chaque règle appartient à un `RuleGroup` :
- `Error` - le fichier ne peut pas être joué tel qu'il est écrit
- `Warning` - il se joue, mais pas comme prévu (un contenu qui n'apparaît jamais, une référence cassée avec une valeur de repli). Ou alors la seule réparation est destructive
- `Advice` - la lecture ne change pas

## Trois passes

| Passe | Ce qu'elle demande | Sur quoi elle travaille |
|---|---|---|
| `RuleAnalyzer` | si chaque valeur est dans sa plage, n'est pas `null`, est un membre connu de l'enum | n'importe quelle racine |
| `LevelGraphAnalyzer` | si les objets s'accordent entre eux | `Level` uniquement |
| `PublishReadinessAnalyzer` | si le niveau peut être donné à des inconnus selon le profil donné | `LevelMeta`, et `Level` en option |

## Règles

Un type entre dans la vérification grâce au marqueur `[RuleContainer]`. Ses propriétés portent des attributs de règle :
- `[RuleNotNull]`, `[RuleInRange]`, `[RuleMinValue]`, `[RuleEnumValid]`, `[RuleCollectionMaxCount]` et d'autres
- `[RuleEnumFlagsValid]` - pour les enums de drapeaux
- `[RuleOptional]` - pour un champ qui peut manquer

Les limites elles-mêmes sont des constantes dans les tables de `Rules/` : `FrameRules`, `ValueRules`, `LevelRules` et d'autres. Par exemple, `LevelRules.MaxObjects` vaut 262 144

Le parcours de tous les conteneurs de règles est généré par `BH.SDK.Roslyn`, sans réflexion. Sur les grands niveaux, cela divise son temps à peu près par deux

## Réparations

Chaque attribut de règle peut réparer sa propre valeur (`Fix`).
`RuleFixer` applique les réparations dans l'ordre inverse de la trace : une réparation peut déplacer des problèmes plus profonds. `ValidateAndFix` répète la passe jusqu'à ce que le résultat ne change plus

La passe du graphe tourne après les réparations. Une réparation peut elle-même créer un problème dans le graphe, par exemple un nouvel id qui coïncide avec un id existant

**Les problèmes du graphe ne sont jamais réparés :** `DuplicateObjectId`, `MissingParent`, `ParentCycle`, `PrefabRemapBroken`, `IdCounterNearExhaustion` et les autres. Chacune de ces réparations est une décision sur le contenu (lequel des deux objets garde son id). Une supposition réécrirait le niveau

> [!caution] Attention
> `ValidateAndFix` modifie l'objet que tu lui passes. Lance-le sur une copie si tu as besoin de l'original, par exemple pour montrer à l'auteur ce qui a changé exactement
