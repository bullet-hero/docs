---
title: Format Blob
date: 2026-10-01
tags: [developer]
---

# Format Blob

Un fichier .blob contient les mêmes données que le .json, sous forme binaire : un en-tête de 24 octets suivi des données. C'est un format de niveau à part entière, pas un cache

Un niveau peut être enregistré uniquement en `.blob`

| Niveau `volcano`, 19 341 objets | Taille |
|---|---|
| `level.json` | 15,7 Mo |
| `level.blob` | 5,1 Mo, lu en 203 ms |

`.blob` ne promet aucune lisibilité. On ne peut ni le lire à l'œil ni le comparer avec un diff, c'est pourquoi il n'est le format par défaut nulle part

Le codec de chaque modèle est créé par le générateur Roslyn

## En-tête

| Décalage | Taille | Champ | Valeur |
|---|---|---|---|
| 0 | 4 | magic | `uint` `0x4F424842`, octets `42 48 42 4F` (`BHBO`) |
| 4 | 2 | génération du codec | `ushort`, `BlobFormat.Generation` = 1 |
| 6 | 2 | drapeaux | `ushort`, bit 0 `FlagHashed` = un hash est présent. Les autres bits sont réservés et doivent valoir 0 |
| 8 | 8 | longueur des données | `long` |
| 16 | 8 | hash | `ulong`, xxHash64 des données avec la génération du codec comme graine |

La longueur de l'en-tête `BlobFormat.HeaderLength` est de 24 octets, suivis des données

## Ordre des vérifications

`BlobFormat.ReadHeader` vérifie l'en-tête dans un ordre strict. Rien n'est alloué tant que l'en-tête n'est pas validé :
1. le magic
2. la génération du codec vaut 1
3. aucun drapeau inconnu
4. la longueur déclarée est égale à la longueur réelle
5. le hash correspond, si `FlagHashed` est activé

Chaque échec est une `BlobFormatException` avec son propre message. "Le fichier est endommagé" et "le fichier vient d'une compilation plus récente" demandent des choses différentes au joueur, donc ils ne sont pas fusionnés en une seule erreur

Le hash n'est volontairement pas cryptographique. Il détecte les dégâts, et la couche OpenPGP protège contre la falsification. Plus - [[4_archives]]

## Encodage

- little-endian, nombres à largeur fixe, pas de varint
- une chaîne est un nombre d'octets `int` suivi de l'UTF-8
- `null` est une longueur de `-1`. Ainsi, une liste vide et une liste absente restent différentes après un aller-retour
- une valeur polymorphe commence par une étiquette d'un octet, `0xFF` est réservé à `null`. L'étiquette est le `GetModelType()` du modèle, le même marqueur que le JSON écrit dans `[tag, data]`
- un nombre d'éléments lu dans un fichier est vérifié dans `BlobReader.ReadCount` avant que quoi que ce soit soit alloué pour lui

## Enveloppes et deux générations

Chaque racine marquée `[ModelGeneration]` écrit sa propre enveloppe : le domaine sous forme de chaîne, la génération du modèle en `int`, la longueur du contenu, puis le contenu lui-même. Voici comment un outil lit la génération d'un fichier :

```csharp
var bytes = File.ReadAllBytes(path);
var reader = new BlobReader(bytes, BlobFormat.HeaderLength, bytes.Length - BlobFormat.HeaderLength);
var domain = reader.ReadString();
var generation = reader.ReadInt();
```

Il y a ici deux générations différentes :
- **la génération du codec**, dans l'en-tête, décrit la disposition des octets. Quand elle change, chaque ancien `.blob` devient illisible en entier : il n'y a rien sur quoi se replier
- **la génération du modèle**, dans chaque enveloppe, décrit la forme d'un domaine. Une ancienne est migrée, une plus récente est refusée via `NewerGenerationException`. Plus - [[5_versioning]]

On ne peut pas les fusionner en un seul nombre. La génération du modèle se trouve dans l'enveloppe, et seul quelqu'un qui connaît déjà la disposition des octets peut trouver l'enveloppe. Une modification du modèle ne fait jamais bouger la génération du codec

## Étendre l'en-tête

L'en-tête n'a pas d'octets de réserve ni de champ portant sa propre longueur. Il grandit de deux façons :
- **un drapeau.** 15 bits sont libres. Un ancien lecteur refuse un fichier avec un drapeau inconnu plutôt que de le lire de travers
- **une nouvelle génération du codec.** Une nouvelle disposition peut tout changer, y compris la longueur de l'en-tête. Un lecteur plus récent peut lire l'ancienne génération à côté de la nouvelle

Rien ne peut être ajouté après les données. La longueur déclarée doit correspondre à la longueur réelle, donc toute queue en trop est refusée. Les nouvelles données de niveau vont à l'intérieur des données, via la génération du modèle

> [!info] Bon à savoir
> Un contenu qui ne se termine pas exactement à sa longueur déclarée compte comme un dégât, dans les deux sens. Parfois, une racine passe toutes les vérifications de l'en-tête et ne s'analyse quand même pas. Elle est alors sautée grâce à sa longueur et garde ses valeurs par défaut. Le saut est noté dans `SerializationReport`, jamais en silence
