---
title: Comment partager un niveau à la main
date: 2026-10-01
tags: [level_author]
---

# Comment partager un niveau à la main

Empaquette le dossier du niveau en zip ou en tar.gz, et chiffre-le avec gpg pour un mot de passe. Sur une autre machine, le niveau décompressé se joue tout de suite, et le jeu lit lui-même ces archives

Un niveau est un dossier de fichiers. Une archive est ce même dossier, empaqueté pour l'envoi.
Tout ce que le niveau utilise voyage avec lui : le morceau, les images, la couverture

Où le destinataire met le niveau - [[2_metadata-and-sharing#Partager un niveau aujourd'hui]]

## Ce qui n'entre pas dans l'archive

- une ressource que le niveau prend depuis un lien. Le lien reste tel quel
- un fichier auquel rien dans le niveau ne renvoie

Le rapport d'export du jeu liste les deux. Plus - [[13_export-and-protection#Exporter le niveau]]

## Cinq types

Chacun s'ouvre avec des outils que l'autre côté a déjà :

| Fichier | Ce qu'il contient | S'ouvre avec |
|---|---|---|
| `level.json.gpg` | seulement le document du niveau, derrière un mot de passe, posé dans le dossier du niveau | gpg |
| `LEVEL_FOLDER.tar.gz` | tout le dossier en une seule archive | 7-Zip, Keka, Ark, l'Explorateur |
| `LEVEL_FOLDER.tar.gz.gpg` | la même archive derrière un mot de passe | gpg |
| `LEVEL_FOLDER.zip` | le même dossier en zip | Windows par un double-clic, rien à installer |
| `LEVEL_FOLDER.zip.gpg` | le même zip derrière un mot de passe | gpg |

Par défaut, le jeu protège l'archive par un mot de passe avec les moyens propres au zip, en AES-256. N'importe quel archiveur sauf l'Explorateur ouvre une telle archive : il demande le mot de passe.
Le jeu écrit les types `.gpg` sur demande

## Avant de lancer les lignes

Remplace deux endroits dans les lignes :
- `LEVEL_FOLDER` - le nom du dossier du niveau, c'est-à-dire son id. C'est une longue suite de chiffres et de lettres, le nom du dossier dans `levels`
- `YOUR_PASSWORD` - le mot de passe lui-même

Un mot de passe tapé dans la ligne de commande reste dans l'historique du shell.
Retire `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` de la ligne, et gpg demande le mot de passe à l'écran

## Le document du niveau avec gpg

Le chiffrement place `level.json.gpg` à côté de l'original. Le fichier original reste où il est : supprime-le toi-même une fois le résultat vérifié.
Le déchiffrement réécrit le document sous son propre nom. Le fichier chiffré reste où il est :

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## Une archive tar.gz

Le dossier est empaqueté depuis l'intérieur : l'archive contient les fichiers du niveau eux-mêmes, sans dossier autour.
Pour décompresser, le dossier cible doit déjà exister, tar ne le crée pas. `mkdir` fonctionne de la même façon dans cmd, dans PowerShell et dans un terminal sur Mac ou Linux :

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

L'empaquetage et le chiffrement en une seule passe. L'archive non protégée n'atteint jamais le disque.
La deuxième ligne déchiffre et décompresse l'archive dans le même dossier :

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## Une archive zip

Sur Windows - dans PowerShell, que chaque machine possède. L'étoile empaquette le contenu du dossier, pas le dossier lui-même.
`Expand-Archive` crée le dossier lui-même, pas besoin de `mkdir` avant :

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

Sur Mac ou Linux - zip et unzip :

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

Un zip avec un mot de passe que 7-Zip demandera se fait avec 7-Zip lui-même. Il doit être installé :

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## Le jeu les relit

Tous les types fonctionnent dans les deux sens. Ce que le jeu a écrit, gpg, tar et zip l'ouvrent. Ce que gpg, tar et zip ont fait, le jeu le lit.
C'est pourquoi des outils standard ont été choisis, et pas un format maison

> [!tip] Conseil
> Le jeu regarde ce qu'est un fichier, pas comment il s'appelle. Donc une archive renommée s'ouvre quand même. Le jeu reconnaît `7z` mais ne l'accepte pas : il nomme le format au lieu de déclarer le fichier cassé. Réempaquette une telle archive en zip

> [!caution] Attention
> **UN MOT DE PASSE OUBLIÉ NE PEUT PAS ÊTRE RÉCUPÉRÉ**. La clé n'est stockée nulle part : ni dans le jeu, ni dans le fichier, ni chez qui que ce soit. Il n'y a ni réinitialisation, ni récupération, ni contournement. Un niveau dont le mot de passe est perdu est perdu avec lui. Note le mot de passe avant de fermer l'éditeur

Suite : [[4_level-folder-and-backups|Le dossier du niveau et les sauvegardes]], [[4_not-losing-work|Ne pas perdre son travail]]
