---
title: Statistics
date: 2026-10-01
tags: [advanced_player]
---

# Statistics

The game counts attempts, deaths, hits and time for each level and for the whole device. Everything is stored locally in the stats folder. A record is kept separately for each set of run conditions

## Two files

| File | What it holds |
|---|---|
| `stats/statistics.json` | everything about you: across all levels and screens |
| `stats/<LevelId>.json` | everything you did with one level |

The files are JSON, times are in UTC. Nothing is sent anywhere

The `stats` folder sits next to `levels` in the game folder, [[1_installation]]. It is never inside a level.
So a level sent to a friend does not arrive already cleared. And your progress survives deleting the level and importing it again

## The "Profile" tab

`Settings` → `Profile` shows the device's shared file:

| Section | Rows |
|---|---|
| `Account` | `Playing since`, `Last played`, `Launches`, `Time in game` |
| `Time` | `Menu`, `Game`, `Editor`, `Loading` |
| `Totals` | `Attempts`, `Clears`, `Deaths`, `Hits`, `Levels played`, `Levels cleared`, `Frames simulated` |
| `Streaks` | `Current clear streak`, `Longest clear streak` |
| `Avatar` | `Dashes`, `Distance travelled` |
| `Tutorial` | `Times completed`, `First completed`, `Last completed` - a completion counts only when every step of the [[13_sandbox|sandbox tutorial]] is done |
| `Authoring` | `Levels created`, `Levels deleted`, `Objects created`, `Operations`, `Generator runs`, `Resources added` |
| `Devices` | `Keyboard and mouse`, `Touchscreen`, `Gamepad`, `Gyroscope` |

Time is counted in real seconds, not in level time. Slow motion at a checkpoint and a run at half speed count for as long as they actually lasted

The device rows show which device steered the avatar during play. A device that is merely connected does not count

## Per level

A level's file holds:

- when you first and last played it
- the real time spent in the level and the number of sessions
- attempts (every restart is a new one), clears, deaths, hits, dashes
- returns to a checkpoint and abandoned runs
- the furthest point reached and the first clear
- where in the level you die: by share of the length and by checkpoint

## Records

A record is kept per run conditions: lives, speed, checkpoints on or off, collision on or off, and the bot.
Speed counts to the hundredths, exactly as on screen

Zen (0 lives) still counts hits: every collision goes into its numbers, only lives and the end of the run are spared

A run beats the record with the same conditions if, in this order:

1. it got further
2. it took fewer hits
3. it ended with more lives
4. it used fewer dashes

A record also stores the run's seed and the level's version at that moment.
The version is not part of the conditions. So a record set before the level was reworked stays visible, with the version shown beside it

**A run from the editor counts, but sets no records.** It adds to attempts, deaths and hits. It gives no record, best progress or first clear, because the level existed only in memory

## Writing, deleting, freezing

The game writes statistics every 30 seconds. And immediately at the end of a run, on a screen change and on exit.
A crash costs at most 30 seconds of data

- **Delete:** `Settings` → `Other` → `Storage`. There you find `Statistics of levels that no longer exist` and `All statistics, your device profile included`
- **Delete with the level:** deleting a level offers `Also delete statistics`
- **Freeze:** anonymous mode stops all writing until the game is closed, [[4_settings]]

> [!warning] Warning
> A level folder copied by hand keeps the level's id. The original and the copy share one statistics file
