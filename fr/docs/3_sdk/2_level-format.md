---
title: Format de niveau
date: 2026-10-02
tags: [developer, level_author]
---

# Format de niveau

Un niveau est un dossier : le contenu dans level.json ou level.blob, les métadonnées dans metadata.json ou metadata.blob, une couverture et des fichiers médias. Les sauvegardes, les records et les paramètres du joueur restent sur l'appareil

## Le dossier du niveau

Chaque nom de fichier d'un dossier de niveau est fixé dans `FileNames` :

| Fichier | Modèle | Ce qu'il contient |
|---|---|---|
| `level.json` ou `level.blob` | `Level` | le contenu : paramètres, objets et événements, audio, ressources, aides |
| `metadata.json` ou `metadata.blob` | `LevelMeta` | titre, description, auteurs, licence, un enregistrement par ressource, une référence à la couverture |
| `logo.png` ou `logo.jpg` | - | la couverture |
| morceau, images, polices | - | les fichiers médias auxquels le niveau renvoie |

**L'extension, c'est le format.** Il n'est écrit nulle part à l'intérieur des fichiers. Le lecteur regarde quel fichier existe : `level.json` ou `level.blob`

Le niveau et les métadonnées choisissent leur format indépendamment l'un de l'autre. Par exemple, le niveau intégré `new-zero-demo` garde `level.blob` à côté de `metadata.json`

**`metadata.json` est un fichier séparé exprès.** Un catalogue affiche mille niveaux à partir de mille petits fichiers de métadonnées. Pas un seul niveau n'est ouvert pour cela

## Ressources

Une ressource est adressée par une paire `uri` et `uri_type` (`ResourceUriType`) :

| Valeur | Type | Où se trouve le fichier |
|---|---|---|
| 1 | `LevelPath` | dans le dossier du niveau. Seul ce type rend un niveau portable |
| 2 | `AbsolutePath` | ailleurs sur cet appareil |
| 3 | `DirectUrl` | téléchargé par le réseau |
| 4 | `StreamingAssets` | livré avec le jeu, pas avec le niveau |

`AbsolutePath` apparaît quand un niveau est créé autour d'un morceau. L'export d'une archive copie un tel fichier à l'intérieur. Plus - [[4_archives]]

La couverture est accessible via `LevelMeta.LevelLogo`, comme toute autre ressource. Le choix entre `logo.png` et `logo.jpg` dépend des octets du fichier lui-même, pas du nom de l'image source

L'enregistrement de paternité de la couverture est un `ResourceMeta` avec `resource_type` 9 (`LevelLogo`). Ni `resource_id` ni `resource_guid` n'y sont remplis : un niveau n'a qu'une couverture, donc le type est toute l'adresse

## Déclarations d'IA

`LevelMeta` et chaque `ResourceMeta` portent `ai_generated` de type `AiGeneration` :

| Valeur | Nom | Ce que cela signifie |
|---|---|---|
| 0 | `NotSpecified` | rien de déclaré, inconnu. La valeur par défaut, et une clé absente se lit ainsi |
| 1 | `No` | déclaré comme fait sans génération par IA |
| 2 | `Yes` | déclaré comme généré par IA |

Dans `LevelMeta`, elle ne couvre que le contenu propre du niveau. Chaque ressource et la couverture se déclarent dans leurs propres enregistrements.
Le fait qu'un niveau contienne du contenu d'IA n'est pas stocké : `LevelMeta.ContainsAiContent()` répond à cette question, et seul `Yes` compte

## Ce qui ne voyage pas avec un niveau

Ces fichiers se trouvent à côté du dossier `levels`, jamais dans un dossier de niveau. Archiver, envoyer ou supprimer un niveau n'y touche pas :

