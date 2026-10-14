---
title: Achievements
date: 2026-10-14
tags: [player]
---

# Achievements

Achievements unlock by themselves from your statistics. Only levels made by someone else count, and only runs played fairly. The list is in the main menu under `{{ui:menu_main_achievements-btn}}`

## The list

`{{ui:menu_main_achievements-btn}}` in the main menu opens every achievement of your build, in groups. A locked one shows how far you are, an unlocked one shows the day it unlocked. A secret achievement shows `{{ui:menu_achievements_hidden_name}}` until it unlocks

## What counts

**A fair run** is one where:

- no bot plays
- collisions are on
- the speed is `{{v:achievements.fair-min-speed}}` or higher
- you have lives: a run in `{{ui:menu_levelview_options-lifes_option-zen}}` counts only where an achievement asks for it

Checkpoints are allowed. A run started from the editor never counts, it sets no record either - [[10_statistics]]

**Not your own level.** A level you opened in the editor on this device is yours. Clearing it counts only for the achievement about testing your own level. Built-in levels, Workshop levels and levels from friends count

## Where it is stored

`stats/achievements.json`, next to the statistics. It only remembers when each achievement unlocked. Whether one is unlocked is decided from the statistics every time, so the file cannot be lost: delete it, and on the next launch everything you have earned comes back, dated that day

Clearing statistics in the settings keeps your achievements. A profile transfer and Steam Cloud carry the file: two devices end up with every achievement either one unlocked - [[14_profile-transfer]]

## Steam

In a Steam build every achievement is also unlocked on Steam, and Steam shows its own notification. Steam's record wins: an achievement Steam has is unlocked in the game with Steam's date. One the game has and Steam does not is unlocked again if your statistics still justify it

Every other build shows the game's own notification at the top of the screen
