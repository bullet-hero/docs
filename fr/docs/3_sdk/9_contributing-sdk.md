---
title: Contribuer au SDK
date: 2026-10-02
tags: [developer]
---

# Contribuer au SDK

Les problèmes du SDK se signalent dans les issues du dépôt bullet-hero/sdk, et les modifications du code s'y envoient en pull requests. Les règles pour les contributeurs se trouvent dans le même dépôt, à côté du code

Le dépôt est [bullet-hero/sdk](https://github.com/bullet-hero/sdk), la branche par défaut est `master`

## Où signaler

| À propos de quoi | Où |
|---|---|
| le SDK et son code | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| le jeu : bugs et demandes des joueurs | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| le texte de la documentation | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## Où sont les règles

Les règles pour les contributeurs se trouvent dans le dépôt du SDK lui-même, à côté du code qu'elles décrivent :

| Fichier | Ce qu'il contient |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | dépendances, paquets de niveaux, compilation de la DLL et du paquet, l'exemple de vérification |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | le modèle mental, un index des dossiers et les conventions de toute la bibliothèque |
| `CLAUDE.md` dans chaque dossier | les règles locales de ce dossier, par exemple [Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md), [Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md), [Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | axes de version, générations, migration et refus |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | comment le modèle adresse les entités : Guid, int, image, chemin de champ |
| [[ugc-licensing-policy]] (sur ce site) | la politique de licences du contenu des utilisateurs, modifiée en même temps que `TrustedSourceCatalog` |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | comment écrire un instantané et un migrateur |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | le contrat des générateurs |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | les analyseurs et le générateur de modèles, comment les recompiler |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | le contrat de double compilation |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | les changements par version `sv`, la plus récente en haut |

## Compilation et tests

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- ici, les mêmes sources que compile Unity sont compilées sans Unity. Un fichier qui rompt le contrat d'indépendance vis-à-vis du moteur casse cette compilation
- la sortie va dans `bin~` et `obj~`
- la commande pack ne fait que créer un `.nupkg`. La publication sur nuget.org est faite par le workflow `release` du dépôt quand un tag `sv` est poussé

> [!caution] Attention
> Les analyseurs et le générateur de modèles sont livrés sous forme de `BH.SDK.Roslyn.dll` précompilé à la racine du SDK. Après avoir modifié quoi que ce soit dans `Roslyn/`, recompile-le et copie-le par-dessus. Sinon, l'ancien générateur continue de tourner, même si les sources disent autre chose

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

Dans l'éditeur Unity, l'élément de menu **Tools > BH.SDK.Roslyn > Build Analyzer** fait la même chose

## Invariants à connaître d'avance

- le cœur ne référence pas un seul type de `UnityEngine`. Le code qui a besoin du moteur va dans `UnityExtensions/` ou dans `UnityIntegration/` derrière `#if BHSDK_UNITY`, avec une branche sans moteur
- le code fonctionne de la même façon avec des fichiers et avec des données en mémoire et n'utilise que l'asynchronisme de la BCL
- `netstandard2.1` et C# 9 sont ce avec quoi compile le projet Unity. On ne les monte pas
- un modèle est une `[GenerateModel] public sealed partial class`. Chaque champ sérialisé prend sa clé dans `Names.cs`
- toute modification d'un modèle est une nouvelle génération avec un instantané et un migrateur. Plus - [[5_versioning]]
- la version du SDK vit à trois endroits : `SdkVersion.cs`, `package.json` et `<Version>` dans `BH.SDK.csproj`. `SdkVersionAgreementTests` échoue si l'un d'eux a bougé seul
