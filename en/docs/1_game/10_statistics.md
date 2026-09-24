---
title: Statistics
date: 2026-09-24
tags: [advanced_player]
---

# Statistics

What the game counts about your play and your authoring, how a record is chosen, where the files are and how to delete or freeze them

## Two files, two questions

| File | Answers |
|---|---|
| `stats/statistics.json` | "this person": everything across every level and screen |
| `stats/<LevelId>.json` | "this level": everything you did with one level |

`stats` sits beside `levels` in the game's folder (see [[1_installation]]), never inside a level. A level you send someone must not arrive already won, and your progress must survive a level being deleted and re-imported. The files are JSON, timestamps are UTC, and nothing is uploaded anywhere

## The Profile tab

`Settings`, `Profile` shows the device-wide file:

| Section | Rows |
|---|---|
| `Account` | `Playing since`, `Last played`, `Launches`, `Time in game` |
| `Time` | `Menu`, `Game`, `Editor`, `Loading` |
| `Totals` | `Attempts`, `Clears`, `Deaths`, `Hits`, `Levels played`, `Levels cleared`, `Frames simulated` |
| `Streaks` | `Current clear streak`, `Longest clear streak` |
| `Avatar` | `Dashes`, `Distance travelled` |
| `Authoring` | `Levels created`, `Levels deleted`, `Objects created`, `Operations`, `Generator runs`, `Resources added` |
| `Devices` | `Keyboard and mouse`, `Touchscreen`, `Gamepad`, `Gyroscope` |

Times are real seconds, not level time, so the checkpoint ramp and a run at half speed count as long as they actually took. The device rows measure which device was steering during play, not which was merely connected

## Per level

A level's file keeps: when you first and last played it, real time spent, visits, attempts (every restart is a new one), clears, deaths, hits, dashes, resumes from a checkpoint, abandoned runs, the furthest point reached, the first clear, and where in the level you die (by fraction of its length and by checkpoint)

## Records

A record is filed under the run's conditions: lives, speed (to hundredths, exactly what the screen shows), checkpoints on or off, and the bot. A run beats the record under the same conditions when, in this order:
1. it got further
2. it took fewer hits
3. it ended with more lives left
4. it spent fewer dashes

A record also stores the seed of the run and the level's version at the time. The version is not part of the key, so a record set before the level was reworked stays visible, with the version beside it

**An editor run counts but never records.** It adds to attempts, deaths and hits, and sets no record, no best progress and no first clear, because it played a level that exists only in memory

## Writing, deleting, freezing

The game writes statistics every 30 seconds, and immediately at the end of a run, on a screen change and on quit. A crash costs at most 30 seconds of numbers

- `Settings`, `Other`, `Storage`: `Statistics of levels that no longer exist` and `All statistics, your device profile included`
- Deleting a level offers `Also delete statistics`
- Anonymous mode stops all writing until the game is closed, see [[4_settings]]

> [!warning] Warning
> A level folder copied by hand keeps the level's id, so the original and the copy share one statistics file
