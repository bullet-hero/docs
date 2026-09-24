---
title: Troubleshooting
date: 2026-09-24
tags: [player]
---

# Troubleshooting

What to do when a level is missing, does not load, asks for a newer game or a password, or comes in an archive the game refuses

Your problem is not here? Where to report it - [[11_help]]

## A level is not in the list

- **Copied in by hand.** The level folder has to sit directly inside `levels`, [[1_installation]]. Press `Scan again` after copying
- **A workshop item.** A Steam build lists only your subscriptions. `Settings` → `General` → `Show All Found Content` adds folders found on disk. They are marked `Not subscribed`
- **Nothing is listed at all.** The levels folder may be unreachable. Storage cleanup in `Other` does not run in that state and says `The level scan found nothing, so this cleanup was refused`

## A level does not load

The loading screen shows its stage: `Reading level`, `Checking level`, `Loading resources`, `Building level`

- **A file at a web address.** A level can take a file from a link instead of keeping it in its folder. `General` → `Resource Web Timeout` is how many seconds the game waits for such a file
- **A damaged level.** A `Json` level is text and can be read by eye. A damaged `Blob` is refused whole. More - [[4_level-folder-and-backups]]
- **An error window.** It has `Copy`, `Save Report` and `Open Reports Folder`. The report goes to the `reports` folder. Attach it to a bug report in [bullet-hero-releases](https://github.com/vertoker/bullet-hero-releases/issues), [[11_help]]
- **`Level needs more objects per frame than this device allows`.** This is not a failure to load. The level plays, but part of it is not drawn. More - [[1_level-budget]]

## "Update required"

An old version of the game does not open files from a newer one. Update the game

| Message | What to do |
|---|---|
| `This level was made in a newer version of the game...` | update the game |
| `This archive holds a level from a newer version of the game...` | update the game |
| `The clipboard holds editor content copied in a newer version...` | update the game |
| `Your settings or statistics were saved by a newer version of the game...` | `Download`, `Keep saves suppressed` or `Overwrite data` |

A card marked `Newer version` or `From a newer version of the game` is the same refusal. It shows before you open the level

### Settings or statistics from a newer version

In this case the game runs on defaults. Until it is closed it saves nothing of its own, and the newer files stay untouched. This is anonymous mode, [[4_settings]].
With `--suppress-game-saves` there is no `Overwrite data` button

A level's statistics from a newer version are not shown. Playing the level overwrites them unless saves are suppressed

### Why the game refuses

Every change to the file format gets a new generation number. A build does not read a file from a newer generation, so that it never reads it wrongly

## A protected level

Before opening, the game asks for a `Password`.
The password is asked once per session and kept in memory only

Only the content is encrypted: objects, keyframes, themes. The name, the cover and the media stay readable, so the card shows without the password

Deleting a protected level needs no password

> [!caution] Caution
> A forgotten password cannot be recovered. No key is kept anywhere - not in the game, not in the file, not by the developers

## An archive is refused

| Message | Cause |
|---|---|
| `this build cannot read that archive format yet` | a `.7z`. Re-pack it as a `.zip` |
| `wrong password` | the password does not match |
| `the file is damaged` | the archive is broken, ask for it again |
| `not a level archive` | the file is not a level archive at all |

A renamed archive is not a problem: the game reads the format from the file's bytes.
Which archives are accepted - [[2_playing-levels]]
