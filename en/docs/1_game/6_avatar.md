---
title: Avatar and movement
date: 2026-09-24
tags: [advanced_player]
---

# Avatar and movement

Every number the avatar moves with: walking, the dash, the hitbox, spawning, and how a level can scale them

Distances are in world units. The default camera is exactly 10 units tall, so a unit is a tenth of the screen's height.
Zooming the camera changes how much you see, not the numbers below

## The numbers

| What | Value | In plain terms |
|---|---|---|
| Walking speed | `15` u/s | crosses the screen top to bottom in two thirds of a second |
| Dash speed | `50` u/s | 3.3 times the walk |
| Dash duration | `0.15` s | |
| Dash reach | `7.5` u | three quarters of the screen's height |
| Dash cooldown | `0.3` s | counted from the start of the dash |
| Dash invulnerability | `0.3` s | also from the start, so it outlasts the movement by 0.15 s |
| Shortest dash | `0.5` u | one avatar body. Nearer than that, there is no dash |
| Body size | `0.5` u | the drawn square |
| Hitbox | radius `0.15` u | 0.3 of the body, smaller than what you see on purpose |
| Spawn and despawn | `0.3` s | grows in, shrinks to a point |

Movement is instant: no acceleration, no slide, no momentum. You stop on the same frame you stop moving

What happens on a hit - [[7_damage]]

## The dash

Invulnerability lasts 0.15 s longer than the movement. This landing grace is what lets you dash *through* an obstacle

You steer during a dash. A dash with no direction held moves nothing

With a cursor, the dash goes where you point:

| Cursor distance | What happens |
|---|---|
| further than 7.5 u | a full dash towards it |
| 0.5 to 7.5 u | a shorter dash that ends exactly on the cursor |
| nearer than 0.5 u | no dash. The press costs nothing |

A shorter dash is the same dash scaled down. Travel, invulnerability and cooldown shrink together, so two half dashes cost exactly what one full dash costs

In `Direction` mode a dash always goes the full 7.5 u. Neither style is stronger: one gives precision, the other simplicity

**Holding dash is not invulnerability.** Cooldown and protection are the same length, so dashes can chain. But between two dashes there is always exactly one frame where you can be hit, at any framerate.
The tightest chain is a dash every third frame at 60 fps

## The hitbox

The ring of dots on the avatar sits exactly on the hitbox. A bullet clipped your outline and did nothing? That is intended

The same ring shows your lives: a lit dot is a life in hand

`Settings` → `Interface` → `Hitbox Ring Opacity` sets how visible the ring is. `0` hides it, but levels are balanced for someone who can see it

The body is a grid of 64 squares. As you lose health, it loses squares from the rim inwards.
With `Graphics` → `Shatter Effect` off, the body is one square that fades instead. This is for weaker devices

## Scaling

A level can animate the avatar's size and speed through its own tracks. It can also take your controls away or switch collision off for a while

- Walk, dash and knockback speeds are multiplied by the same number. So half speed also halves the dash reach (3.75 u)
- A bigger avatar moves proportionally faster, because its dodges grew too. The hitbox grows with the body
- Dash aiming uses the current reach, not the 7.5 from the table
- Windows in seconds are not scaled: cooldown, invulnerability, damage timeout, spawn

Bots follow the same rules, [[9_bots]]
