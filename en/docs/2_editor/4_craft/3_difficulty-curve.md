---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

What the player can physically do, in numbers, how to build a curve, and why you cannot judge your own level

## The player in numbers

Design a level against these numbers:

| What | Value |
|---|---|
| Player hitbox | a circle `0.15` world units in radius, while the avatar is drawn `0.5` wide |
| Ordinary speed | `15` units per second |
| Dash | `50` units per second for `0.15 s`, recharge `0.3 s` |
| Invulnerability on a dash | the whole `0.3 s` |
| One dash | `7.5` units, covered almost instantly |
| After a hit | no control for `0.2 s`, further hits ignored for `1 s` |
| Human reaction | 0.2 to 0.25 seconds, which is 12 to 15 frames at 60 fps |
| Launch defaults | 3 lives, speed 1.0, checkpoints on |

Everything else follows from these numbers:
- a gap one unit wide is more than six hitbox radii, which is wide
- a gap of 0.6 is tight
- 7.5 units is half a second of running, or one dash

## A hit is not a death

After being hit the player is knocked back and has no control for `0.2 s`.
Every further hit is ignored for a full `1 s`. A wall of ten projectiles in a row costs one life, not ten

> [!info] Worth knowing
> Intuition says the opposite. A dense volley looks like instant death. In fact it is cheaper than a single projectile arriving the moment invulnerability ran out

## What the player chooses

Lives, playback speed and checkpoints are chosen by the player on the launch screen.
The defaults are 3 lives, speed 1.0, checkpoints on

You can place checkpoints, but you cannot make anyone use them. And you cannot forbid playing at half speed

Design against the defaults, but build nothing on "they will die here".
What you design is a sensation, not a punishment

## The curve: teach, test, twist

1. Show the pattern in a safe form where failing is nearly impossible
2. Demand it for real
3. Change one variable - speed, direction, count - and demand it again

If a pattern first appears already in its hard form, the level gets blamed.
The player dies without understanding what was wanted

## Memorisation

A level passable only from memory is a legitimate genre. But it has to be a decision rather than an accident

The line is simple: after dying, the player has to understand what there is to memorise.
Still unclear after the tenth death is not memorisation, it is noise

## Testing on someone else

You cannot judge your own level.
By the time you publish, you have passed your own hard section two hundred times and it is easy to you

> [!tip] Recommendation
> Hand the level to someone seeing it for the first time and watch in silence. No hints. A place where a person dies three times and asks what the level wanted is not hard, it is unclear

## Start short

Make a first level 1 to 2 minutes long.
Interest runs out before the track does. A four-minute level is four times the work and ten times the reasons to stop

Next: [[1_readability-and-fairness|Readability and fairness]], [[4_composition-and-camera|Composition and the camera]]
