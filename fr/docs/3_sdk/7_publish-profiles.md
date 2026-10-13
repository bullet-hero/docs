---
title: Profils de publication
date: 2026-10-01
tags: [developer, level_author]
---

# Profils de publication

Un service décrit les niveaux qu'il accepte dans un fichier PublishProfile : licences, sources des ressources, champs obligatoires, limites de taille. Ajouter un service, c'est écrire un fichier, pas modifier l'analyseur

## Un profil, ce sont des données

Un profil de publication (`PublishProfile`) est un modèle qui se sérialise comme n'importe quelle autre racine, avec sa propre génération

Un niveau peut aller dans le Steam Workshop, sur le serveur officiel, sur un serveur communautaire, dans le catalogue d'une version pour store. Chaque endroit répond aux mêmes questions à sa façon. Les réponses changent avec les années, le code non

Ce que décide un profil :

| Champ | Signification |
|---|---|
| `ProfileKey` | de quel service il s'agit, répété dans chaque rapport |
| `AllowedLicenses` | les valeurs de `TypicalLicenseType` que le service accepte |
| `AllowedUriTypes` | comment les ressources peuvent être récupérées. Une liste vide autorise toutes les façons |
| `AllowUnknownLicense`, `AllowPermissionInstead` | si une licence inconnue ou une autorisation écrite suffit |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution`, `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | ce qui doit être rempli |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | limites de taille, 0 signifie sans limite |
| `Sources`, `UnknownSourceTrust` | une liste de sites et la note d'un site qui n'y figure pas |

Seul le profil décide quelles licences sont acceptables. Cela ressemble à une propriété de la licence, mais c'est en fait une propriété du service qui reçoit le niveau

## Quatre profils intégrés

| Fabrique | `ProfileKey` | Pour quoi |
|---|---|---|
| `CreateOpen()` | `local` | un niveau sur ton appareil. Rien n'est exigé |
| `CreateStandard()` | `standard` | un serveur public |
| `CreateWorkshop()` | `workshop` | le Steam Workshop. Toute variante de CC BY passe, les documents manquants ne donnent qu'un avertissement |
| `CreateStrict()` | `strict` | une version pour store, plus stricte que `standard` |

| Quoi | `standard` | `strict` |
|---|---|---|
| licences | CC0 1.0, CC BY 4.0 et 3.0, CC BY-NC 4.0 et 3.0, SIL OFL 1.1, MIT, Apache 2.0, the Unlicense | comme dans `standard` |
| provenance des ressources | depuis le dossier du niveau, depuis le jeu ou par lien direct | pas de liens |
| attribution et hashes | - | obligatoires |
| limite par ressource | 64 Mio | 32 Mio |
| limite par fichier de données | 32 Mio | 16 Mio |
| limite par niveau | 256 Mio | 128 Mio |

> [!tip] Recommandation
> N'ajoute pas de fabrique pour ton service. Prends l'un des quatre profils, modifie les champs nécessaires et livre-le sous forme de fichier JSON

### Pourquoi ces licences et ces tailles

- les licences de la famille GPL sont exclues de `standard`. Une œuvre sous GPL distribuée par l'App Store entre en conflit avec les conditions d'Apple
- CC BY-SA est exclue : ShareAlike imposerait de changer la licence du niveau lui-même
- CC BY-ND est exclue : NoDerivatives interdit la modification sur laquelle repose le jeu
- les tailles strictes sont ce qu'un téléphone peut télécharger sur un réseau mobile

## D'où vient une ressource

Le champ de licence dit ce que l'auteur affirme. `SourceTrust` dit ce que vaut cette affirmation, compte tenu du site d'où vient la ressource :

| Note | Résultat | Exemples |
|---|---|---|
| `Approved` | publier | Kenney, ccMixter, Incompetech |
| `PartiallyApproved` | publier, l'enregistrement mérite un coup d'œil | Pixabay, SoundImage |
| `RequiresLicenseCheck` | vérifier la licence sur la vraie page | OpenGameArt, Free Music Archive, Wikimedia Commons |
| `RequiresResourceCheck` | identifier d'abord l'œuvre elle-même | Rawpixel, itch.io |
| `NotAllowed` | refuser | YouTube, SoundCloud, Spotify |
| `Unknown` | pas d'enregistrement, `UnknownSourceTrust` décide | - |

`TrustedSourceCatalog.CreateDefault()` renvoie 25 sites. C'est une liste de départ. Chaque opérateur est censé la modifier. Rien n'a donc le droit de compter sur la présence d'un enregistrement

Une liste `Sources` vide désactive la notation des sources

Les plateformes de streaming sont listées en `NotAllowed` au lieu d'être omises. Un site absent est noté via `UnknownSourceTrust`, et dans `standard` et `strict` cette note demande une vérification au lieu de refuser

Le catalogue et [[ugc-licensing-policy]] décrivent la même chose et se modifient ensemble

## Que faire de la réponse

L'appel est `ValidationFacade.ValidateForPublish`. Plus - [[6_validation]]

`PublishReadinessReport` contient :
- `HasErrors` - des problèmes dans le groupe `Error`
- `NeedsManualReview` - des problèmes dans le groupe `Warning`
- `IsReady`

Le profil ne décide pas de la suite. Le client bloque l'envoi en cas d'erreurs. Le serveur place le niveau dans une file de vérification au lieu de le publier

La même vérification du côté de l'auteur - [[5_publish-readiness]]
