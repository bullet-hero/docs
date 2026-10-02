---
title: How a bot plays your level
date: 2026-10-02
tags: [level_author]
---

# How a bot plays your level

A bot plays the level with the same controls you have and checks readability, not difficulty. It does not guarantee the level gets cleared

It watches what is flying, looks for free room and moves the same character you do.
It walks, dashes, takes damage and dies

The bot is chosen before a level starts, next to lives and speed

## A bot in the editor

In the editor a bot steers the preview player:
1. Open `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_player_title}}`
2. Tick `{{ui:settings_game-editor-player_bot}}`
3. Switch the preview player on in the toolbar

The preview player has no choice of bot, it is always `{{ui:enum_bot-kind_reflex}}`. Only this bot needs nothing prepared in advance.
It keeps working while you edit the level, at any playback speed, backwards included

Right after a scrub the bot plays worse for a moment: it is learning again what lies ahead

While you drag a gizmo handle or type in a text field, the preview player does not listen to your controls

**`{{ui:settings_game-editor-player_bot-debug}}`** in the same settings draws over the level. It is off by default, and its three parts are on, so once you switch it on you see the whole picture at once:
- `{{ui:settings_game-editor-player_bot-debug-grid}}` - how much free room the bot thinks each part of the screen has. Red is where it expects a hit, and the colour fades as the room grows. Nothing is drawn where it considers itself safe
- `{{ui:settings_game-editor-player_bot-debug-target}}` - the point it is heading for. A target that does not move means the bot is satisfied, not stuck
- `{{ui:settings_game-editor-player_bot-debug-reach}}` - how far it expects to get: the inner ring by walking, the outer one with a dash. It never picks a target outside them

Only `{{ui:enum_bot-kind_reflex}}` is drawn. Switch it on while paused, where the picture stands still

**A full run with any bot.** In the level settings, on the `{{ui:settings_level-settings_play}}` tab, there is the same `{{ui:settings_level-settings_bot}}` list as on the level screen in the menu: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`. This starts a real run of the level, not the preview player

## Reading the result

A bot checks readability, not difficulty:
- the bot calmly passes a section that is hard for you. Then the section reads well, and you lack practice
- the bot is hit in the same place again and again. Look at that place: usually it is a hazard that leaves no room to get away. A human will not read it any better

## What a bot promises and what it does not

**A bot does not guarantee the level gets cleared.** It is a player that does not get tired, not a player that does not lose.
If a section requires entering a pattern correctly a second before it, the bot will be hit. This is not a bug

> [!info] Worth knowing
> A bot cannot cheat, that is how it is built. It has the same controls as a player and nothing more: the same speed, the same dash, the same hitbox, the same damage. Where a player cannot pass, the bot cannot either

**A bot loads the device.** It looks for free room on every frame.
On a weak device expect frame drops. On a heavy level the first seconds will be the worst

## A level that beat the bot

Bots get better only on levels they have not seen yet. Levels a bot already clears teach it nothing

Did your level beat the bot? Send it in:
1. Open an issue in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)
2. Write which bot lost and where
3. Attach the level folder

Next: [[1_readability-and-fairness|Readability and fairness]], [[3_difficulty-curve|Difficulty]]
