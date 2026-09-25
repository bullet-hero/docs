---
title: Readability and fairness
date: 2026-09-24
tags: [level_author]
---

# Readability and fairness

The player has to understand what killed them. Telegraphs, reaction time, contrast, and a hitbox that need not match the art

There is one test of fairness: **dying, does the player blame themselves or the level?**
Everything on this page pushes the answer towards "themselves"

## Telegraphing

A danger has to be visible before it becomes dangerous

A shape and a collider are two separate fields of one object.
So a warning is simple: a beam with a shape and no collider glows and never touches you. Half a second later a second one appears beside it, this time with a collider

The reverse is equally legal: an invisible wall is an object with no shape and a real collider

> [!caution] Caution
> An invisible danger is fair in exactly one case: the player already knows it is there, because the level showed it earlier

## Reaction time

A person sees and reacts in roughly 0.2 to 0.25 seconds at best.
At 60 level frames per second that is 12 to 15 frames

A danger appearing less than 12 frames before contact (10, for example) cannot be passed first time. It can only be learned.
When that is acceptable - [[3_difficulty-curve#Memorisation]]

## Contrast

What is dangerous must differ from the background more than decoration does.
The most common failure is a dark projectile on a dark background, at the exact moment the background is also changing

> [!tip] Recommendation
> Take both the background and the projectile colours from the theme. Then one theme edit keeps the contrast everywhere. Hand-typed colours keep it only until the first change

## One danger, one look

Every kind of danger needs its own recognisable look, and its own sound if you use one. Once the player has learned that a thing hurts, everything that looks like it has to hurt too

Never contradict your own signals. If something that looks like decoration kills in one place, the player stops trusting everything that looks like decoration

## Structure beats density

A screen full of motion reads as noise rather than as difficulty.
A player does not distinguish 40 projectiles. They distinguish a wall with a hole, a wave, a spiral, a corridor

Eight objects with structure are harder and fairer than forty without

## A level plays the same every time

A level has no conditions, counters or triggers reacting to the player. Everything is authored on the timeline.
Randomness does not change either: the same spot produces the same numbers on any device

So a level cannot be made reactive. It also cannot become unfair by accident, only by design

What does change between runs is chosen by the player: lives, playback speed and checkpoints.
More - [[3_difficulty-curve#What the player chooses]]

Next: [[3_difficulty-curve|Difficulty and the curve]], [[5_color-and-postprocessing|Colour, themes and post-processing]]
