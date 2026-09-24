---
title: Avatar and movement
date: 2026-09-24
tags: [advanced_player]
---

# Avatar and movement

Every number the avatar moves with: walking, the dash, the hitbox, spawning, and how a level can scale them

Distances are in world units. The default camera is exactly 10 units tall, so a unit is a tenth of the screen's height. Zooming the camera changes how much you see, not any number below

## The numbers

| What | Value | In plain terms |
|---|---|---|
| Walking speed | `15` u/s | crosses the screen top to bottom in two thirds of a second |
| Dash speed | `50` u/s | 3.3 times the walk |
| Dash duration | `0.15` s | |
| Dash reach | `7.5` u | three quarters of the screen's height |
| Dash cooldown | `0.3` s | counted from the moment the dash starts |
| Dash invulnerability | `0.3` s | also from the start, so it outlasts the travel by 0.15 s |
| Shortest dash | `0.5` u | one avatar body. Nearer than that, the dash is refused |
| Body size | `0.5` u | the drawn square |
| Hitbox | radius `0.15` u | 0.3 of the body, smaller than what you see on purpose |
| Spawn and despawn | `0.3` s | growing in, compressing to a point |

Movement is instant: no acceleration, no slide, no momentum. You stop on the frame you stop asking to move. Hits are covered on the [[7_damage]] page

## The dash

The 0.15 s of protection that outlasts the movement is a landing grace, and it is what makes dashing *through* something solid work. You steer during a dash, and a dash with nothing held moves nothing

With a cursor, the dash goes where you point:

| Cursor distance | What happens |
|---|---|
| further than 7.5 u | a full dash towards it |
| 0.5 to 7.5 u | a shorter dash that ends exactly on the cursor |
| nearer than 0.5 u | no dash. The press costs nothing |

A shorter dash is the same dash scaled down: travel, invulnerability and cooldown all shrink together, so two half dashes cost exactly what one full dash costs. A `Direction` player always dashes the full 7.5 u. Neither style is stronger: one buys precision, the other simplicity

**Holding dash is not invulnerability.** Cooldown and protection are the same length, so dashes can chain, and between two of them there is always exactly one frame where you can be hit, at any framerate. The fastest possible chain is a dash every third frame at 60 fps

## The hitbox

The ring of dots on the avatar sits exactly on the hitbox, so you can see where it really is. A bullet that visibly clips your outline and does nothing is the game working as intended. The same ring counts lives: a lit dot is a life in hand. `Settings`, `Interface`, `Hitbox Ring Opacity` sets its visibility, and `0` hides it (levels are balanced for someone who can see it)

The body is a grid of 64 squares that loses squares from the rim inwards as you lose health. `Graphics`, `Shatter Effect` off makes it one square that fades instead, for a weaker device

## Scaling

A level can animate the avatar's size and speed through its own tracks, and can also take your controls away or switch collision off for a while

- Walk, dash and knockback speeds are multiplied by the same number, so half speed also halves the dash reach (3.75 u)
- A bigger avatar moves proportionally faster, because its dodges grew with it. The hitbox scales with the body
- The dash aiming rules use the current reach, not the printed 7.5
- Windows measured in seconds (cooldown, invulnerability, damage timeout, spawn) are not scaled

The same rules bind the bots, see [[9_bots]]
