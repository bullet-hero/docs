---
title: Readability and fairness
date: 2026-10-01
tags: [level_author]
---

# Readability and fairness

The player has to understand what killed them. Show a danger before it becomes dangerous, give at least 12 frames to react and make danger stand out more than decoration

There is one test of fairness: **dying, does the player blame themselves or the level?**
Everything on this page pushes the answer towards "themselves"

## Telegraphing

A danger has to be visible before it becomes dangerous

A shape and a collider are two separate fields of one object.
So a warning is simple: a beam with a shape and no collider glows and does not hit. Half a second later a second one appears beside it, this time with a collider

The reverse is legal too: an invisible wall is an object with no shape but a real collider

> [!caution] Caution
> An invisible danger is fair in one case only: the player already knows it is there, because the level showed it earlier

## Reaction time

A person notices a danger and reacts in roughly 0.2-0.25 seconds at best.
At 60 level frames per second that is 12-15 frames

A danger that appears less than 12 frames before contact (10, for example) cannot be passed the first time. It can only be learned.
When that is acceptable - [[3_difficulty-curve#Memorisation]]

## Contrast

What is dangerous has to differ from the background more than decoration does.
The most common failure is a dark projectile on a dark background, at exactly the moment the background is changing too

> [!tip] Recommendation
> Take both the background and the projectile colours from the theme. Then one theme edit keeps the contrast everywhere. Hand-typed colours keep it only until the first edit

## One danger, one look

Every kind of danger needs its own recognisable look, and its own sound if you use sound. Once the player has learned that such a thing hits, everything that looks the same has to hit too

Do not contradict your own signals. If something that looks like decoration kills in one place, the player stops trusting everything that looks like decoration

## Structure beats density

A screen full of motion reads as noise, not as difficulty.
A player does not tell apart 40 projectiles. They tell apart a wall with a hole, a wave, a spiral, a corridor

Eight objects with structure are harder and fairer than forty without it

## A level always plays the same

A level has no conditions, counters or triggers that react to the player. Everything is written on the timeline.
Randomness does not change either: the same spot gives the same numbers on any device

So a level cannot be made reactive. But it cannot become unfair by accident either, only on purpose

Between runs only what the player chooses changes: lives, playback speed and checkpoints.
More - [[3_difficulty-curve#What the player chooses]]

Next: [[3_difficulty-curve|Difficulty and the curve]], [[5_color-and-postprocessing|Colour, themes and post-processing]]
