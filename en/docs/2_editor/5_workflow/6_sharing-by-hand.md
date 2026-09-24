---
title: Sharing a level by hand
date: 2026-09-24
tags: [level_author]
---

# Sharing a level by hand

What an archive carries, the five shapes it can take, and the tar, zip and gpg lines that make and open each of them

A level is a folder of files, and an archive is that folder made portable. Everything the level uses travels with it - the song, the images, the cover - so unpacking one on another machine gives a level that plays

There are five shapes, and each opens with tools that already exist on the other side:
`level.json.gpg` - the level document alone, behind a password, sitting in the level folder
`LEVEL_FOLDER.tar.gz` - the whole folder as one archive. 7-Zip, Keka and Ark all open it, and so does Explorer
`LEVEL_FOLDER.tar.gz.gpg` - the same archive behind a password
`LEVEL_FOLDER.zip` - the same folder as a zip. Windows opens it on a double click with nothing installed
`LEVEL_FOLDER.zip.gpg` - that zip behind a password

A password on an archive means the zip's own AES-256 by default: the password lives inside the archive rather than in a gpg layer around it, and 7-Zip or any other archiver opens it by asking. Explorer refuses that one outright, which is the price. The `.gpg` shapes above are still written on request, for anyone who already uses gpg

What cannot travel is a resource the level fetches from a link. It is left pointing where it points and the export report names it. A file lying in the level folder that nothing references is not packed either, and the report counts those

Encrypt the level document. It writes `level.json.gpg` beside the original and leaves the original where it is, so delete it yourself once you have checked the result:
`gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json`

Decrypt it back. The document is written out under its own name again, and the encrypted file stays:
`gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD level.json.gpg > level.json`

Pack the level folder into one archive. The folder is packed from the inside, so the archive holds the level's own files rather than a folder containing them:
`tar -czf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER .`

Make the folder to unpack into. Both unpacking lines below need it to exist already, because tar will not create it - and the same line works in cmd, in PowerShell and in a terminal on Mac or Linux:
`mkdir LEVEL_FOLDER`

Unpack the archive into it:
`tar -xzf LEVEL_FOLDER.tar.gz -C LEVEL_FOLDER`

Pack and encrypt in one pass. Nothing is written between the two steps, so an unprotected archive never touches the disk at all:
`tar -czf - -C LEVEL_FOLDER . | gpg -c --cipher-algo AES256 --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD -o LEVEL_FOLDER.tar.gz.gpg`

Decrypt and unpack that one back into the same folder:
`gpg -d --batch --pinentry-mode loopback --passphrase YOUR_PASSWORD LEVEL_FOLDER.tar.gz.gpg | tar -xz -C LEVEL_FOLDER`

Make a zip instead, in PowerShell, which every Windows machine already has. The star matters: it packs what is inside the folder rather than the folder itself:
`Compress-Archive -Path LEVEL_FOLDER\* -DestinationPath LEVEL_FOLDER.zip`

Unpack that zip. This one creates the folder itself, so no mkdir first:
`Expand-Archive -Path LEVEL_FOLDER.zip -DestinationPath LEVEL_FOLDER`

On Mac or Linux the same two lines are zip and unzip:
`cd LEVEL_FOLDER && zip -r ../LEVEL_FOLDER.zip .`
`unzip LEVEL_FOLDER.zip -d LEVEL_FOLDER`

Make a zip with a password 7-Zip will ask for, which needs 7-Zip installed:
`7z a -tzip -mem=AES256 -pYOUR_PASSWORD LEVEL_FOLDER.zip .\LEVEL_FOLDER\*`

Two things are placeholders. `LEVEL_FOLDER` is the level's own folder name, which is its id - the long string of digits and letters the folder in `levels` is called. `YOUR_PASSWORD` is the password itself, and a password written into a command line stays in the shell history afterwards - drop `--batch --pinentry-mode loopback --passphrase YOUR_PASSWORD` from any of those lines and gpg asks for it on screen instead

> [!tip] Tip
> All of them work in both directions - what the game writes, gpg, tar and zip open, and what gpg, tar and zip make, the game reads. That is the whole reason for using standard tools instead of a format of our own

> [!tip] Tip
> The game reads what a file IS rather than what it is called, so a renamed archive still opens. 7z is the one format it recognises and refuses: it says so by name instead of calling the file broken, and re-packing it as a zip is enough

> [!caution] Caution
> **A FORGOTTEN PASSWORD CANNOT BE RECOVERED**. No key is kept anywhere - not in the game, not in the file, not by the developers. There is no reset, no recovery and no way in. A level whose password is lost is lost with it, so write the password down somewhere before you close the editor

More: [[4_level-folder-and-backups|The level folder and backups]], [[4_not-losing-work|Not losing your work]]
