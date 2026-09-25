---
title: Export and protection
date: 2026-09-24
tags: [level_author]
---

# Export and protection

Exporting a level to a folder or an archive and protecting it with a password

## Export level

Writes the level outside the game: as a folder or as one archive

An archive carries the level, its metadata and every file it uses.
A song that lives outside the level folder is copied in too. Its reference is re-pointed at the copy in the archive

| Option | What you get | Opened with |
|---|---|---|
| `Folder` | the same folder the level has on disk. Zip it and send it | nothing needed |
| `Folder (protected level)` | the same folder, with the level document encrypted. The metadata, the cover and the media stay readable, so a level browser still shows its card | gpg for the level document |
| `Archive .zip` | one file | a double click in Windows Explorer, nothing to install |
| `Archive .tar.gz` | one file | any archiver |
| `Archive .zip + password` | a zip with its own AES-256 encryption. The usual meaning of a password on an archive | 7-Zip or any other archiver, which asks for the password |
| `Archive .zip + password (gpg)`, `Archive .tar.gz + password (gpg)` | the same archive wrapped in `.gpg` | gpg |

Windows Explorer opens none of the password options. That is what a password costs

> [!tip] Tip
> Anything that could not travel (a resource behind a URL, a file nothing references) is listed in the report after the export

> [!warning] Warning
> A password protects the content in transit and from casual copying. It is not DRM: anyone with the file and the password can always open it

## Protect level

Encrypts the level's document on disk. Opening the level asks for the password

What is protected is the **content**: objects, keyframes, themes.
The metadata, the cover and the media stay readable. So the level browser still shows the level's card without the password

The password is asked once per session and kept in memory only.
It is never written anywhere, so autosave keeps working

To remove the protection, leave the field empty and press `Apply`

> [!caution] Caution
> A forgotten password cannot be recovered. No key is kept anywhere, and there is no way into the file without it
