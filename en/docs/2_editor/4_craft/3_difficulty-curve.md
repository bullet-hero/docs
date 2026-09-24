---
title: Difficulty and the curve
date: 2026-09-24
tags: [level_author]
---

# Difficulty and the curve

What the player can physically do, in numbers, how to build a curve, and why you cannot judge your own level

Difficulty cannot be discussed without numbers, so they come first: what the player's character can do, what a hit costs and what the player decides for themselves

## The player in numbers

The player's avatar is drawn `0.5` wide, but its hitbox is a circle of only `0.15` in radius. Ordinary speed is `15` per second. The dash is `50` per second, lasts `0.15 s` and recharges over `0.3 s`, so one dash is `7.5` units covered almost instantly, and you are invulnerable for the whole `0.3 s`

Everything else follows. A gap one unit wide is more than six hitbox radii, which is wide. A gap of 0.6 is tight. 7.5 units is half a second of running, or one dash

## A hit is not a death

After being hit the player is knocked back and has no control for `0.2 s`, and every further hit is ignored for a full `1 s`. A wall of ten projectiles in a row costs one life, not ten

> [!info] Worth knowing
> Intuition says the opposite. A dense volley looks like instant death and is in fact cheaper than a single projectile arriving the moment invulnerability ran out

## What the player chooses

The number of lives, the playback speed and whether checkpoints are on are chosen by the player on the launch screen. The defaults are 3 lives, speed 1.0, checkpoints on. You can place checkpoints, you cannot make anyone use them, and you cannot forbid playing at half speed

Design against the default, but build nothing on "they will die here". What you design is a sensation, not a punishment

## The curve: teach, test, twist

Show the pattern first in a safe form where failing is nearly impossible. Then demand it for real. Then change one variable - speed, direction, count - and demand it again

A pattern appearing for the first time already in its hard form is the case where the level gets blamed. The player dies without having understood what was wanted

## Memorisation

A level passable only from memory is a legitimate genre, but it has to be a decision rather than an accident. The line is that after dying, the player has to understand what there is to memorise. Still unclear after the tenth death is not memorisation, it is noise

## Testing on someone else

You cannot judge your own level. By the time you publish, you have passed your own hard section two hundred times and it is easy to you

> [!tip] Recommendation
> Hand it to someone seeing it for the first time and watch in silence. No hints. A place where a person dies three times and asks what the level wanted is not a hard place, it is an unclear one

## Start short

Make a first level 1 to 2 minutes long. Interest runs out before the track does, and a four-minute level is four times the work and ten times the reasons to stop

Next: [[1_readability-and-fairness|Readability and fairness]], [[4_composition-and-camera|Composition and the camera]]