| Dossier ou fichier | Ce que c'est | Pourquoi il reste |
|---|---|---|
| `backups/` | les enregistrements automatiques de l'éditeur, un dossier par id de niveau, `backup_level_<time>.<extension>` | une copie dans le dossier qu'elle protège serait supprimée avec lui |
| `stats/` | records et progression par `LevelId` et `statistics.json` | un niveau envoyé par quelqu'un arriverait déjà terminé |
| `settings.json` | `UserSettings`, les paramètres du joueur pour tout l'appareil | ils appartiennent au joueur, pas au niveau |
| `resources/themes`, `effects`, `shapes`, `prefabs` | les bibliothèques partagées de l'appareil | tous les niveaux de l'appareil les partagent |
| `reports/` | rapports de diagnostic | - |

## Clés JSON

Le JSON est toujours écrit compact, sans indentation. Pour le lire à l'œil, formate-le dans un éditeur de texte

**La longueur d'une clé dépend du nombre de fois où elle apparaît dans un niveau :**
- une clé qui apparaît une fois par fichier s'écrit en mots entiers en `snake_case` : `level_id`, `min_generation`
- une clé qui se répète des milliers de fois est réduite à quelques lettres : `objs`, `f`, `e`, `v`

Les clés occupent 52 % des octets d'un fichier de niveau, c'est donc une règle, pas une affaire de goût. Toutes les clés sont déclarées dans `Names.cs`

**Une valeur polymorphe s'écrit `[tag, data]`.** Une chaîne simple donne `[0,{"v":"Author"}]`, une chaîne localisée `[1,{"strs":[...]}]`

Les enveloppes d'identifiants comme `ObjectId` s'écrivent comme un nombre ou une chaîne nus

## Identifiants

**Le signe d'un identifiant entier a un sens.** `0` signifie toujours "non défini" :

| Identifiant | Clé JSON | Positif | Négatif |
|---|---|---|---|
| `ObjectId` | `id`, et `pid` pour le parent | un objet du niveau | un objet du jeu : `-1` la caméra, `-2` le joueur local, `-3` la racine d'un modèle de prefab |
| identifiants de ressources | `txid`, `fnid`, `auid`, `byid`, `ttid` | une ressource livrée avec le jeu | une ressource propre au niveau |
| `AudioId` d'une piste audio | `aid` | une piste de ce niveau | non utilisé |

Un `pid` égal à `0` signifie que l'objet n'a pas de parent. Les nombres inférieurs à `-3` n'existent que pendant l'exécution du jeu et n'atteignent jamais un fichier

**`Marker`, `Checkpoint` et `BeatSegment` n'ont pas d'identifiant.** Leur adresse est une place dans le temps : pour un marqueur et un checkpoint, c'est l'image `f`, pour un segment de pulsation, c'est la première image de son intervalle `sp` (les segments ne se chevauchent pas). Si un tel objet est déplacé, son adresse change

**Un remplacement de prefab désigne un champ par un numéro, pas par une clé JSON.** Un placement garde ses remplacements dans la liste `mod`. La `key` de chaque remplacement contient trois nombres :
- `id` - l'objet à l'intérieur du modèle, pas sa copie dans le niveau
- `f` - le numéro permanent du champ
- `i` - l'élément d'un champ liste, ou `-1` pour le champ entier

Le numéro est lié au champ pour toujours. Renommer la clé JSON de ce champ ne casse pas les remplacements déjà enregistrés dans les niveaux

## Le "g" extérieur

Chaque racine de sérialisation est enveloppée dans une enveloppe à deux clés :

```json
{"g":2,"v":{"level_id":"18df5f61-3aa4-4812-bf69-d357f2201bc3","vrs":"1.0", ... }}
```

`g` est la génération du modèle (`Names.Generation`), `v` les données

Les enveloppes s'imbriquent. Dans `Level`, `LevelSettings`, `GameLevel`, `AudioLevel`, `LevelResources` et `LevelHints` ont chacun leur propre enveloppe. Comment fonctionnent les générations - [[5_versioning]]

> [!caution] Attention
> `g` et `vrs` sont deux nombres différents. `vrs` est la version du niveau donnée par l'auteur (`LevelMeta.LevelVersion`), elle n'a rien à voir avec le format. Ne modifie pas `g` à la main : un fichier dont le `g` est plus élevé que ce que connaît la compilation n'est pas lu du tout
