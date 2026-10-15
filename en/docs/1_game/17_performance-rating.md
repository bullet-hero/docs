---
title: Performance rating
date: 2026-10-15
tags: [player, level_author]
---

# Performance rating

Before you play, the game shows how heavy a level is to run on your device. Green means it runs smoothly, yellow means it is tight, red means it is too heavy and the frame rate will drop

The score is a number where `{{v:performance.score-limit}}` is exactly the time one frame may take at your target frame rate. The band comes from the score:

| Band | Score |
|---|---|
| `{{ui:level_performance_holds}}` | below `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | from `{{v:performance.score-warning}}` to `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | above `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | the level or the device has not been measured |

The score is a forecast for the heaviest moment of the level, not for its average. A level that is light for three minutes and freezes for one second gets the score of that second

## Where you see it

- the level browser: a coloured dot on every level card, and the `{{ui:root_level-filters_performance}}` group in the filters
- the level page in the menu: the band and the score
- the level editor, in the level's metadata: the score on your device and on the reference devices, plus the heaviest moments of the level as timestamps

## Two halves of the score

**The level's half** is measured when the level is saved in the editor and stored in its metadata. It describes what the level asks for: how many objects are alive, how much of the screen they cover, how many effects and post-processing passes run. A level saved before this feature has no such record and shows as `{{ui:level_performance_unknown}}` until it is saved again. The editor measures it when you open the level and keeps the result until you close the game, without writing it into the file

**The device's half** says how fast your device does each of those things. Until you measure your device, the game uses a reference device of your platform. Your settings count too: render scale, anti-aliasing, effects and post-processing all change the score without a new measurement

## Measuring your device

1. Open `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}` from the main menu
2. Press `{{ui:settings_graphics-performance_measure}}`
3. Wait a few minutes. The settings screen hides and the game plays test levels. Do not switch to another app

When it finishes, the section says what limits your device (the processor or the graphics chip) and which `{{ui:settings_quick-setup_performance}}` preset it suggests

If the measurement was unstable (the device was too hot, another app was busy), the game ignores it and keeps the reference device. Close other apps and measure again

## Moving to another device

The measurement belongs to the device it was taken on. A profile transfer ([[14_profile-transfer]]) and cloud saves do not carry it, so a new device starts from its reference device until you measure it again
