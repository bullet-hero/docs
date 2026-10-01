---
title: Difficulty and the curve
date: 2026-10-01
tags: [level_author]
---

# Difficulty and the curve

Design against the numbers: the player's hitbox is a circle of radius 0.15 units, speed is 15 units per second, reaction is 12-15 frames. Show a new pattern in a safe form first

You cannot judge your own difficulty: test the level on someone who sees it for the first time

## The player in numbers

Design the level against these numbers:

| What | Value |
|---|---|
| Player hitbox | a circle `0.15` world units in radius, although the avatar is drawn `0.5` wide |
| Ordinary speed | `15` units per second |
| Dash | `50` units per second for `0.15 s`, recharge `0.3 s` |
| Invulnerability on a dash | the whole `0.3 s` |
| One dash | `7.5` units, almost instantly |
| After a hit | no control for `0.2 s`, further hits ignored for `1 s` |
| Human reaction | 0.2-0.25 seconds, which is 12-15 frames at 60 fps |
| Launch values | 3 lives, speed 1.0, checkpoints on |

Everything else is worked out from these numbers:
- a gap one unit wide is more than six hitbox radii, which is wide
- a gap of 0.6 is tight
- 7.5 units is half a second of running or one dash

## A hit does not kill at once

After a hit the player is knocked back and has no control for `0.2 s`.
Further hits are ignored for a whole `1 second`. A wall of ten projectiles in a row costs one life, not ten

> [!info] Worth knowing
> Intuition says the opposite. A dense volley looks like instant death. In fact it is cheaper than a single projectile arriving exactly when invulnerability has run out

## What the player chooses

Lives, playback speed and checkpoints are chosen by the player on the launch screen.
The defaults are 3 lives, speed 1.0, checkpoints on

You can place checkpoints, but you cannot make anyone use them. And you cannot forbid playing at half speed

Design against the defaults, but build nothing on the calculation "this is where they die".
You are designing a sensation, not a punishment

## The loop

The player repeats one loop: play, die, try again. A good level builds its layers on top of it, and the loop has to be:
- simple at the start, with no hard mechanics right away
- expandable, so new elements arrive gradually and it does not get stale
- rewarding, because an immediate reward for the right action keeps motivation up

## The curve: teach, test, twist

1. Show the pattern in a safe form where a mistake is almost impossible
2. Demand it for real
3. Change one variable - speed, direction, count - and demand it again

If a pattern first appears straight away in its hard form, the level gets the blame.
The player dies and does not understand what was wanted

Fairness has a limit too. Too much "hand-holding" takes the fun away just as unfairness does

## Memorisation

A level that can only be passed from memory is a legitimate genre. But it has to be a decision, not an accident

The line is simple: after dying, the player has to understand what exactly to remember.
Still unclear after the tenth death is not memorisation, it is noise

## Testing through someone else's eyes

You cannot judge your own level yourself.
By the time you publish, you have passed your own hard spot two hundred times, and to you it is easy

> [!tip] Recommendation
> Give the level to someone who sees it for the first time and watch in silence. Do not give hints. A spot where a person dies three times and asks what was wanted is not hard, it is unclear

## Start short

Make the first level 1-2 minutes long.
Interest runs out before the track does. A four-minute level is four times the work and ten times the reasons to stop

Next: [[1_readability-and-fairness|Readability and fairness]], [[4_composition-and-camera|Composition and the camera]]
