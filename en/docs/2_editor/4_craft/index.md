---
title: Craft
date: 2026-09-24
tags: [level_author]
---

# Craft

Level design: readability, rhythm, difficulty, composition and colour

This section is about what makes a level good to play rather than merely correct: the player understands what killed them, moves with the music and wants to try again. It assumes you already know the six ideas from [[3_how-the-editor-thinks]] and have played one level of your own to the end

## One test of fairness

Dying, does the player blame themselves or the level? Every page here pushes the answer towards the first. A level is deterministic: it has no conditions, counters or triggers reacting to the player, and randomness gives the same numbers on any device. So a level cannot become unfair by accident, only by design

## The numbers to design against

| What | Value |
|---|---|
| Player hitbox | a circle `0.15` in radius, while the avatar is drawn `0.5` wide |
| Ordinary speed | `15` units per second |
| Dash | `50` units per second for `0.15 s`, recharge `0.3 s`, invulnerable for the whole `0.3 s` |
| After a hit | no control for `0.2 s`, further hits ignored for `1 s` |
| Human reaction | 0.2 to 0.25 seconds, which is 12 to 15 frames at 60 fps |
| Launch defaults | 3 lives, speed 1.0, checkpoints on, all chosen by the player |

A danger that appears less than 12 frames before contact cannot be passed first time, it can only be learned. [[3_difficulty-curve]] shows how the rest follows from these numbers

## Five areas

- **Readability.** A danger is visible before it becomes dangerous, and structure beats density: eight objects in a pattern are harder and fairer than forty without one. See [[1_readability-and-fairness]]
- **Rhythm.** The beat grid is for you, playback never reads it. The size of a movement carries the strength of a sound, and the level peaks where the track does. See [[2_rhythm-and-structure]]
- **Difficulty.** Teach, test, twist: show a pattern safely, demand it, then change one variable. See [[3_difficulty-curve]]
- **Composition.** Screens differ in aspect ratio, and a phone cutout can cover a projectile, so meaningful content stays away from the edge. The camera is a tool, and constant shake makes a level physically impossible to finish. See [[4_composition-and-camera]]
- **Colour.** Theme references instead of literal colours, and contrast checked on every theme. Post-processing turns on at a peak and off again. See [[5_color-and-postprocessing]]

> [!tip] Recommendation
> You cannot judge your own level, because after two hundred runs every hard section is easy to you. Hand it to someone seeing it for the first time and watch in silence. A place where a person dies three times and asks what the level wanted is not hard, it is unclear

> [!info] Worth knowing
> Lives, playback speed and checkpoints are the player's choice on the launch screen. What you design is a sensation, not a punishment, so build nothing on "they will die here"
