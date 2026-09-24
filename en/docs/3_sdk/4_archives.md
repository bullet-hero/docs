---
title: Archives and protection
date: 2026-09-24
tags: [developer, level_author]
---

# Archives and protection

How the SDK packs a level into one file or puts it behind a password, and how it recognizes what it was handed

## Export modes

A level leaves the device in one of the `LevelExportMode` shapes:

| Value | Mode | What is written | Protection |
|---|---|---|---|
| 0 | `Folder` | a plain folder, the same shape as on disk | none |
| 1 | `FolderProtectedLevel` | a folder where only `level.json.gpg` is encrypted | OpenPGP |
| 2 | `TarGz` | `<name>.tar.gz` | none |
| 3 | `TarGzProtected` | `<name>.tar.gz.gpg` | OpenPGP |
| 4 | `Zip` | `<name>.zip` | none |
| 5 | `ZipProtected` | `<name>.zip.gpg` | OpenPGP |
| 6 | `ZipEncrypted` | `<name>.zip` with AES-256 entries | the zip's own |

The number is the identity of a mode and never changes. The order in the editor's dropdown is set separately (`DisplayOrder`)

**Every format is an open standard.** `tar -xzf`, `gpg -d` and any archiver open them without the game:

```bash
gpg -d level.tar.gz.gpg > level.tar.gz
tar -xzf level.tar.gz
```

## Two protection schemes

**`ZipEncrypted` is the default way to put a level behind a password.** The person receiving it has an archiver and most likely does not have gpg

**OpenPGP covers a document, a folder and an archive with one scheme.** Only it can protect a folder

In `FolderProtectedLevel` the metadata, the cover and the media stay readable. So a level browser still shows the card

The inner extension stays in the name: `level.json.gpg`. That is exactly how `gpg -c level.json` names the file, so the format is known without a guess

## What goes inside

`LevelArchiveBuilder` computes the contents from the model, not from a folder listing. A file the level does not reference stays out. The report says how many were left behind

The level's references are handled like this:
- a resource with `AbsolutePath` is copied into the archive. Its reference is rewritten to `LevelPath`, but in the exported copy only
- a `DirectUrl` stays as it is and is reported: a URL cannot travel inside a file
- a missing file is reported with the code `archive.resource_missing`

## Recognition by bytes

Anybody can write a file name. So `ArchiveFormatSniffer` decides by the first 8 bytes:

| First bytes | Format |
|---|---|
| `1F 8B` | `TarGz` |
| `50 4B 03 04`, `50 4B 05 06`, `50 4B 07 08`, `50 4B 30 30` | `Zip` |
| `37 7A BC AF 27 1C` | `SevenZip` |
| an OpenPGP packet tag, checked last | `OpenPgp`: decrypted, then sniffed again |

> [!warning] Warning
> `.7z` is not read and not written. It is recognized only so the refusal can name it (`Unsupported`). Then the person re-packs the level as zip instead of deciding the file is broken

## Reading

`LevelArchiveReader.ReadAsync` takes a folder or a seekable `Stream`. It returns a `LevelArchiveContent` whose `LevelArchiveOpenResult` is one of:

| Result | Meaning |
|---|---|
| `Ok` | read |
| `PassphraseRequired` | there is no passphrase, ask for it |
| `WrongPassphrase` | the person already entered a passphrase, and it is wrong |
| `Damaged` | the file is damaged |
| `NotAnArchive` | this is not an archive |
| `Unsupported` | the format is recognized but not supported |

`PeekMetaAsync` reads only the metadata, for a card or a catalogue

A server reads whatever somebody chose to upload. So the reader works under `ArchiveLimits`. The defaults are:
- 4096 entries
- 512 MiB per entry
- 1 GiB in total

Nothing is unpacked outside the store it was given

The editor side of export - [[13_export-and-protection]]
