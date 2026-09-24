---
title: Sharing a level by hand
date: 2026-09-24
tags: [level_author]
---

# Sharing a level by hand

What an archive carries, the five shapes it can take, and the tar, zip and gpg lines that make and open each of them

A level is a folder of files. An archive is that folder packed for sending.
Everything the level uses travels with it: the song, the images, the cover. Unpacked on another machine, the level plays straight away

Where the other person puts the level - [[2_metadata-and-sharing#Sharing a level today]]

## What stays out of the archive

- a resource the level fetches from a link. The link stays as it was
- a file nothing in the level references

The game's export report lists both. More - [[13_export-and-protection#Export level]]

## The five shapes

Each opens with tools that already exist on the other side:

| File | What it holds | Opens with |
|---|---|---|
| `level.json.gpg` | the level document alone, behind a password, sitting in the level folder | gpg |
| `LEVEL_FOLDER.tar.gz` | the whole folder as one archive | 7-Zip, Keka, Ark, Explorer |
| `LEVEL_FOLDER.tar.gz.gpg` | the same archive behind a password | gpg |
| `LEVEL_FOLDER.zip` | the same folder as a zip | Windows on a double click, with nothing installed |
| `LEVEL_FOLDER.zip.gpg` | that zip behind a password | gpg |

By default the game puts the password on an archive with the zip's own AES-256. Any archiver but Explorer opens it by asking for the password.
The game writes the `.gpg` shapes on request

## Before running the lines

Replace two things in the lines:
- `LEVEL_FOLDER` - the level's own folder name, which is its id. It is the long string of digits and letters the folder in `levels` is called
- `YOUR_PASSWORD` - the password itself

A password written into a command line stays in the shell history.
Drop `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` from a line, and gpg asks for the password on screen

## The level document with gpg

Encrypting writes `level.json.gpg` beside the original. The original stays where it is: delete it yourself once you have checked the result.
Decrypting writes the document out under its own name again. The encrypted file stays:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## A tar.gz archive

The folder is packed from the inside: the archive holds the level's own files, with no folder around them.
To unpack, the target folder must already exist, tar will not create it. `mkdir` works the same in cmd, in PowerShell and in a terminal on Mac or Linux:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

Packing and encrypting in one pass. An unprotected archive never touches the disk.
The second line decrypts and unpacks the archive back into the same folder:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## A zip archive

On Windows - in PowerShell, which every Windows machine has. The star packs what is inside the folder, not the folder itself.
`Expand-Archive` creates the folder itself, so no `mkdir` first:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

On Mac or Linux - zip and unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

A zip with a password 7-Zip will ask for is made by 7-Zip itself. It has to be installed:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## The game reads them back

All shapes work in both directions. What the game writes, gpg, tar and zip open. What gpg, tar and zip make, the game reads.
That is why standard tools were chosen instead of a format of the game's own

> [!tip] Tip
> The game reads what a file is, not what it is called. So a renamed archive still opens. `7z` is the one format it recognises and refuses: it names the format instead of calling the file broken. Re-pack such an archive as a zip

> [!caution] Caution
> **A FORGOTTEN PASSWORD CANNOT BE RECOVERED**. No key is kept anywhere: not in the game, not in the file, not by the developers. There is no reset, no recovery and no way in. A level whose password is lost is lost with it. Write the password down before you close the editor

Next: [[4_level-folder-and-backups|The level folder and backups]], [[4_not-losing-work|Not losing your work]]
