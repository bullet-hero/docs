---
title: How to share a level by hand
date: 2026-10-01
tags: [level_author]
---

# How to share a level by hand

Pack the level folder into zip or tar.gz, and encrypt it with gpg for a password. On another machine the unpacked level plays right away, and the game reads such archives itself

A level is a folder of files. An archive is the same folder, packed for sending.
Everything the level uses travels with it: the song, the images, the cover

Where the recipient puts the level - [[2_metadata-and-sharing#Sharing a level today]]

## What does not go into the archive

- a resource the level takes from a link. The link stays as it was
- a file nothing in the level refers to

The game's export report lists both. More - [[13_export-and-protection#Export level]]

## Five kinds

Each opens with tools the other side already has:

| File | What is inside | Opens with |
|---|---|---|
| `level.json.gpg` | only the level document, behind a password, sitting in the level folder | gpg |
| `LEVEL_FOLDER.tar.gz` | the whole folder as one archive | 7-Zip, Keka, Ark, Explorer |
| `LEVEL_FOLDER.tar.gz.gpg` | the same archive behind a password | gpg |
| `LEVEL_FOLDER.zip` | the same folder as a zip | Windows with a double click, nothing to install |
| `LEVEL_FOLDER.zip.gpg` | the same zip behind a password | gpg |

By default the game puts a password on the archive with zip's own means, AES-256. Any archiver except Explorer opens such an archive: it asks for the password.
The game writes the `.gpg` kinds on request

## Before running the lines

Replace two places in the lines:
- `LEVEL_FOLDER` - the name of the level folder, that is, its id. It is a long string of digits and letters, the name of the folder inside `levels`
- `YOUR_PASSWORD` - the password itself

A password typed into the command line stays in the shell history.
Remove `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` from the line, and gpg asks for the password on screen

## The level document with gpg

Encryption puts `level.json.gpg` next to the original. The original file stays where it is: delete it yourself once you have checked the result.
Decryption writes the document under its own name again. The encrypted file stays where it is:

```bash
gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json
```

## A tar.gz archive

The folder is packed from the inside: the archive holds the level files themselves, with no folder around them.
To unpack, the target folder must already exist, tar does not create it. `mkdir` works the same in cmd, in PowerShell and in a terminal on Mac or Linux:

```bash
tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .
mkdir LEVEL_FOLDER
tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER
```

Packing and encryption in one pass. The unprotected archive never reaches the disk at all.
The second line decrypts and unpacks the archive back into the same folder:

```bash
tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg
gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER
```

## A zip archive

On Windows - in PowerShell, which every machine has. The star packs the contents of the folder, not the folder itself.
`Expand-Archive` creates the folder itself, no `mkdir` needed beforehand:

```
Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip
Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER
```

On Mac or Linux - zip and unzip:

```bash
cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .
unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER
```

A zip with a password that 7-Zip will ask for is made by 7-Zip itself. It has to be installed:

```
7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*
```

## The game reads them back

All kinds work both ways. What the game wrote, gpg, tar and zip open. What gpg, tar and zip made, the game reads.
That is why standard tools were chosen, not a format of its own

> [!tip] Tip
> The game looks at what a file is, not at what it is called. So a renamed archive still opens. The game recognises `7z` but does not accept it: it names the format instead of declaring the file broken. Repack such an archive as zip

> [!caution] Caution
> **A FORGOTTEN PASSWORD CANNOT BE RECOVERED**. The key is stored nowhere: not in the game, not in the file, not with anyone. There is no reset, no recovery and no workaround. A level with a lost password is lost along with it. Write the password down before you close the editor

Next: [[4_level-folder-and-backups|The level folder and backups]], [[4_not-losing-work|Not losing your work]]
