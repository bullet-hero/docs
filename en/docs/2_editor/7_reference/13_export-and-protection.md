---
title: Export and protection
date: 2026-09-24
tags: [level_author]
---

# Export and protection

Exporting a level to a folder or an archive and protecting it with a password

## Export level

Writes this level somewhere outside the game - as a folder, or as one archive file

An archive carries the level, its metadata and every file it uses, including a song that lives outside the level folder: that one is copied in and re-pointed at the archive

**Folder** - the same shape a level has on disk. Zip it, send it, unzip it
**Archive .zip** - one file, opened by Windows Explorer on a double click with nothing installed
**Archive .tar.gz** - one file, opened by any archiver
**+ password** - the zip's own AES-256, which 7-Zip or any other archiver opens by asking for the password. This is what a password on an archive means by default
**+ password (gpg)** - the same archive wrapped in `.gpg` instead, opened by gpg. Explorer opens neither of the two, which is what a password costs

> [!tip] Tip
> Anything that could not travel - a resource behind a URL, a file nothing references - is listed in the report afterwards

> [!warning] Warning
> A password protects the content in transit and from casual copying. It is not DRM: anyone holding the file and the password can always open it

## Protect level

Keeps this level's own document encrypted on disk, so opening it asks for a password

What is protected is the **content** - objects, keyframes, themes. The metadata, the cover and the media stay readable, so the level browser still draws the card without the password

The password is asked once per session and kept in memory only - never written anywhere, so autosave keeps working

Leave the field empty and press Apply to remove the protection

> [!caution] Caution
> Nothing here can recover a forgotten password. There is no key kept anywhere and no way back into the file without it
