---
title: Serveur public et extension
date: 2026-10-02
tags: [server_advanced]
---

# Serveur public et extension

Pour un serveur public, il existe déjà le SDK ouvert : les mêmes modèles et les mêmes vérifications que dans le build client, sans Unity. Le protocole, l'API du serveur et les outils de modération ne sont pas encore décidés

> [!warning] Avertissement
> Il n'y a pas encore de code serveur ni de protocole. Ci-dessous, la partie du SDK sur laquelle le serveur tournera, et elle fonctionne déjà. Les adresses, le format des messages et l'API du serveur lui-même ne sont pas ici, ils n'existent pas

## Le SDK tourne sur un serveur

Le SDK est le modèle de données ouvert du jeu : modèles, sérialisation en JSON et dans un format binaire, règles de validation, générateurs.
Les mêmes sources que compile Unity se construisent comme une bibliothèque `netstandard2.1` ordinaire, sans le moteur. Un serveur ou un utilitaire peut la référencer :

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

Le paquet s'appelle `BulletHero.SDK`. Le code est sur [github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk), sous licence MIT

La version du SDK correspond en général à celle du jeu et ne promet pas encore de stabilité de l'API. Plus - [[5_versioning]]

**Le client et le serveur font les mêmes vérifications sur les mêmes modèles.** Un niveau que l'éditeur considère comme prêt l'est aussi pour le serveur. Il n'y a pas de second jeu de règles à garder en accord

## ValidateForPublish

Un seul appel répond à la question "ce niveau peut-il être publié ici" :

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

Il fait trois passes à la fois :

1. les règles déclaratives sur le niveau et ses métadonnées
2. les vérifications du graphe du niveau
3. les conditions propres au service, tirées de son `PublishProfile`

**Passer le niveau lui-même est facultatif.** `metadata.json` est un fichier séparé pour qu'un catalogue puisse évaluer des milliers de niveaux sans en ouvrir un seul. Cette passe peu coûteuse couvre l'essentiel de la politique

Mais deux vérifications ont besoin de `level.json` : une ressource sans aucune fiche, et la façon dont les ressources sont récupérées. Un rapport propre à partir des seules métadonnées signifie "aucune erreur dans ce qui a été lu". `IsReady` reste `false` tant que le fichier du niveau n'est pas vérifié

`payload` contient les tailles mesurées : de chaque ressource, de `level.json`, de `metadata.json`, du niveau entier. Sans lui, les limites de taille du profil ne peuvent pas être vérifiées

Rien n'est corrigé pendant la vérification, et c'est voulu. Modifier le contenu en silence au moment de la sortie est bien la dernière chose dont un service a besoin. Plus - [[6_validation]]

## Trois verdicts

| Groupe | Signification | Ce que fait le serveur |
|---|---|---|
| `Error` | le service refuse | rejette l'envoi (`HasErrors`) |
| `Warning` | publiable, mais quelqu'un doit regarder | met le niveau dans la file de modération (`NeedsManualReview`) |
| `Advice` | pris en note | rien |

Le client bloque un envoi sur les mêmes erreurs avant même qu'il commence. Un niveau que ton serveur refuserait y arrive rarement

## Ton propre PublishProfile

La politique d'un service est un fichier, un modèle sérialisé du SDK. Un serveur plus strict ou plus souple, c'est un autre fichier, pas un fork du code

**Un niveau qui reste sur l'appareil du joueur n'est pas vérifié du tout.** Le profil ne compte qu'au moment où le niveau est proposé à un service. Comment un auteur prépare un niveau pour ce moment - [[5_publish-readiness]]

Préréglages :

