---
title: Statistics
date: 2026-09-24
tags: [advanced_player]
---

# Statistics

What the game counts about your play and your authoring, how a record is chosen, where the files are and how to delete or freeze them

## Two files

| File | What it holds |
|---|---|
| `stats/statistics.json` | everything about you: across every level and screen |
| `stats/<LevelId>.json` | everything you did with one level |

The files are JSON, timestamps are UTC. Nothing is uploaded anywhere

The `stats` folder sits beside `levels` in the game's folder, [[1_installation]]. It is never inside a level.
That way a level you send a friend does not arrive already won. And your progress survives a level being deleted and re-imported

## The Profile tab

`Settings` → `Profile` shows the device-wide file:

| Section | Rows |
|---|---|
| `Account` | `Playing since`, `Last played`, `Launches`, `Time in game` |
| `Time` | `Menu`, `Game`, `Editor`, `Loading` |
| `Totals` | `Attempts`, `Clears`, `Deaths`, `Hits`, `Levels played`, `Levels cleared`, `Frames simulated` |
| `Streaks` | `Current clear streak`, `Longest clear streak` |
| `Avatar` | `Dashes`, `Distance travelled` |
| `Authoring` | `Levels created`, `Levels deleted`, `Objects created`, `Operations`, `Generator runs`, `Resources added` |
| `Devices` | `Keyboard and mouse`, `Touchscreen`, `Gamepad`, `Gyroscope` |

Times are real seconds, not level time. The checkpoint ramp and a run at half speed count as long as they actually took

The device rows show which device was steering during play. A device that was merely connected does not count

## Per level

A level's file keeps:

- when you first and last played it
- real time spent in it and the number of visits
- attempts (every restart is a new one), clears, deaths, hits, dashes
- resumes from a checkpoint and abandoned runs
- the furthest point reached and the first clear
- where in the level you die: by fraction of its length and by checkpoint

## Records

A record is filed under the run's conditions: lives, speed, checkpoints on or off, and the bot.
Speed counts to hundredths, exactly what the screen shows

A run beats the record under the same conditions when, in this order:

1. it got further
2. it took fewer hits
3. it ended with more lives left
4. it spent fewer dashes

A record also stores the seed of the run and the level's version at the time.
The version is not part of the conditions. So a record set before the level was reworked stays visible, with the version beside it

**An editor run counts but never records.** It adds to attempts, deaths and hits. It gives no record, no best progress and no first clear, because the level existed only in memory

## Writing, deleting, freezing

The game writes statistics every 30 seconds. And right away at the end of a run, on a screen change and on quit.
A crash costs at most 30 seconds of numbers

- **Delete:** `Settings` → `Other` → `Storage`. It has `Statistics of levels that no longer exist` and `All statistics, your device profile included`
- **Delete with a level:** deleting a level offers `Also delete statistics`
- **Freeze:** anonymous mode stops all writing until the game is closed, [[4_settings]]

> [!warning] Warning
> A level folder copied by hand keeps the level's id. The original and the copy share one statistics file
