---
title: Avatar and movement
date: 2026-09-24
tags: [advanced_player]
---

# Avatar and movement

Every number the avatar moves with: walking, the dash, the hitbox, spawning, and how a level can scale them

This page is the source of truth for the avatar. The game and both bots are built to match these numbers, and in the SDK they are the constants of `AvatarRules`. Code that disagrees with this page is a bug in the code

Distances are in world units. The default camera is exactly 10 units tall (`ValueRules.DefaultZoom`), so a unit is a tenth of the screen's height and the avatar's body is half a unit across.
Zooming the camera changes how much you see, not the numbers below

## The numbers

| What | Value | In plain terms |
|---|---|---|
| Walking speed | `15` u/s | crosses the screen top to bottom in two thirds of a second |
| Dash speed | `50` u/s | 3.3 times the walk |
| Dash duration | `0.15` s | |
| Dash reach | `7.5` u | speed × duration, three quarters of the screen's height |
| Dash cooldown | `0.3` s | counted from the start of the dash |
| Dash invulnerability | `0.3` s | also from the start, so it outlasts the movement by 0.15 s |
| Shortest dash | `0.5` u | one avatar body. Nearer than that, there is no dash |
| Knockback speed | `50` u/s | 3.3 times the walk, [[7_damage]] |
| Knockback duration | `0.2` s | no steering during it |
| Damage timeout | `1.0` s | every further hit inside it is ignored |
| Body size | `0.5` u | the drawn square |
| Hitbox | radius `0.15` u | 0.3 of the body, smaller than what you see on purpose |
| Spawn and despawn | `0.3` s | grows in, shrinks to a point |
| Player size affects speed | fully, `1.0` | a bigger avatar moves proportionally faster. This is the level's Player Size track, not the camera's zoom |
| Heading turn rate | `30` /s | cosmetic: which way the body faces |
| Arrival distance | `0.01` u | nearer than this to your cursor counts as standing on it |

Derived from them, and these are the numbers that actually decide a dodge:

| What | Value |
|---|---|
| Shortest dash: distance | `0.5` u |
| Shortest dash: duration | `0.01` s |
| Shortest dash: cooldown and invulnerability | `0.02` s each |
| Fastest possible dashing | every third frame at 60 fps, 20 per second |
| Knockback distance | `10` u |

What happens on a hit - [[7_damage]]

## Moving

You steer in one of two ways, and the game never mixes them:
- **A direction**: WASD, a gamepad stick, the gyro. The avatar moves the way you push, at walking speed. A stick pushed halfway moves at half speed, and that is the only "walk slowly" there is
- **A cursor**: the mouse or a finger. The avatar chases the point, it does not teleport to it. It moves at its own walking speed and lags behind a fast mouse

Movement is instant in both: no acceleration, no slide, no momentum. You stop on the same frame you stop moving

## The dash

Invulnerability lasts 0.15 s longer than the movement. This landing grace is what lets you dash *through* an obstacle

You steer during a dash. The dash goes where you are asking to go, the direction you hold or the point you aim at, and you may change it mid-dash. A dash with no direction held moves nothing

With a cursor, the dash goes where you point and stops there:

| Cursor distance | What happens |
|---|---|
| further than 7.5 u | a full dash towards it. You stop short of the cursor |
| 0.5 to 7.5 u | a shorter dash that ends exactly on the cursor |
| nearer than 0.5 u | no dash |

A shorter dash is the same dash scaled down. Travel, invulnerability and cooldown shrink together: a half-length dash is invulnerable for half as long and comes back in half the time. It is never a cheaper dash. Two half dashes cost exactly what one full dash costs and cover the same ground

A refused dash costs nothing: no cooldown starts and nothing is spent. A direction player holding nothing gets the same answer, no dash

### Two styles, one budget

- In `Direction` mode a dash always goes the full 7.5 u. Reliable reach, no aiming, but no way to stop partway
- With a cursor you choose the length and can stop exactly on a point. A short dash means shorter protection and one more vulnerable frame per dash. Pointing far away gives you the full dash back

Down a straight line both cover the same ground in the same time. Neither style is stronger: one gives precision, the other simplicity

### Dashing over and over

**Holding dash is not invulnerability.** Cooldown and protection are the same length, so holding the button gives an unbroken chain of dashes. But between two dashes there is always exactly one frame where you can be hit, at any framerate, on a slow phone as much as on a fast PC.
The tightest chain is a dash every third frame at 60 fps

## The hitbox

The ring of dots on the avatar sits exactly on the hitbox. A bullet clipped your outline and did nothing? That is intended

While you are invulnerable (dashing, or just hit) the hitbox is not there at all

The same ring shows your lives: a lit dot is a life in hand

`Settings` → `Interface` → `Hitbox Ring Opacity` sets how visible the ring is. `0` hides it, but levels are balanced for someone who can see it

The body is a grid of 25 squares, 5 by 5. As you lose health, it loses squares from the rim inwards.
With `Graphics` → `Shatter Effect` off, the body is one square that fades instead. This is for weaker devices

## Arriving and leaving

The avatar takes `0.3` s to grow into a level and `0.3` s to compress to a point when it dies. It answers no input during either, and it cannot be hit while arriving

## Scaling

A level can animate the avatar's size and speed through its own tracks. It can also take your controls away or switch collision off for a while

- Walk, dash and knockback speeds are multiplied by the same number. So half speed also halves the dash reach (3.75 u)
- A bigger avatar moves proportionally faster, because its dodges grew too. Size here is the avatar's own size from the level's Player Size track. The camera's zoom changes no speed, no distance and no window: the avatar covers 15 units a second whatever the camera does
- The hitbox is a fraction of the drawn body, so it grows and shrinks with the avatar
- Dash aiming uses the current reach, not the 7.5 from the table. On a level that halved your speed, a cursor 3.75 u away already asks for a full dash, and the 0.5 u floor becomes 0.25 u, because the dash under it is half as long too
- Windows in seconds are not scaled: cooldown, invulnerability, damage timeout, spawn. Only the dash's own length scales its own two windows

Bots follow the same rules, [[9_bots]]
