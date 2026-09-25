---
title: Bots
date: 2026-09-24
tags: [player, advanced_player]
---

# Bots

What a bot does when it plays a level for you, what it does not promise, what it costs, and how the two bots differ

**A bot plays the level for you, with your own controls.** It watches what is coming, looks for free room and moves the same character you would. It walks, dashes, takes damage and dies

**A bot does not guarantee a clear.** It never gets tired, but it can lose. If a pattern has to be entered correctly a second early, the bot will be hit. Nothing is broken when that happens

**A bot loads your device.** Looking for free room is real work on every frame. On a weak device expect a lower framerate. On a heavy level the first seconds are the worst

To pick a bot, use the `Bot` option on the level screen: `No Bot`, `Reflex Bot v1` or `Warm Bot v1`. It is chosen per run, like lives and speed

> [!info] Worth knowing
> A bot cannot cheat, and that is how it is built rather than a promise. It has the same controls you have and nothing more: the same speed, the same dash, the same hitbox, the same damage. It cannot pass through anything you could not

## A level beat the bot?

Bots get better on levels the developers have never seen. Such a level is worth sending in

Open an issue in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues). Say which bot lost and where, and attach the level folder

## The two bots

Every frame a bot produces one input, the same kind a keyboard produces, and nothing else. It has no access to the avatar's position, its health or the level's state.
If a bot does not answer on some frame, your own device steers on that frame

| | `Reflex Bot v1` | `Warm Bot v1` |
|---|---|---|
| What it knows | the next 1.5 seconds, recomputed every frame | the whole level, worked out once |
| When it loads the device | every frame, for as long as it runs | once, before the run |
| What it can do | avoid what it can see coming | follow a plan no lookahead would find |
| What breaks it | a pattern that had to be entered a second early | the level changing under it |
| How it steers | a direction | a target |

The warm bot aims for zero damage. It pays for that with an extra loading stage, `Baking route`. It can take tens of seconds

Before the calculation the game warns you. `Cancel` stops it and gives the run back to you.
The warm bot's route depends on the seed, [[8_determinism]]

## Where else bots play

- **The editor's preview player**: `Settings` → `Game Editor` → `Bot Steers The Player`. Only the reflex bot plays there: it needs nothing prepared and survives a scrub. More - [[5_bot-playtest]]
- **The main menu background**: the arena behind the buttons is the reflex bot playing live, with no lookahead at all

The bot is part of a record's conditions. So a run played by a bot never replaces your own best, [[10_statistics]]
