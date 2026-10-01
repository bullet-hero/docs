---
title: Troubleshooting
date: 2026-10-01
tags: [player]
---

# Troubleshooting

A level copied by hand shows up in the list after a new scan. A level from a newer version needs a game update, and a .7z archive needs repacking into zip. A forgotten password cannot be recovered

Didn't find your problem? Where to report it - [[11_help]]

## A level is not in the list

- **Copied by hand.** The level folder must sit directly in `levels`, [[1_installation]]. After copying, press `Scan again`
- **A Workshop item.** The Steam build shows only your subscriptions. `Settings` → `General` → `Show All Found Content` adds the folders found on disk. They are marked `Not subscribed`
- **Nothing shows at all.** The levels folder may be unreachable. In that state the storage cleanup in `Other` does not run and says `The level scan found nothing, so this cleanup was refused`

## A level does not load

The loading screen shows the stage: `Reading level`, `Checking level`, `Loading resources`, `Building level`

- **A file from a web address.** A level can take a file from a link instead of keeping it in its folder. `General` → `Resource Web Timeout` is how many seconds the game waits for such a file
- **A damaged level.** A level in `Json` is text, it can be read by eye. A damaged `Blob` is refused whole. More - [[4_level-folder-and-backups]]
- **An error window.** It has `Copy`, `Save Report` and `Open Reports Folder`. The report goes to the `reports` folder. Attach it to a bug report in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues), [[11_help]]
- **`Level needs more objects per frame than this device allows`.** This is not a loading error. The level plays, but part of it is not drawn. More - [[1_level-budget]]

## "Update required"

An older version of the game does not open files from a newer one. Update the game

| Message | What to do |
|---|---|
| `This level was made in a newer version of the game...` | update the game |
| `This archive holds a level from a newer version of the game...` | update the game |
| `The clipboard holds editor content copied in a newer version of the game...` | update the game |
| `Your settings or statistics were saved by a newer version of the game...` | `Download`, `Keep saves suppressed` or `Overwrite data` |

A card marked `Newer version` or `From a newer version of the game` is the same refusal. It shows before the level is even opened

### Settings or statistics from a newer version

In this case the game runs on defaults. Until it is closed it saves nothing of its own, and the newer files stay untouched. This is anonymous mode, [[4_settings]].
With `--suppress-game-saves` there is no `Overwrite data` button

Level statistics from a newer version are not shown. Playing the level overwrites them, unless saves are turned off

### Why the game refuses

Every change to the file format gets a new generation number. A build does not read a file of a newer generation, so that it does not read it wrong

## A protected level

Before opening, the game asks for a `Password`.
The password is asked once per session and kept only in memory

Only the content is encrypted: objects, keyframes, themes. The title, cover and media stay readable, so the card shows even without the password

Deleting a protected level does not need the password

> [!caution] Caution
> A forgotten password cannot be recovered. The key is stored nowhere - not in the game, not in the file, not with anyone

## An archive is refused

| Message | Cause |
|---|---|
| `this build cannot read that archive format yet` | it is `.7z`. Repack it into `.zip` |
| `wrong password` | the password does not match |
| `the file is damaged` | the archive is broken, ask for it again |
| `not a level archive` | the file is not a level archive at all |

A renamed archive is not a problem: the game recognizes the format by the file's bytes.
Which archives are accepted - [[2_playing-levels]]
