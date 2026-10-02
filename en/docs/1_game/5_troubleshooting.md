---
title: Troubleshooting
date: 2026-10-03
tags: [player]
---

# Troubleshooting

A level copied by hand shows up in the list after a new scan. A level from a newer version needs a game update, and a .7z archive needs repacking into zip. A forgotten password cannot be recovered. Discord shows your activity only in a Steam build, with the Discord app running

Didn't find your problem? Where to report it - [[11_help]]

## A level is not in the list

- **Copied by hand.** The level folder must sit directly in `levels`, [[1_installation]]. After copying, press `{{ui:root_level-browser_refresh}}`
- **A Workshop item.** The Steam build shows only your subscriptions. `{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}` adds the folders found on disk. They are marked `{{ui:root_level-entry_not-listed}}`
- **Nothing shows at all.** The levels folder may be unreachable. In that state the storage cleanup in `{{ui:settings_other_title}}` does not run and says `The level scan found nothing, so this cleanup was refused`

## A level does not load

The loading screen shows the stage: `{{ui:root_loading_reading}}`, `{{ui:root_loading_validating}}`, `{{ui:root_loading_resources}}`, `{{ui:root_loading_building}}`

- **A file from a web address.** A level can take a file from a link instead of keeping it in its folder. `{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}` is how many seconds the game waits for such a file
- **A damaged level.** A level in `Json` is text, it can be read by eye. A damaged `Blob` is refused whole. More - [[4_level-folder-and-backups]]
- **An error window.** It has `{{ui:root_error_copy}}`, `{{ui:root_error_save}}` and `{{ui:root_error_open-reports-folder}}`. The report goes to the `reports` folder. Attach it to a bug report in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues), [[11_help]]
- **`Level needs more objects per frame than this device allows`.** This is not a loading error. The level plays, but part of it is not drawn. More - [[1_level-budget]]

## "Update required"

An older version of the game does not open files from a newer one. Update the game

| Message | What to do |
|---|---|
| `This level was made in a newer version of the game...` | update the game |
| `This archive holds a level from a newer version of the game...` | update the game |
| `The clipboard holds editor content copied in a newer version of the game...` | update the game |
| `Your settings or statistics were saved by a newer version of the game...` | `{{ui:root_update-required_download}}`, `{{ui:root_update-required_keep}}` or `{{ui:root_update-required_overwrite}}` |

A card marked `{{ui:root_level-entry_newer-version}}` or `{{ui:root_level-entry_newer-file}}` is the same refusal. It shows before the level is even opened

### Settings or statistics from a newer version

In this case the game runs on defaults. Until it is closed it saves nothing of its own, and the newer files stay untouched. This is anonymous mode, [[4_settings]].
With `--suppress-game-saves` there is no `{{ui:root_update-required_overwrite}}` button

Level statistics from a newer version are not shown. Playing the level overwrites them, unless saves are turned off

### Why the game refuses

Every change to the file format gets a new generation number. A build does not read a file of a newer generation, so that it does not read it wrong

## A protected level

Before opening, the game asks for a `{{ui:level_passphrase_password}}`.
The password is asked once per session and kept only in memory

Only the content is encrypted: objects, keyframes, themes. The title, cover and media stay readable, so the card shows even without the password

Deleting a protected level does not need the password

> [!caution] Caution
> A forgotten password cannot be recovered. The key is stored nowhere - not in the game, not in the file, not with anyone

## An archive is refused

| Message | Cause |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | it is `.7z`. Repack it into `.zip` |
| `{{ui:editor_create-level_archive-wrong-password}}` | the password does not match |
| `{{ui:editor_create-level_archive-damaged}}` | the archive is broken, ask for it again |
| `{{ui:editor_create-level_archive-not-archive}}` | the file is not a level archive at all |

A renamed archive is not a problem: the game recognizes the format by the file's bytes.
Which archives are accepted - [[2_playing-levels]]

## Discord does not show what I am playing

- **Not a Steam build.** Only the Steam builds show your activity in Discord
- **Discord is closed.** The Discord desktop app must be running on the same computer. Started it after the game? The status appears on the next screen change
- **Activity is hidden.** In Discord: `User Settings` -> `Activity Privacy` -> share your detected activities
- **A level of your own shows no name.** By design: only a Workshop level or one that ships with the game is named, and the editor never names its level. Why - [[game-privacy-policy#Discord Rich Presence]]
