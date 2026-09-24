---
title: Sharing a level by hand
date: 2026-09-24
tags: [level_author]
---

# Sharing a level by hand

What an archive carries, the five shapes it can take, and the tar, zip and gpg lines that make and open each of them

A level is a folder of files, and an archive is that folder made portable. Everything the level uses travels with it - the song, the images, the cover - so unpacking one on another machine gives a level that plays. Where the other person puts it is in [[2_metadata-and-sharing#Sharing a level today]]

Only a resource fetched from a link stays behind, still pointing where it pointed, and a file nothing references is not packed. The game's export report lists both, see [[13_export-and-protection#Export level]]

## The five shapes

Each opens with tools that already exist on the other side:

| File | What it holds | Opens with |
|---|---|---|
| `level.json.gpg` | the level document alone, behind a password, sitting in the level folder | gpg |
| `LEVEL_FOLDER.tar.gz` | the whole folder as one archive | 7-Zip, Keka, Ark, Explorer |
| `LEVEL_FOLDER.tar.gz.gpg` | the same archive behind a password | gpg |
| `LEVEL_FOLDER.zip` | the same folder as a zip | Windows on a double click, with nothing installed |
| `LEVEL_FOLDER.zip.gpg` | that zip behind a password | gpg |

The game's own password on an archive is the zip's AES-256 by default, which any archiver but Explorer opens by asking. It writes the `.gpg` shapes on request

## Before running the lines

Two things are placeholders. `LEVEL_FOLDER` is the level's own folder name, which is its id - the long string of digits and letters the folder in `levels` is called. `YOUR_PASSWORD` is the password itself

A password written into a command line stays in the shell history afterwards. Drop `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` from any line below and gpg asks for it on screen instead

## The level document with gpg

Encrypting writes `level.json.gpg` beside the original and leaves the original where it is, so delete it yourself once you have checked the result. Decrypting writes the document out under its own name again, and the encrypted file stays:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## A tar.gz archive

The folder is packed from the inside, so the archive holds the level's own files rather than a folder containing them. Both unpacking lines need the target folder to exist already, because tar will not create it, and `mkdir` works the same in cmd, in PowerShell and in a terminal on Mac or Linux:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

Packing and encrypting in one pass writes nothing between the two steps, so an unprotected archive never touches the disk. The second line decrypts and unpacks it back into the same folder:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## A zip archive

In PowerShell, which every Windows machine already has. The star packs what is inside the folder rather than the folder itself, and `Expand-Archive` creates the folder itself, so no `mkdir` first:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

On Mac or Linux the same two lines are zip and unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

A zip with a password 7-Zip will ask for needs 7-Zip installed:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## The game reads them back

All of them work in both directions - what the game writes, gpg, tar and zip open, and what gpg, tar and zip make, the game reads. That is the whole reason for using standard tools instead of a format of our own

> [!tip] Tip
> The game reads what a file IS rather than what it is called, so a renamed archive still opens. 7z is the one format it recognises and refuses: it says so by name instead of calling the file broken, and re-packing it as a zip is enough

> [!caution] Caution
> **A FORGOTTEN PASSWORD CANNOT BE RECOVERED**. No key is kept anywhere - not in the game, not in the file, not by the developers. There is no reset, no recovery and no way in. A level whose password is lost is lost with it, so write the password down somewhere before you close the editor

More: [[4_level-folder-and-backups|The level folder and backups]], [[4_not-losing-work|Not losing your work]]
