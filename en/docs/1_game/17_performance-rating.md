---
title: Performance rating
date: 2026-10-17
tags: [player, level_author]
---

# Performance rating

Before you play, the game shows how heavy a level is to run on your device, as a gauge of five bars: the more bars are lit, the lighter the level. Green bars mean it runs smoothly, yellow means it is tight, red means the frame rate will drop

The score is a number where `{{v:performance.score-limit}}` is exactly the time one frame may take at your target frame rate. The band comes from the score:

| Bars | Band | Score |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | below `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | from `{{v:performance.score-warning}}` to `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | above `{{v:performance.score-limit}}`, up to `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | above `{{v:performance.score-heavy}}`, up to `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | above `{{v:performance.score-severe}}` |
| none | `{{ui:level_performance_unknown}}` | the level or the device has not been measured |

The score is a forecast for the heaviest moment of the level, not for its average. A level that is light for three minutes and freezes for one second gets the score of that second

## Where you see it

- the level browser: the gauge on every level card, and the `{{ui:root_level-filters_performance}}` group in the filters
- the level page in the menu: the gauge, the band and the score
- the level editor, in the level's metadata: the score on your device and on the reference devices, plus the heaviest moments of the level as timestamps

## Two halves of the score

**The level's half** is measured in the editor in the seconds after each save, while you keep working, and stored in its metadata. If you leave the editor before it finishes, the file keeps the previous measurement. It describes what the level asks for: how many objects are alive, how much of the screen they cover, how many effects and post-processing passes run. A level saved before this feature has no such record and shows as `{{ui:level_performance_unknown}}` until it is saved again. The editor measures it when you open the level and keeps the result until you leave the editor, without writing it into the file

**The device's half** says how fast your device does each of those things. Until you measure your device, the game uses a reference device of your platform. Your settings count too: render scale, anti-aliasing, effects and post-processing all change the score without a new measurement

## Measuring your device

1. Open `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}` from the main menu
2. Press `{{ui:settings_graphics-performance_measure}}`. A window says what helps the measurement: close other apps and games, plug a phone or a laptop into a charger, do not touch the device
3. Press `{{ui:settings_graphics-performance_start}}` and wait up to {{v:performance.benchmark-max-seconds}} seconds. The settings screen hides, and the game plays test levels and shows what it measures in the top corners. Do not switch to another app

`{{ui:settings_graphics-performance_stop}}` ends the measurement early. A measurement that was stopped or ran out of time saves nothing, and the previous result stays

When it finishes, the window shows the result: the gauge of the demo level on your device, what limits your device (the processor or the graphics chip), which `{{ui:settings_quick-setup_performance}}` preset it suggests, and how many of your levels fall in each band. `{{ui:settings_graphics-performance_again}}` measures once more

If the measurement was unsteady (the device was too hot, another app was busy), the game still uses it, since it is closer to your device than any reference, and the window says so. Close other apps and measure again for a more exact score

## Moving to another device

The measurement belongs to the device it was taken on. A profile transfer ([[14_profile-transfer]]) and cloud saves do not carry it, so a new device starts from its reference device until you measure it again
