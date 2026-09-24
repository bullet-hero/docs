---
title: Determinism
date: 2026-09-24
tags: [advanced_player]
---

# Determinism

Why a level with the same seed plays the same on every device, how randomness works and what this gives you

## A level is a function of time

A level is built on a timeline. Every object lives on a stretch of frames and moves along keyframes

A level does not read what you do. So frame 1200 looks the same whether you are alive, dead, dashing or played by a bot

Influence runs one way. A level may resize the avatar, slow it, take its controls or switch its collision off. There is no channel back from the avatar to the level

There are no triggers. The developers discuss them for later versions, but nothing is decided

A level runs against real time. The framerate only sets how often the screen is redrawn.
The same run plays identically at 30 and at 144 frames per second

## The seed

The seed comes from the first place that sets one:

1. `Player Seed` on the level screen (`Randomize` picks a new one, `Clear` removes it)
2. the level's own seed, set by its author
3. a fresh seed for this run

`0` means "not set". So an ordinary level takes a new seed every time it loads

The result window shows the seed of a run, and a record stores it. That way a good run can be replayed

## How randomness works

A random value in a level is not taken from a generator that remembers its state. It is computed from its address:

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

The same address always gives the same number. On any device and in any order of computation.
Every part of the address is something the author edits. So the same layout repeats the same run

## What this gives you

- **The warm bot** works out a route through the whole level before the run starts. This works because exactly the level it planned against is the one that plays
- **The reflex bot** builds frames ahead of the current one and steers against them
- **Checkpoint rewinds** rebuild the target frame instead of undoing anything
- **The editor** builds any frame from scratch, so scrubbing is instant
- **Records and statistics** mean the same thing on every device

## Known limits

The level side is deterministic. The avatar side has defects the developers have listed and not yet fixed:

- two hazards touch the avatar on the same frame. Which one aims the knockback can differ between runs
- the avatar's clock is not reset when a level starts. A dash can last one frame longer or shorter, depending on how long the level took to load

A repeat of the same bot run on the same build was measured identical to the last digit. So these defects do not fire on every level.
Because of them, a run is reproducible in practice, but not by guarantee
