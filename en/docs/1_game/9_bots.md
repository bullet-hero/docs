---
title: Bots
date: 2026-09-24
tags: [player, advanced_player]
---

# Bots

What a bot does when it plays a level for you, what it never promises, what it costs, and how the two bots differ

**A bot plays the level for you, with your own controls.** It watches what is coming, works out where there is room, and moves the same character you would - it walks, it dashes, it takes damage and it dies

**It is not a guarantee that the level gets cleared.** A bot is a player that never gets tired, not a player that never loses. On a level built around a pattern you have to enter correctly a second early, it will be hit - and nothing is broken when that happens

**It costs performance while it runs.** Working out where the room is takes real work on every frame, so on a weak device expect a lower framerate, and on a heavy level expect the first seconds to be the worst

> [!info] Worth knowing
> A bot cannot cheat, and that is how it is built rather than a promise. It has exactly the controls you have and nothing more - the same speed, the same dash, the same hitbox, the same damage. There is no path through the game that lets it pass through something you could not

**Bots get better on levels the developers have never seen.** A level that beats one is worth sending in: open an issue on [the SDK repository](https://github.com/vertoker/bullet-hero-sdk), say which bot lost and where, and attach the level folder

## How a bot plays

Every frame a bot produces one input, the same kind a keyboard produces, and nothing else. It has no access to the avatar's position, its health or the level's state. If a bot declines to answer on some frame, you keep your own device for that frame

| | `Reflex Bot v1` | `Warm Bot v1` |
|---|---|---|
| What it knows | the next 1.5 seconds, recomputed every frame | the whole level, worked out once |
| When it pays | every frame, for as long as it runs | once, before the run |
| What it can do | avoid what it can see coming | commit to a plan no lookahead would find |
| What breaks it | a pattern that had to be entered a second early | the level changing under it |
| How it steers | a direction | a target |

The warm bot aims for zero damage and pays for it with an extra loading stage, `Baking route`, which can take tens of seconds. Before it starts the game warns you, and `Cancel` stops the calculation and gives the run back to you. Its route depends on the seed, see [[8_determinism]]

## Where bots play

- **The level screen**, the `Bot` option: `No Bot`, `Reflex Bot v1` or `Warm Bot v1`, chosen per run like lives and speed
- **The editor's preview player**: `Settings`, `Game Editor`, `Bot Steers The Player`. Only the reflex bot plays there, because it needs nothing prepared and survives a scrub, see [[5_bot-playtest]]
- **The main menu background**: the arena behind the buttons is the reflex bot playing live, with no lookahead at all

The bot is part of a record's conditions, so a run played by a bot never replaces your own best, see [[10_statistics]]
