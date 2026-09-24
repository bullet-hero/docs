---
title: Installation
date: 2026-09-24
tags: [player]
---

# Installation

Where to get the game, where it keeps your levels and what happens when you update

## Download

Every build and store - [[download]]

The game runs on PCs and phones. The levels, the editor and the controls are the same everywhere

A store build is installed and updated by the store itself.
The Android `.apk` is installed by hand

## Where your files are

There are no accounts. Everything the game remembers stays on your device

The game has its own data folder. It is not the folder the game is installed to

| System | Folder |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

The fastest way to open it is from the game: `Settings` → `General` → `Open Game Folder`

What is inside:

| Folder | What it holds |
|---|---|
| `levels` | your levels, each in its own folder |
| `backups` | the editor's autosaves |
| `stats` | statistics |
| `settings.json` | settings |
| `reports` | error reports |

## Updating

A new version of the game reads all old levels and settings. There is nothing to move

An old version does not open levels from a newer one. If the game asks you to update, update

> [!caution] Caution
> On Android, uninstalling the game also deletes all your levels. Save the ones you need before uninstalling

## Android and folder access

When the game needs a file outside its own folder, Android itself asks which folder to open.
The game sees only that folder and nothing else

You can take the access back: `Settings` → `Other` → `Folder access`
