---
title: Troubleshooting
date: 2026-09-24
tags: [player]
---

# Troubleshooting

What to do when a level is missing, does not load, asks for a newer game or a password, or comes in an archive the game refuses

## A level is not in the browser

- **Copied in by hand.** The folder has to be the level folder itself, directly inside `levels` (see [[1_installation]]). Press `Scan again` after copying
- **A workshop item.** A Steam build lists only what you are subscribed to. `Settings`, `General`, `Show All Found Content` also lists folders found on disk, marked `Not subscribed`
- **Nothing is listed at all.** The levels folder may be unreachable. Storage cleanup in `Other` refuses to run in that state and says `The level scan found nothing, so this cleanup was refused`

## A level does not load

- **The loading screen names its stage**: `Reading level`, `Checking level`, `Loading resources`, `Building level`. A level can point a file at a web address instead of carrying it, and `General`, `Resource Web Timeout` is how many seconds the game waits for such a file before giving up
- **A damaged document.** A level saved as `Json` is text and can be read by eye. A `Blob` is binary and a damaged one is refused whole. See [[4_level-folder-and-backups]]
- **An error window** offers `Copy`, `Save Report` and `Open Reports Folder`. Reports go to the `reports` folder. Attach one when you report the problem
- **`Level needs more objects per frame than this device allows`** is not a failure to load: the level plays and part of it is not drawn. See [[1_level-budget]]

## "Update required"

Every change to the file format gets a new generation number. A build refuses a file from a newer generation rather than read it wrongly, which protects the file

| Message | What to do |
|---|---|
| `This level was made in a newer version of the game...` | update the game |
| `This archive holds a level from a newer version of the game...` | update the game |
| `The clipboard holds editor content copied in a newer version...` | update the game |
| `Your settings or statistics were saved by a newer version of the game...` | `Download`, `Keep saves suppressed` or `Overwrite data` |

In the last case the game runs on defaults and saves nothing of its own until it is closed, so the newer files stay untouched (see anonymous mode in [[4_settings]]). With `--suppress-game-saves` there is no `Overwrite data` button

A card marked `Newer version` or `From a newer version of the game` is the same refusal, shown before you open the level. Statistics of a level saved by a newer version are not shown, and playing the level overwrites them unless saves are suppressed

## A protected level

The browser asks for a `Password` before opening. Only the content (objects, keyframes, themes) is encrypted: the name, the cover and the media stay readable, so the card is drawn without the password. It is asked once per session and kept in memory only. Deleting a protected level does not need it

> [!caution] Caution
> A forgotten password cannot be recovered. No key is kept anywhere - not in the game, not in the file, not by the developers

## An archive is refused

| Message | Cause |
|---|---|
| `this build cannot read that archive format yet` | a `.7z`. Re-pack it as a `.zip` |
| `wrong password` | the password does not match |
| `the file is damaged` | the archive is broken, ask for it again |
| `not a level archive` | the file is not a level archive at all |

A renamed archive is not a problem: the game reads what a file is from its bytes. Accepted formats are in [[2_playing-levels]]
