---
title: Damage and lives
date: 2026-09-24
tags: [advanced_player]
---

# Damage and lives

What a hit does to the avatar, second by second, how lives are counted, and what a death does with checkpoints

## A hit in three stages

1. **The shove, `0.2` s.** You are pushed away from what hit you at `50` units per second. That is about 10 units, a full screen height. No input is accepted meanwhile. You cannot dash out of it: the knockback outranks everything
2. **Control returns** after those 0.2 s
3. **You cannot be hit** for a full `1.0` s from the moment of the hit. Every hit inside that second is ignored

If you stand exactly on top of what hit you, there is nowhere to push you. Then you are not pushed at all

You also cannot be hit while spawning (`0.3` s) or during a dash's `0.3` s of protection, [[6_avatar]]

> [!info] Worth knowing
> Sitting inside a hazard costs one life, not ten. Being shoved into a second hazard is survivable too. A dense volley looks like instant death and is often cheaper than a single projectile that arrives right as the second of protection ends

## Lives

The number of lives is chosen on the level screen: `Zen`, `One life`, `Three lifes` or `Custom` up to 16, [[2_playing-levels]]

Every hit costs one life. The hit that takes the last one is a death.
`Zen` never ends the run

The ring of dots around the avatar shows your lives: a lit dot is a life in hand, a dim one is spent.
The result window reports `Hits taken` and `Lives left`

## What a death does

By default a death does not end the run:

1. The level clock eases to a stop over `0.5` s of real time. The music bends down with it
2. The level jumps back to the last checkpoint you reached. Your lives are refilled
3. The clock eases back up to the run's speed over another `0.5` s. You cannot be hit during this ramp, otherwise a checkpoint next to a dangerous spot would take all your lives in the first second

Pausing pauses the ramp too

With `Checkpoints` off on the level screen, the rewind goes to the start of the level

To make a death open the result window, turn on `Settings` → `Interface` → `Open Menu on Lose`. Playback then stops.
From the window, `Restart from Checkpoint` starts a new attempt from the checkpoint you reached

## Checkpoints

The level's author places checkpoints. You decide whether they count, with the `Checkpoints` toggle

The checkpoint you have reached is the latest one at or before the current position in the level. So going back to it undoes nothing, it only rewinds

An author can make a checkpoint restore health. Crossing it then refills your lives once, mid-run

The progress bar at the bottom of the screen has a notch for every checkpoint. The bar is turned on in `Interface` → `Show Progress Bar`

Runs with and without checkpoints keep separate records, [[10_statistics]]
