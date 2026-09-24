---
title: Playing levels
date: 2026-09-24
tags: [player]
---

# Playing levels

How to find a level, add someone else's, start a run and read the result window

## Main menu

| Button | What it does |
|---|---|
| `Levels` | the list of levels, described below |
| `Editor` | the level editor, [[2_editor/1_basics/index]] |
| `Settings` | every setting, [[4_settings]] |
| `Story` | does not work yet |
| `Multiplayer` | does not work yet |

## The level list

`Levels` in the main menu opens the list of levels. Levels come from three places:

- `My Levels` - the `levels` folder, [[1_installation]]
- `Built-in` - the levels that come with the game
- `Workshop` - Steam builds only. It lists the items you are subscribed to

At the top there are the search field, `Sort` and `View` (grid or list).
You can sort by `Best match`, `Name`, `Length`, `Progress` and `Recent`

Copied a level into the folder? Press `Scan again` and the list updates

A lock on a card means the level is protected by a password

A hold or a right click on a card opens a menu: `Open` and `Delete`

## Adding someone else's level

A level is a plain folder of files. You can zip it and send it to a friend

**A folder.** Copy the level folder into `levels` and press `Scan again`.
Copy the level folder itself: the one holding `level.json` (or `level.blob`) and `metadata.json`

**An archive.** Open the editor and create a new level with the `Level Archive` generator.
Then pick the file with `Choose Level Archive...`

| File | Result |
|---|---|
| `.zip`, `.tar.gz` | opens |
| `.zip` with its own password, `.zip.gpg`, `.tar.gz.gpg` | opens after `protected, enter the password and press again` |
| `.7z` | refused for now. Re-pack it as a zip |
| anything else | refused, [[5_troubleshooting]] |

A renamed archive still opens: the game reads the format from the file's bytes.
An archive from an older version of the game is updated on import

By default an imported level gets an id of its own. So it cannot overwrite a level already on your device

More - [[6_sharing-by-hand]]. *Afterbeat* levels - [[3_afterbeat-import]]

## The level screen

The level screen shows the cover, the authors, the description and the music credit. It also has the `Authors` and `Licenses` buttons

The age rating is declared by the level's author. The developers do not check it

Before a run you can pick the conditions:

| Option | Choices |
|---|---|
| `Lifes` | `Zen` (the run never ends), `One life`, `Three lifes`, `Custom` (a slider up to 16) |
| `Speed` | `0.5`, `1.0`, `2.0`, `Custom` (a slider up to 2). The level and its music change together |
| `Checkpoints` | on or off, [[7_damage]] |
| `Bot` | `No Bot`, `Reflex Bot v1`, `Warm Bot v1`, [[9_bots]] |
| `Player Seed` | a number, `Randomize`, `Clear`. `0` - a fresh seed every run, [[8_determinism]] |

`Play` starts the run

The pause window has `Continue`, `Restart`, `Settings`, `Back to Menu` and `Exit Game`

## The result window

The window shows `Passed` or `Failed` and three sections: `Progress`, `Damage` and `Conditions`

- rows: `Completed`, `Checkpoint reached`, `Time`, `Level length`, `Hits taken`, `Lives left`, `Longest clean streak`
- run conditions: `Speed`, `Lives`, `Bot`, `Seed`, `Checkpoints`
- buttons: `Restart`, `Restart from Checkpoint`, `Settings`, `Back to Menu`

By default a lost run does not open this window. The run rewinds to the last checkpoint instead.
To change that - `Settings` → `Interface` → `Open Menu on Lose`

## Records

The level screen has a record block: `Best`, `Attempts` and `Cleared` (or `Never played`)

Each set of conditions has its own record: lives, speed, checkpoints and the bot. The block shows the record for the conditions selected right now.
Attempts and clears count every run

How a record is chosen - [[10_statistics]]

## Card markers

| Marker | What it means |
|---|---|
| `Not subscribed` | a workshop folder is on disk, but you are not subscribed to it. Listed only while `Settings` → `General` → `Show All Found Content` is on |
| `Offline` | the level source did not answer |
| `Newer version`, `From a newer version of the game` | this version of the game cannot open the level, [[5_troubleshooting]] |

## Deleting a level

Hold or right-click a card → `Delete`. The game asks for confirmation first

You can delete the level's statistics (`Also delete statistics`) and backups (`Also delete backups`) along with it

Deleting a protected level needs no password
