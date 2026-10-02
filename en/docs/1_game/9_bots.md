---
title: Bots
date: 2026-10-02
tags: [player, advanced_player]
---

# Bots

A bot plays a level for you with your own controls. It watches what is coming, looks for free space and moves the same character you do: it walks, dashes, takes damage and dies

**A bot does not guarantee a clear.** It does not get tired, but it can lose. If a pattern has to be entered correctly a second before it arrives, the bot gets hit. Nothing is broken when that happens

**A bot loads the device.** Searching for free space is real work on every frame. Expect frame drops on a weak device. On a heavy level the first seconds are the worst

To choose a bot, use the `{{ui:menu_levelview_options-bot}}` condition on the level screen: `{{ui:enum_bot-kind_none}}`, `{{ui:enum_bot-kind_reflex}}` or `{{ui:enum_bot-kind_warm}}`. It is chosen for each run, like lives and speed

> [!info] Worth knowing
> A bot cannot cheat, and that is how it is built, not a promise. It has the same controls you have and nothing more: the same speed, the same dash, the same hitbox, the same damage. It cannot pass through anything you could not pass through

## A level beat the bot?

Bots get better on levels they have not seen yet. Such a level is worth sending

Open an issue in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Write which bot lost and where, and attach the level folder

## Two bots

Every frame a bot gives one input, the same as a keyboard does, and nothing else. It has no access to the avatar's position, its health or the state of the level.
If the bot does not answer on some frame, your device steers on that frame

| | `{{ui:enum_bot-kind_reflex}}` | `{{ui:enum_bot-kind_warm}}` |
|---|---|---|
| What it knows | the next 1.5 seconds, recalculated every frame | the whole level, calculated once |
| When it loads the device | every frame while it runs | once, before the run |
| What it can do | avoid what it sees ahead | follow a plan no look-ahead would ever find |
| What breaks it | a pattern that had to be entered a second earlier | a level that changed under it |
| How it steers | by direction | by target |

The warm bot aims for zero damage. It pays for that with an extra loading stage, `{{ui:root_loading_baking}}`. It can last tens of seconds

The `?` next to `{{ui:menu_levelview_options-bot}}` warns about this in advance, with a paragraph per bot. `{{ui:root_loading_cancel}}` stops the calculation and hands the run to you.
The warm bot's route depends on the seed, [[8_determinism]]

## Where else bots play

- **The editor's test player**: `{{ui:settings_common_title}}` → `{{ui:settings_game-editor_title}}` → `{{ui:settings_game-editor-player_bot}}`. Only the reflex bot plays there: it needs nothing prepared in advance and it survives rewinding. More - [[5_bot-playtest]]
- **The main menu background**: the arena behind the buttons is a reflex bot playing live with no look-ahead at all

The bot is part of a record's conditions. So a bot's run never replaces your best result, [[10_statistics]]
