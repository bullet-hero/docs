---
title: Letting a bot play your level
date: 2026-09-24
tags: [level_author]
---

# Letting a bot play your level

What a bot does, what it never promises, what it costs, and how to use one to test the level you are building

A bot plays the level with your own controls. It watches what is coming, looks for room, and moves the same character you would.
It walks, dashes, takes damage and dies

You pick a bot before a run, next to lives and speed

## A bot in the editor

In the editor a bot steers the preview player:
1. Open `Settings` → `Game Editor` → `Preview Player`
2. Tick `Bot Steers The Player`
3. Switch the preview player on in the toolbar

The preview player has no choice of bot, it is always `Reflex Bot v1`. Only this bot needs nothing prepared in advance.
It keeps working while you edit, at any playback speed, backwards included

Right after a scrub the bot plays worse for a moment: it is relearning what is coming

While you drag a gizmo handle or type in a text field, the preview player ignores your own controls

**`Show What The Bot Sees`** under the same settings draws over the level. It is off by default, and its three parts are on, so switching it on shows the whole picture at once:
- `Clearance Field` - how much room the bot believes each part of the screen has. Red is where it expects to be hit, and the colour fades out as the room grows. Nothing is drawn where it considers itself safe
- `Chosen Target` - the point it is heading for. A target that stops moving means the bot is satisfied, not stuck
- `Reach Rings` - how far it thinks it can get: the inner ring by walking, the outer one with the dash. It never picks a target outside them

Only `Reflex Bot v1` is drawn. Turn it on while paused, where the picture holds still

**A full run with any bot.** Level Settings, the `Play` tab, has the same `Bot` dropdown as the level screen in the menu: `No Bot`, `Reflex Bot v1`, `Warm Bot v1`. That starts a real run of the level, not the preview player

## Reading the result

A bot is a readability check, not a difficulty check:
- the bot walks calmly through a section you find hard. Then the section is readable, and you are unpractised
- the bot is hit again and again in one place. Look at that place: it is usually a hazard that leaves no room to escape. A human reads it no better

## What a bot promises and what it does not

**A bot does not guarantee the level gets cleared.** It is a player that never gets tired, not a player that never loses.
If a section asks you to enter a pattern correctly a second early, the bot will be hit. Nothing is broken

> [!info] Worth knowing
> A bot cannot cheat, that is how it is built. It has exactly the controls a player has and nothing more: the same speed, the same dash, the same hitbox, the same damage. Where a player cannot pass, neither can the bot

**A bot costs performance.** It looks for room on every frame.
On a weak device expect a lower framerate. On a heavy level the first seconds will be the worst

## A level that beats a bot

Bots get better only on levels the developers have never seen. Levels a bot already clears teach it nothing

Did your level beat a bot? Send it in:
1. Open an issue in [bullet-hero/releases](https://github.com/bullet-hero/releases/issues)
2. Say which bot lost and where
3. Attach the level folder

Next: [[1_readability-and-fairness|Readability and fairness]], [[3_difficulty-curve|Difficulty]]
