---
title: Determinism
date: 2026-09-24
tags: [advanced_player]
---

# Determinism

Why a level with the same seed plays the same on every device, how randomness works without drawing numbers, and what this buys

## A level is a function of time

A level is authored on a timeline: every object lives on a stretch of frames and moves along keyframes. There are no triggers. Nothing in a level reads what you do, so frame 1200 of a level looks the same whether you are alive, dead, dashing or played by a bot

Influence runs one way. A level may resize the avatar, slow it, take its controls or switch its collision off, and there is no channel back from the avatar to the level. A trigger system is discussed by the developers for a later version, and nothing about it is decided

The level is simulated against real time, and the framerate only sets how often the screen is redrawn. The same run plays identically at 30 and at 144 frames per second

## Randomness is addressed, not drawn

A random value in a level is not taken from a generator that remembers its state. It is computed from its address:

`Hash(seed, keyframe frame, layer, start frame, track, channel)`

The same address always gives the same number, on any device and in any order the processor happens to work in. Every part of it is something the author edits, so reproducing the layout reproduces the run

The seed comes from the first of three places that sets one:
1. `Player Seed` on the level screen (`Randomize` rolls one, `Clear` removes it)
2. the level's own seed, set by its author
3. a fresh seed for this run

`0` means "not set", so an ordinary level rolls a new seed every time it loads. The result window shows the seed a run used, and a record stores it, so a good run can be replayed

## What this buys

- **The warm bot** works out a route through the whole level before the run starts. That is only possible because the level it planned against is the level that will play
- **The reflex bot** builds frames ahead of the current one and steers against them
- **Checkpoint rewinds** rebuild the target frame instead of undoing anything
- **The editor** builds any frame from scratch, which is what makes scrubbing instant
- **Records and statistics** mean the same thing on every device

## Known limits

The level side is deterministic. The avatar side has defects the developers have listed and not yet fixed:

- when two hazards touch the avatar on the same frame, which one aims the knockback can differ between two runs
- the avatar's clock is not reset when a level starts, so a dash can last one frame longer or shorter depending on how long the level took to load

A repeat of the same bot run on the same build was measured identical to the last digit, so these do not fire on every level. They are why a run is reproducible in practice rather than by guarantee
