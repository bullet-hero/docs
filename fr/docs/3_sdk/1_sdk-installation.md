---
title: Installation
date: 2026-10-02
tags: [developer, level_author]
---

# Installation

Le SDK, c'est le paquet BulletHero.SDK sur nuget.org, ou une compilation depuis les sources. Unity le prend comme sous-module git, et l'exemple ConsoleSmoke vérifie que tes niveaux se lisent

Le code du SDK se trouve sur [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk). La licence est MIT

## .NET

Le paquet `BulletHero.SDK` est publié sur nuget.org : `dotnet add package BulletHero.SDK`. Les trois dépendances arrivent avec lui. Pour le compiler plutôt depuis les sources :

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

Ensuite, branche l'un des deux :
- le `.nupkg` depuis un dossier local : `dotnet add package BulletHero.SDK --source <folder>`. Les trois dépendances arrivent avec lui
- `BH.SDK.dll` directement. Ajoute alors toi-même les trois paquets ci-dessous : une référence à une DLL n'apporte pas ses dépendances

Les dépendances, toutes depuis NuGet :

| Paquet | Version | À quoi il sert |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | OpenPGP pour les niveaux protégés par mot de passe |
| `SharpZipLib` | 1.4.2 | tar et zip (gzip vient de la BCL) |

### Détails de la compilation

- l'assembly est `BH.SDK.dll`, et sa documentation XML se trouve à côté
- la cible est `netstandard2.1`, le langage est C# 9. Ce sont les mêmes valeurs que dans le projet Unity, donc les mêmes sources compilent dans Unity comme en dehors
- les dossiers de sortie sont `bin~` et `obj~`. Le tilde est nécessaire, car Unity n'importe pas les dossiers dont le nom se termine par ce caractère

## Unity

Le jeu branche le SDK comme sous-module git :

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

Pour le retirer : `git rm -r -f Assets/Plugins/BH.SDK`

Ce que le projet Unity doit fournir lui-même :
- `Newtonsoft.Json` via le paquet `com.unity.nuget.newtonsoft-json`
- `BouncyCastle.Cryptography` et `SharpZipLib` depuis NuGet (le jeu les installe avec NuGetForUnity)
- le symbole de compilation `BHSDK_UNITY` dans les Player Settings. Sans lui, `UnityIntegration` prend la branche sans moteur
- `BH.SDK.Roslyn.dll` à la racine du SDK. Unity n'applique un analyseur qu'à l'assembly de son dossier et aux assemblies qui la référencent. Déplacé ailleurs, il n'analyse plus rien

La racine du dépôt contient un `package.json` avec le nom `com.vertoker.bullet-hero-sdk` et une version minimale d'Unity `6000.0`. Le Package Manager peut donc aussi ajouter le SDK par URL git. Cette voie n'est pas utilisée et n'est pas décrite ici

## Vérifier : l'exemple ConsoleSmoke

`Samples~/ConsoleSmoke` est une application console `net8.0`. Elle référence le `BH.SDK.dll` compilé, exactement comme le ferait un outil tiers.
L'application lit un dossier de niveau et affiche le nom, le nombre d'objets et la génération. Ensuite, elle fait faire au niveau un aller-retour par JSON et par `.blob`

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| Code de sortie | Signification |
|---|---|
| 0 | tout correspond |
| 1 | arguments incorrects |
| 2 | `level.*` ou `metadata.*` introuvable |
| 3 | un aller-retour ne correspond pas |
| 4 | le fichier est plus récent que ce SDK |

La sortie sur le niveau intégré du jeu `new-zero-demo` (enregistrée avec `sv 1.0.0`) :

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

Suite - [[2_level-format]]

## De quoi est fait le SDK

| Partie | Ce que c'est | Besoin d'Unity |
|---|---|---|
| `BH.SDK` | le cœur : modèles, sérialisation, versions, règles, validation, archives, publication, générateurs | non |
| `UnityIntegration` | une couche fine dont chaque fichier compile avec et sans Unity (`#if BHSDK_UNITY`), par exemple le logger `Cat` | non : hors d'Unity, elle est compilée directement dans le cœur |
| `UnityExtensions` | conversions vers les types d'Unity, transformations 2D, mouvement de l'avatar | oui, toujours |
| `BH.SDK.Roslyn` | des analyseurs et un générateur de sources. Pour chaque modèle marqué `[GenerateModel]`, il écrit `Equals`, la copie, les codecs JSON et `.blob` et le parcours de validation | s'exécute à la compilation |

Un fichier de modèle ne contient que ses champs et ses constructeurs. Tout ce qui se répète est écrit par le générateur. Ainsi, un champ ne peut pas être oublié dans l'un des sept corps générés

## Pourquoi une bibliothèque à part

- **Les niveaux survivent au jeu.** Un niveau est un dossier de fichiers dans des formats ouverts (JSON, tar.gz, zip, OpenPGP). Le code qui les lit est ouvert lui aussi. Un niveau reste lisible même quand le jeu qui l'a écrit a disparu
- **Compatibilité avec d'autres jeux de rythme.** Le format est décrit publiquement, donc un convertisseur vers ou depuis un autre jeu peut s'écrire en s'appuyant dessus
- **Des corrections rapides.** Un défaut du format se voit de l'extérieur. Quiconque lit le code peut le signaler ou envoyer une correction
- **Des outils tiers.** Un convertisseur, un validateur, un générateur de niveaux ou un mod travaille avec les mêmes modèles que le jeu. Pas besoin de les reconstituer à partir des fichiers
- **Les serveurs.** Le cœur compile sans Unity en `netstandard2.1`. Un serveur exécute donc les mêmes vérifications sur les mêmes modèles que le client
