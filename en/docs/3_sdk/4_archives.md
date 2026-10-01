---
title: Archives and protection
date: 2026-10-01
tags: [developer, level_author]
---

# Archives and protection

A level is exported as a folder, tar.gz or zip, optionally under a password: zip with AES-256 or OpenPGP. The SDK detects the format of a received file by its first bytes, not by its name

## Export modes

A level leaves the device in one of the `LevelExportMode` forms:

| Value | Mode | What is written | Protection |
|---|---|---|---|
| 0 | `Folder` | a plain folder, the same shape as on disk | none |
| 1 | `FolderProtectedLevel` | a folder where only `level.json.gpg` is encrypted | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | none |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | none |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | `<name>.zip` with AES-256 entries | zip's own |

The number is the identity of the mode, it never changes. The order in the editor's dropdown is set separately (`DisplayOrder`)

**Every format is an open standard.** `tar -xzf`, `gpg -d` and any archiver open them without the game:

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## Two protection schemes

**`ZipEncrypted` is the default way to lock a level with a password.** The recipient has an archiver, but most likely not gpg

**OpenPGP locks a document, a folder and an archive with one scheme.** Only it can protect a folder

In `FolderProtectedLevel` the metadata, the cover and the media stay readable. So the level browser still shows the card

The inner extension stays in the name: `level.json.gpg`. That is exactly what `gpg -c level.json` names the file, so the format is known without guessing

## What goes inside

`LevelArchiveBuilder` works out the contents from the model, not from the list of files in the folder. A file the level does not reference stays outside. The report says how many such files were left

The level's references are handled like this:
- a resource with `AbsolutePath` is copied into the archive. Its reference is rewritten to `LevelPath`, but only in the exported copy
- `DirectUrl` stays as is and goes into the report: a URL cannot travel inside a file
- a missing file goes into the report with the code `archive.resource_missing`

## Detection by bytes

Anyone can write a file name. So `ArchiveFormatSniffer` decides by the first 8 bytes:

| First bytes | Format |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| an OpenPGP packet tag, checked last | `OpenPgp`: decrypted and detected again |

> [!warning] Warning
> `.7z` is neither read nor written. It is detected only so that the refusal names it (`Unsupported`). Then a person repacks the level as zip instead of deciding the file is broken

## Reading

`LevelArchiveReader.ReadAsync` takes a folder or a seekable `Stream`. It returns `LevelArchiveContent`, where `LevelArchiveOpenResult` is one of these values:

| Result | Meaning |
|---|---|
| `Ok` | read |
| `PassphraseRequired` | there is no password, it has to be asked for |
| `WrongPassphrase` | the person has already entered a password, and it is wrong |
| `Damaged` | the file is damaged |
| `NotAnArchive` | this is not an archive |
| `Unsupported` | the format is recognized but not supported |

`PeekMetaAsync` reads only the metadata, for a card or a catalog

A server reads whatever someone chose to upload. So the reader works within `ArchiveLimits`. By default these are:
- 4096 entries
- 512 MiB per entry
- 1 GiB in total

Nothing is unpacked outside the storage it was given

Export from the editor's side - [[13_export-and-protection]]
