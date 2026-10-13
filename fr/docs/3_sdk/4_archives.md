---
title: Archives et protection
date: 2026-10-01
tags: [developer, level_author]
---

# Archives et protection

Un niveau s'exporte en dossier, en tar.gz ou en zip, avec un mot de passe en option : zip avec AES-256 ou OpenPGP. Le SDK détecte le format d'un fichier reçu par ses premiers octets, pas par son nom

## Modes d'export

Un niveau quitte l'appareil sous l'une des formes de `LevelExportMode` :

| Valeur | Mode | Ce qui est écrit | Protection |
|---|---|---|---|
| 0 | `Folder` | un dossier simple, de la même forme que sur le disque | aucune |
| 1 | `FolderProtectedLevel` | un dossier où seul `level.json.gpg` est chiffré | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | aucune |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | aucune |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | `<name>.zip` avec des entrées en AES-256 | celle du zip |

Le numéro est l'identité du mode, il ne change jamais. L'ordre dans la liste déroulante de l'éditeur est fixé à part (`DisplayOrder`)

**Chaque format est un standard ouvert.** `tar -xzf`, `gpg -d` et n'importe quel archiveur les ouvrent sans le jeu :

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## Deux schémas de protection

**`ZipEncrypted` est la façon par défaut de verrouiller un niveau par mot de passe.** Le destinataire a un archiveur, mais très probablement pas gpg

**OpenPGP verrouille un document, un dossier et une archive avec un seul schéma.** Lui seul peut protéger un dossier

Dans `FolderProtectedLevel`, les métadonnées, la couverture et les médias restent lisibles. Le navigateur de niveaux affiche donc toujours la carte

L'extension intérieure reste dans le nom : `level.json.gpg`. C'est exactement le nom que `gpg -c level.json` donne au fichier, donc le format se reconnaît sans deviner

## Ce qui va à l'intérieur

`LevelArchiveBuilder` déduit le contenu à partir du modèle, pas de la liste des fichiers du dossier. Un fichier auquel le niveau ne renvoie pas reste dehors. Le rapport indique combien de ces fichiers ont été laissés

Les références du niveau sont traitées ainsi :
- une ressource en `AbsolutePath` est copiée dans l'archive. Sa référence est réécrite en `LevelPath`, mais seulement dans la copie exportée
- `DirectUrl` reste tel quel et va dans le rapport : une URL ne peut pas voyager dans un fichier
- un fichier manquant va dans le rapport avec le code `archive.resource_missing`

## Détection par les octets

N'importe qui peut écrire un nom de fichier. C'est pourquoi `ArchiveFormatSniffer` décide d'après les 8 premiers octets :

| Premiers octets | Format |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| une étiquette de paquet OpenPGP, vérifiée en dernier | `OpenPgp` : déchiffré puis détecté à nouveau |

> [!warning] Avertissement
> `.7z` n'est ni lu ni écrit. Il est détecté uniquement pour que le refus le nomme (`Unsupported`). La personne recompresse alors le niveau en zip au lieu de conclure que le fichier est cassé

## Lecture

`LevelArchiveReader.ReadAsync` prend un dossier ou un `Stream` avec accès aléatoire. Il renvoie `LevelArchiveContent`, où `LevelArchiveOpenResult` prend l'une de ces valeurs :

| Résultat | Signification |
|---|---|
| `Ok` | lu |
| `PassphraseRequired` | il n'y a pas de mot de passe, il faut le demander |
| `WrongPassphrase` | la personne a déjà saisi un mot de passe, et il est faux |
| `Damaged` | le fichier est endommagé |
| `NotAnArchive` | ce n'est pas une archive |
| `Unsupported` | le format est reconnu mais pas pris en charge |

`PeekMetaAsync` ne lit que les métadonnées, pour une carte ou un catalogue

Un serveur lit ce que quelqu'un a choisi d'envoyer. Le lecteur travaille donc dans les limites de `ArchiveLimits`. Par défaut, ce sont :
- 4096 entrées
- 512 Mio par entrée
- 1 Gio au total

Rien n'est décompressé en dehors du stockage qui lui a été donné

L'export du côté de l'éditeur - [[13_export-and-protection]]
