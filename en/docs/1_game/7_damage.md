---
title: Damage and lives
date: 2026-09-24
tags: [advanced_player]
---

# Damage and lives

What a hit does to the avatar, second by second, how lives are counted, and what a death does with checkpoints

## A hit in three stages

1. **The shove, `0.2` s.** You are pushed away from what hit you at `50` u/s, about 10 units, a full screen height, and answer no input at all. You cannot dash out of it: the knockback outranks everything
2. **Control returns** after those 0.2 s
3. **You still cannot be hit** for a full `1.0` s from the moment of the hit. Every further hit inside that second is ignored

Standing exactly on top of what hit you gives no direction to be pushed in, and then you are not pushed at all. You also cannot be hit while spawning (`0.3` s) or during a dash's own `0.3` s of protection, see [[6_avatar]]

> [!info] Worth knowing
> Sitting inside a hazard costs one life, not ten, and being shoved into a second hazard is survivable. A dense volley looks like instant death and is often cheaper than a single projectile arriving the moment the second of protection ran out

## Lives

The number of lives is a launch option on the level screen: `Zen`, `One life`, `Three lifes` or `Custom` up to 16 (see [[2_playing-levels]]). Every hit costs one life, and the hit that takes the last one is a death. `Zen` never ends the run

The ring of dots around the avatar shows them: a lit dot is a life in hand, a dim one is spent. The result window reports `Hits taken` and `Lives left`

## What a death does

With the default settings a death does not end the run:

1. The level clock eases to a stop over `0.5` s of real time, and the music bends down with it
2. The playhead jumps back to the last checkpoint you reached, and your lives are refilled
3. The clock eases back up to the run's speed over another `0.5` s. You cannot be hit during this ramp, otherwise a checkpoint next to live content would spend all your lives in the first second

Pausing pauses the ramp too. With `Checkpoints` off on the level screen, no checkpoint is ever reached and the rewind goes to the start of the level

`Settings`, `Interface`, `Open Menu on Lose` switches this off: playback stops and the result window opens. From there `Restart from Checkpoint` starts a new attempt from the checkpoint you reached

## Checkpoints

The level author places checkpoints. You decide whether they count, with the `Checkpoints` toggle. The checkpoint you have reached is simply the latest one at or before the playhead, so going back never needs anything undone

An author can also make a checkpoint restore health: crossing it refills your lives once, mid-run. The progress bar at the bottom of the game screen has a notch for every checkpoint (`Interface`, `Show Progress Bar`)

Each checkpoints setting keeps its own records, see [[10_statistics]]
