---
title: Determinism
date: 2026-10-02
tags: [advanced_player]
---

# Determinism

A level with the same seed plays the same on any device and at any frame rate. Its randomness is computed from the seed, and your actions do not affect the level

## A level is a function of time

A level is built on a timeline. Every object lives on a span of frames and moves along keyframes

The level does not read your actions. So frame 1200 looks the same whether you are alive, dead, dashing or a bot is playing for you

Influence goes one way. A level can change the avatar's size, slow it down, take control away or turn collisions off. There is no channel back from the avatar to the level

There are no triggers. They are being discussed for future versions, but nothing is decided

A level runs on real time. The frame rate only sets how often the screen is redrawn.
The same run plays the same at 30 and at 144 frames per second

## The seed

The seed is taken from the first place where it is set:

1. `{{ui:level_level-view_seed-value}}` on the level screen (`{{ui:level_level-view_seed-randomize}}` picks a new one, `{{ui:level_level-view_seed-clear}}` removes it)
2. the level's own seed, set by the author
3. a new seed for this run

`0` means "not set". So an ordinary level takes a new seed on every load

The result window shows the run's seed, and the record stores it. That way a lucky run can be repeated

## How randomness works

A random value in a level does not come from a generator that remembers its state. It is computed from its address:

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

The same address always gives the same number. On any device and in any order of computation.
Every part of the address is something the author edits. So the same layout repeats the same run

## What this gives you

- **The Warm bot** plans a route through the whole level before the run starts. That is possible because exactly the level it planned for is the one that plays
- **The Reflex bot** builds frames ahead of the current one and dodges by them
- **Rewinding to a checkpoint** builds the needed frame again rather than undoing anything
- **The editor** builds any frame from scratch, so scrubbing is instant
- **Records and statistics** mean the same thing on any device

## Known limits

The level side is deterministic. The avatar side has known defects that are not fixed yet:

- two obstacles hit the avatar on the same frame. Which of them sets the knockback direction can differ between runs
- the avatar's clock is not reset when the level starts. A dash can last a frame longer or shorter, depending on how long the level took to load

Repeating the same bot run on one build matched to the last digit when measured. So these defects do not fire on every level.
Because of them a run is reproducible in practice, but not guaranteed
