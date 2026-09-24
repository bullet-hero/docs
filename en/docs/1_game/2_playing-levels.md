---
title: Playing levels
date: 2026-09-24
tags: [player]
---

# Playing levels

The level browser, getting someone else's level into the game, the options on the level screen and what the result window shows

## The level browser

`Levels` in the main menu lists levels from up to three sources: `My Levels` (the `levels` folder, see [[1_installation]]), `Built-in`, and `Workshop` in Steam builds, which lists the items you are subscribed to

- The search field, `Sort` (`Best match`, `Name`, `Length`, `Progress`, `Recent`) and `View` (grid or list)
- `Scan again` re-reads the sources after you copy a folder in
- A lock on a card means the level is protected by a password
- `Not subscribed` marks a workshop folder found on disk but not in your subscriptions, listed only while `Settings`, `General`, `Show All Found Content` is on. `Offline` means the source could not be asked
- `Newer version` and `From a newer version of the game` mean this build cannot open it, see [[5_troubleshooting]]

A hold or a right click on a card offers `Open` and `Delete`. Deleting asks first, offers `Also delete statistics` and `Also delete backups`, and needs no password

## Getting someone else's level

**A folder.** Copy the level folder itself, the one holding `level.json` (or `level.blob`) and `metadata.json`, into `levels` and press `Scan again`

**An archive.** Open the editor, create a new level with the `Level Archive` generator and pick the file with `Choose Level Archive...`

| File | Result |
|---|---|
| `.zip`, `.tar.gz` | opens |
| `.zip` with its own password, `.zip.gpg`, `.tar.gz.gpg` | opens after `protected, enter the password and press again` |
| `.7z` | refused for now. Re-pack it as a zip |
| anything else | refused, see [[5_troubleshooting]] |

The game reads what a file is from its bytes, so a renamed archive still opens. An archive from an older build is migrated on the way in. By default the imported level gets an id of its own, so it cannot overwrite a level already on your device

More: [[6_sharing-by-hand]], and for *Afterbeat* levels [[3_afterbeat-import]]

## The level screen

A level's screen shows the cover, the authors, the age rating the author declared (the developers do not check it), the music credit, the description, `Authors` and `Licenses`, and the launch options:

| Option | Choices |
|---|---|
| `Lifes` | `Zen` (the run never ends), `One life`, `Three lifes`, `Custom` (a slider up to 16) |
| `Speed` | `0.5`, `1.0`, `2.0`, `Custom` (a slider up to 2). The level and its music change together |
| `Checkpoints` | on or off, see [[7_damage]] |
| `Bot` | `No Bot`, `Reflex Bot v1`, `Warm Bot v1`, see [[9_bots]] |
| `Player Seed` | a number, `Randomize`, `Clear`. `0` means a fresh seed every run, see [[8_determinism]] |

`Play` starts the run. The pause window offers `Continue`, `Restart`, `Settings`, `Back to Menu` and `Exit Game`

## The result window

It shows `Passed` or `Failed` and three sections, `Progress`, `Damage` and `Conditions`, with the rows `Completed`, `Checkpoint reached`, `Time`, `Level length`, `Hits taken`, `Lives left`, `Longest clean streak` and the launch conditions (`Speed`, `Lives`, `Bot`, `Seed`, `Checkpoints`). Buttons: `Restart`, `Restart from Checkpoint`, `Settings`, `Back to Menu`

By default a lost run does not open it: it rewinds to the last checkpoint. `Settings`, `Interface`, `Open Menu on Lose` changes that

## Records

The record block on the level screen shows `Best`, `Attempts` and `Cleared`, or `Never played`, for the lives, speed, checkpoints and bot selected right now: a run under other conditions is a different achievement. Attempts and clears count every run. How a record is chosen is on the [[10_statistics]] page