| Préréglage | Clé | Pour quoi |
|---|---|---|
| `CreateOpen()` | `local` | niveaux sur l'appareil, rien n'est exigé |
| `CreateStandard()` | `standard` | un serveur public, la politique de [[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | builds des boutiques, pas de liens directs, un hash sur chaque ressource |

Les champs principaux :

| Champ | Ce qu'il décide |
|---|---|
| `AllowedLicenses` | quelles licences types sont acceptées, une liste vide les accepte toutes |
| `AllowedUriTypes` | comment les ressources peuvent être récupérées, une liste vide autorise tous les moyens |
| `AllowUnknownLicense` | si une ressource peut ne rien dire de ses conditions |
| `AllowPermissionInstead` | si l'autorisation de l'ayant droit peut remplacer une licence refusée (toujours envoyé en vérification) |
| `RequireResourceMeta`, `RequireResourceUrl`, `RequireAttribution` | ce que doit contenir la fiche de chaque ressource |
| `RequireAgeRating`, `RequireLevelAuthors`, `RequireHashes` | ce que le niveau doit déclarer |
| `MaxResourceBytes`, `MaxDataFileBytes`, `MaxTotalBytes` | limites de taille, zéro signifie aucune limite |
| `Sources`, `UnknownSourceTrust` | la liste des sites de confiance et la façon dont un site hors liste est évalué |

Les deux préréglages publics :

| | `standard` | `strict` |
|---|---|---|
| Liens directs vers les ressources | autorisés | interdits |
| Mention de l'auteur sur chaque ressource | non exigée | exigée |
| Hash du contenu dans chaque fiche | non exigé | exigé |
| Plus grande ressource | {{v:publish.standard.max-resource-mb}} Mo | {{v:publish.strict.max-resource-mb}} Mo |
| Plus grand `level.json` ou `metadata.json` | {{v:publish.standard.max-data-file-mb}} Mo | {{v:publish.strict.max-data-file-mb}} Mo |
| Plus grand niveau | {{v:publish.standard.max-level-mb}} Mo | {{v:publish.strict.max-level-mb}} Mo |
| Un site hors liste | `RequiresLicenseCheck` | `RequiresResourceCheck` |

Tous les préréglages et tous les champs - [[7_publish-profiles]]

### Pourquoi standard n'a pas de GPL

Les licences de la famille GPL sont exclues de `standard` exprès. Une œuvre sous GPL distribuée via l'App Store entre en conflit avec les conditions d'Apple. Un catalogue qui les accepterait ne pourrait pas être publié plus tard sur iOS

> [!info] Bon à savoir
> La liste des sites de confiance livrée avec le SDK n'est qu'un point de départ. Les sites changent leurs conditions, donc chaque propriétaire de serveur devrait la redéfinir dans son propre profil. Rien ne peut compter sur la présence d'un site précis dans la liste

## Modération

Ce que le serveur officiel prévoit d'ajouter par-dessus la vérification. Un serveur public en aura très probablement besoin aussi :

- **Une file de modération.** Elle se remplit avec les problèmes `Warning`
- **Signalements et blocage** de niveaux et d'utilisateurs. Les règles de Google Play et de l'App Store exigent les deux pour tout contenu que voient d'autres personnes
- **Suppression par hash.** La fiche d'une ressource peut stocker les hash du contenu de ses fichiers sous la forme `sha256:<hex>`. Un signalement nomme une œuvre, et grâce aux hash chaque niveau qui la contient se trouve par recherche, au lieu d'être deviné d'après les titres. L'éditeur enregistre le hash quand une ressource est importée
- **Conditions d'utilisation.** Elles couvrent ce que la licence ne couvre pas : la déclaration de l'auteur qu'il détient les droits, le droit du propriétaire du serveur de retirer un niveau, le droit d'afficher son titre et sa couverture dans les listes

**Le Steam Workshop fonctionne autrement.** Valve stocke les fichiers, et il n'y a pas de file de modération du côté de Bullet Hero. Le jeu vérifie un niveau ou une collection avant l'envoi, et une erreur bloque l'envoi - [[17_publishing]]. Après la publication, le jeu décide seulement ce qu'il en télécharge

## Formats d'archive

Un niveau est un dossier de fichiers, et une archive le rend portable. Ce que le SDK lit et écrit :

| Format | Lecture | Écriture | Remarque |
|---|---|---|---|
| `.tar.gz` | oui | oui | par défaut |
| `.zip` | oui | oui | peut être chiffré entrée par entrée en AES-256 |
| `.tar.gz.gpg`, `.zip.gpg` | oui | oui | un message OpenPGP protégé par mot de passe, la seule protection possible pour `.tar.gz` |
| `level.json.gpg` | oui | oui | un seul fichier de niveau protégé |
| `.7z` | non | non | détecté pour pouvoir le refuser en le nommant clairement |

Le format est détecté d'après les premiers octets du fichier, pas d'après son extension. Le nom est la seule partie d'un fichier que n'importe qui peut changer

`tar -xzf`, `gpg -d` et n'importe quel archiveur zip ouvrent tous les formats écrits. Le jeu n'est pas nécessaire pour décompresser un niveau. Plus - [[4_archives]]

## Ce qui n'est pas décidé

- le protocole entre le jeu et un serveur, et s'il sera le même pour OWS et NOWS
- l'API du serveur : envoi, catalogue, recherche, comptes
- comment indiquer au jeu un serveur communautaire
- comment le serveur lui-même s'étend, et dans quel langage
- le jeu à plusieurs sur un serveur : transport, autorité, synchronisation du niveau et salons

Pour le jeu à plusieurs, une seule chose a été mise au point : comment l'avatar d'un joueur apparaît et disparaît sur un message réseau

La publication de niveaux sur un service quel qu'il soit n'arrivera pas avant la mise à jour qui suit `gv 1.0.0`. Les données sur lesquelles s'appuie la vérification doivent entrer dans les niveaux avant leur publication

## Licence du niveau et n'importe quel serveur

Par défaut, un niveau est distribué sous *CC BY-NC*, et l'auteur peut choisir une autre licence dans les métadonnées du niveau. L'autorisation de partager un niveau va de son auteur directement à chaque destinataire. Aucun serveur, officiel ou communautaire, ne peut donc héberger un niveau sous *CC BY-NC* à des fins commerciales

Un serveur avec un autre code sous une autre licence ne change rien aux droits sur le contenu. Les règles complètes pour les auteurs - [[ugc-licensing-policy]]
