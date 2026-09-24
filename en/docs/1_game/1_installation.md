---
title: Installation
date: 2026-09-24
tags: [player]
---

# Installation

Where to get the game, where it keeps your levels, settings and statistics on each system, and what updating does to them

## Download

Builds are on the [[download]] page. A store build (Steam, Google Play and the others listed in [[1_game/index]]) is installed and updated by the store. The free Android build is an APK you install by hand

## Where your files live

The game keeps everything in one folder of its own, separate from the folder it is installed in:

| System | Folder |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Linux | `~/.config/unity3d/vertoker/Bullet Hero` (Unity's standard location, not yet checked on a build) |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` on most devices |
| macOS, iOS | not documented yet |

On a desktop, `Settings`, `General`, `Open Game Folder` opens it. Inside:

| Entry | What it holds |
|---|---|
| `levels` | your levels, one folder each |
| `backups` | the editor's autosaves, one folder per level |
| `stats` | statistics, see [[10_statistics]] |
| `settings.json` | every setting |
| `themes`, `effects`, `shapes`, `prefabs` | the editor's device-wide libraries |
| `reports` | error reports |

`backups` and `stats` sit beside `levels`, not inside a level. A level folder is what gets zipped and sent, and your progress and history must not travel with it

## Android and folder access

On Android a file picker hands the game a document rather than a path, so every file or folder outside the game's own storage goes through the system picker: importing an archive, exporting a level. Before the first picker the game shows `Folder access` and explains that Bullet Hero sees only the folder you pick and nothing else on the device

The game declares no storage permission, because the picker itself is the consent. `Settings`, `Other`, `Folder access` lists the folders you granted and `Revoke` takes one back. Revoking deletes nothing inside the folder

The Afterbeat folder import needs real paths and is not available on Android yet

## Updating

- A newer build reads files written by an older one. Every change to the file format comes with a migration, so levels, settings and statistics are converted as they are read
- An older build refuses files written by a newer one instead of reading them wrongly, see [[5_troubleshooting]]
- The data folder is not the install folder, so installing a new build over the old one leaves your levels where they were

> [!caution] Caution
> On Android, uninstalling the game deletes its storage, levels included. Export the levels you want to keep before you uninstall

The game sends nothing anywhere. The one network request it can make is a level loading a file its author put behind a web address
