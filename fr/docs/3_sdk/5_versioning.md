---
title: Versions et migrations
date: 2026-10-02
tags: [developer, level_author]
---

# Versions et migrations

Il y a trois versions : gv pour le jeu, sv pour le SDK, mg pour la génération du format des modèles. D'après mg, le SDK migre un ancien fichier et refuse de lire un fichier dont la génération est plus récente que la compilation

## Trois versions

| Étiquette | Signifie | Ce qu'elle versionne | Où elle se trouve |
|---|---|---|---|
| `gv` | `game version` | le client du jeu | le `bundleVersion` du projet Unity |
| `sv` | `sdk version` | le SDK en tant que bibliothèque, semver sur l'API publique | `SdkVersion.Value` |
| `mg` | `model generation` | le format des modèles, une génération par domaine | `[ModelGeneration]` sur chaque racine, `ModelGenerations.Current` |

Les versions actuelles sont `gv {{v:version.gv}}`, `sv {{v:version.sv}}`, `mg {{v:version.mg}}`

Les numéros `gv` et `sv` ne sont pas tenus de se suivre, mais dans la plupart des cas ils coïncident.
Les versions montent ensemble, et une mise à jour commune porte la même version

Ce que signifie chaque partie :
- `gv` : majeure, c'est une mise à jour globale (histoire, multijoueur), mineure, ce sont de nouvelles fonctionnalités ordinaires, patch, un correctif urgent
- `sv`, à partir du moment où le SDK commencera à promettre une API stable : majeure, c'est un changement d'API incompatible (un type retiré, la signature ou le sens d'un membre modifié), mineure, un ajout auquel personne n'a besoin de réagir, patch, une correction qui ne change aucune signature

**`mg` compte plus que les autres.** C'est d'après lui que le SDK décide de migrer un fichier ou de refuser de le lire

L'écran des paramètres affiche les trois dans cet ordre et avec leurs étiquettes : `gv {{v:version.gv}}, sv {{v:version.sv}}, mg {{v:version.mg}}`. Sans les étiquettes, deux numéros identiques dans un rapport de bug ne se distinguent pas

Une version qui se termine par `b` et un numéro, par exemple `gv 1.1.0b1`, est une bêta : une compilation de la version suivante destinée aux tests, en général sur une branche bêta de Steam. La version qui la suit sort sans la lettre (`gv 1.1.0`). Un fichier enregistré par une bêta peut ne pas s'ouvrir dans la version précédente

> [!warning] Avertissement
> Tant que le SDK n'annonce pas le contraire, `sv` suit le jeu, et `sv 1.0.0` ne promet aucune stabilité d'API. Pour du code compilé contre la DLL, une version majeure de `sv` ne dit encore rien de la compatibilité

## Des numéros qui ne sont pas des versions

Deux autres numéros ressemblent à une "version" mais n'en sont pas :
- `LevelMeta.LevelVersion` (clé `vrs`) - la version du niveau donnée par l'auteur, une chaîne comme `"1.0"`
- `BlobFormat.Generation` - la disposition des octets de `.blob`. Plus - [[3_blob-format]]

## Génération : un entier par domaine

Un domaine est une racine qui migre comme un tout. Il y en a 21 : `Level`, `LevelMeta`, `UserSettings`, `Prefab`, `ThemeData`, `PublishProfile` et d'autres.
Cela inclut les parties à l'intérieur de `Level` : `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources`, `LevelHints`. Chaque domaine écrit sa génération dans la clé `g` de son enveloppe

| Constante | Valeur | Signification |
|---|---|---|
| `ModelGenerations.Invalid` | -1 | aucune génération |
| `ModelGenerations.Test` | 0 | l'échafaudage `Versions/V0` qui fait tourner le chemin de migration |
| `ModelGenerations.V1_AlphaRelease` | 1 | ce que `gv 1.0.0` a livré, la plupart des domaines y sont encore |
| `ModelGenerations.V2_SimplifyEntrance` | 2 | `UserSettings`, `LevelMeta`, `LevelStatistics`, `GameStatistics` et la nouvelle `Collection` |
| `ModelGenerations.Current` | la plus récente | ce qu'affichent l'interface et les rapports |

**Une génération est un seul nombre, pas `major.minor`.** Une modification de la forme d'un fichier exige une migration ou non. Il n'y a pas de degré intermédiaire

**Les numéros viennent d'un seul compteur global.** Un domaine qui a changé reçoit `ModelGenerations.Current + 1`, pas son propre numéro libre suivant. C'est précisément ce qui garde son sens à l'unique `mg` de la chaîne de version

## Le nouveau est refusé

Chaque modification d'un modèle est une nouvelle génération. Un changement de forme, un champ ajouté et une nouvelle valeur d'enum comptent pareil.
Une génération plus élevée que ce que connaît la compilation est donc une forme qu'elle n'a certainement jamais vue

Il y a une exception : un modèle entièrement nouveau qu'aucun modèle existant ne mentionne, par exemple des skins d'avatar dans un fichier à part. C'est un nouveau domaine sans rien à migrer, donc la génération ne monte pas. Ce qui monte, c'est la génération du modèle existant qui commence à y faire référence

Un tel fichier n'est pas lu du tout : pas de valeurs par défaut, pas de parties sautées. `NewerGenerationException` porte `Domain`, `FileGeneration` et `BuildGeneration`, et l'hôte demande au joueur de mettre à jour

```
refused: 'Level' is at generation 2, newer than this build's 1 (domain Level, file 2, this SDK 1) - update the SDK
```

## L'ancien migre

Un domaine qui change de forme reçoit :
1. une nouvelle génération tirée du compteur global
2. un instantané figé de l'ancienne forme dans `Versions/V<old>/` : une classe avec `[GenerateModel]` et `[ModelGeneration(domain, <old>)]`
3. une `ModelMigration<TFrom, TTo>` dans `Versions/V<old>/Migrations/`

```csharp
public class GameEventsV0ToV1 : ModelMigration<GameEventsV0, GameEvents>
{
    public override GameEvents Migrate(GameEventsV0 from) => new();
}
```

`VersionedTypeRegistry` trouve les instantanés et les migrateurs par réflexion et parcourt la chaîne jusqu'à la forme actuelle. Chaque substitution avec perte pendant la lecture va dans `SerializationReport`, pas dans le silence

## Refus avant la lecture

`LevelMeta.MinGeneration` (clé `min_generation`) est la génération la plus élevée parmi les domaines du niveau. Elle est calculée à l'enregistrement par `LevelGenerations.Required()` et n'est jamais saisie à la main

Le client la compare avant d'ouvrir `level.json`. Un niveau venu du futur est donc refusé sans lire des mégaoctets de contenu. Un fichier qui ne déclare rien stocke `-1`

Le registre complet des décisions - [VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) dans le dépôt du SDK
