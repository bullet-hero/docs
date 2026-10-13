---
title: Installation
date: 2026-10-02
tags: [player]
---

# Installation

The game keeps levels, settings and statistics in one data folder. Updating is safe: a new version reads all old data. On Android, uninstalling the game erases the levels too

Download here - [[download]]

## Where your files are

| System | Folder |
|---|---|
| Windows | `C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

The fastest way to open it is from the game: `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general-open_folder}}`

What is inside:

| Folder | What it holds |
|---|---|
| `levels` | your levels, each in its own folder |
| `backups` | the editor's autosaves |
| `stats` | statistics |
| `settings.json` | settings |
| `reports` | error reports |

## Uninstalling

On Windows, Linux and Mac the free version carries an uninstaller next to the game: `unins000.exe` on Windows, `unins000` on Linux, and `unins000` beside `Bullet Hero.app` on a Mac. Run it and it removes the game by itself, without a single question. Your levels, settings and statistics stay in the data folder

It removes only the game's own files. Anything you put into the game's folder yourself stays, and the folder goes only once it is empty. If the game is running, the uninstaller closes it first, as its close button would, and the AI's MCP server with it. A level with unsaved changes loses them, so save it before uninstalling

Installed with the Windows installer, the game is removed like any other program, in Windows Settings under Apps

A store version is removed by its store

## Updating

A new version of the game reads all old data without problems, whatever the update and whatever changed

An old version will not open levels from a newer one. If the game asks you to update, update

In the Google Play version, the main menu offers a new update and it downloads in the background. When it is ready, the main menu shows `{{ui:menu_update-ready_text}}` - press `{{ui:menu_update-ready_install-btn}}`. After a cleared level it may also ask you to rate the game

> [!caution] Caution
> On Android, uninstalling the game also deletes all your levels. Export the profile before uninstalling - [[14_profile-transfer]]
