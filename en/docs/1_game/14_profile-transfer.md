---
title: Profile transfer
date: 2026-10-02
tags: [player]
---

# Profile transfer

Your whole profile fits in one zip file: levels, statistics, settings and the library. Export it before reinstalling or moving to another device, then import it there

The buttons are in `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`. It works on Windows, Mac, Linux and Android. It is not available on iOS

## What goes into the file

| Part | In the data folder | Ticked by default |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | yes |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | yes |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | yes |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | yes |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | no |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | no |

The file is an ordinary zip and opens in any archiver. Inside are the same folders as in the data folder ([[1_installation]]), plus `profile.json`, which describes the file

## Export

1. Press `{{ui:settings_profile-transfer_export}}`
2. Tick the parts you need
3. Choose where to save the file

Export works wherever the settings open: in the main menu, in a paused run and in the editor. Statistics are written to disk first, so the file is current

## Import

1. Open the settings from the main menu and press `{{ui:settings_profile-transfer_import}}`
2. Pick the zip file
3. Tick the parts and choose the mode
4. Confirm

Import works only from the main menu. A running level or an open editor holds its files, and they cannot be replaced underneath it

| Mode | What happens |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | each ticked part is emptied and filled from the file |
| `{{ui:settings_profile-transfer_mode-merge}}` | levels are added. A level you both have is replaced whole by the newer copy. Statistics keep the larger value of each counter and the better record. Library files, autosaves and reports are only added, yours stay |

Every import asks once more before writing anything. A replace names the parts it empties, a merge says how many levels it adds, replaces and keeps

**Settings from another kind of device.** A profile from a phone imported on a computer (or the other way round) keeps your own controls and graphics. Everything else comes from the file

The game refuses a file from a newer version of the game - update the game first. It also refuses a file that is not a zip, a zip that is not a profile, a password-protected zip and a damaged file. Nothing is changed in any of these cases

## Backup

Before any import the game saves the parts it is about to replace into one backup. It lies in the `profile-backups` folder inside the data folder. There is only one: the next import overwrites it

- `{{ui:settings_profile-transfer_backup-restore}}` puts the backup back. What it replaces becomes the new backup, so a restore can be undone too
- `{{ui:settings_profile-transfer_backup-save-as}}` saves a copy wherever you choose
- `{{ui:settings_profile-transfer_backup-delete}}` deletes it
- `{{ui:settings_profile-transfer_clear-cache}}` deletes the whole `profile-backups` folder: the backup and whatever an interrupted transfer left behind

`{{ui:settings_profile-transfer_backup-to-folder}}` is ticked by default during an import: the game asks where to keep a copy outside the game right away

> [!caution] Caution
> On Android the backup lies in the game's data folder and is deleted together with the game. Before uninstalling, export the profile or save the backup somewhere else

If the game closes in the middle of an import, the next launch puts the profile back as it was

## Moving between builds on Android

A copy of the game installed from a file (itch.io and the like) cannot be updated from Google Play, and the other way round. The builds are signed differently, so Android refuses the update. To switch:

1. Export the profile and save the file outside the game
2. Uninstall the game
3. Install the other build
4. Import the profile
