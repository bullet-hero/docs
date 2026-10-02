---
title: Statistics
date: 2026-10-02
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

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}` shows the device's shared file:

| Section | Rows |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`, `{{ui:settings_profile_last-played}}`, `{{ui:settings_profile_launches}}`, `{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`, `{{ui:settings_profile_game-time}}`, `{{ui:settings_profile_editor-time}}`, `{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`, `{{ui:settings_profile_clears}}`, `{{ui:settings_profile_deaths}}`, `{{ui:settings_profile_hits}}`, `{{ui:settings_profile_levels-played}}`, `{{ui:settings_profile_levels-cleared}}`, `{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`, `{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`, `{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`, `{{ui:settings_profile_tutorial-first}}`, `{{ui:settings_profile_tutorial-last}}` - a completion counts only when every step of the [[13_sandbox|sandbox tutorial]] is done |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`, `{{ui:settings_profile_levels-deleted}}`, `{{ui:settings_profile_objects}}`, `{{ui:settings_profile_operations}}`, `{{ui:settings_profile_generators}}`, `{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`, `{{ui:settings_profile_device-touch}}`, `{{ui:settings_profile_device-gamepad}}`, `{{ui:settings_profile_device-gyro}}` |

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

- **Delete:** `{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`. There you find `{{ui:settings_other_cache-orphan-statistics}}` and `{{ui:settings_other_cache-all-statistics}}`
- **Delete with the level:** deleting a level offers `{{ui:root_level-delete_statistics}}`
- **Freeze:** anonymous mode stops all writing until the game is closed, [[4_settings]]
- **Carry to another device:** export the profile and import it there. A merge keeps the larger value of each counter, [[14_profile-transfer]]

> [!warning] Warning
> A level folder copied by hand keeps the level's id. The original and the copy share one statistics file
