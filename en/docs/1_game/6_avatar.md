---
title: Avatar and movement
date: 2026-10-02
tags: [advanced_player]
---

# Avatar and movement

The avatar walks at {{v:avatar.move-speed}} units per second, and a dash carries it {{v:avatar.dash-distance}} units in {{v:avatar.dash-time}} s. The hitbox is a circle of radius {{v:avatar.hitbox-radius}} units, smaller than the drawn {{v:avatar.body-size}}-unit square

This page is the source of truth for the avatar. The game and both bots are built to these numbers, and the SDK records them as the `AvatarRules` constants. Code that disagrees with this page is a bug in the code

Distances are in world units. The default camera is exactly {{v:camera.default-height}} units tall (`ValueRules.DefaultZoom`), so a unit is a tenth of the screen height, and the avatar's body is half a unit wide.
Camera zoom changes how much you see, but not the numbers below

## The numbers

| What | Value | In plain words |
|---|---|---|
| Walk speed | `{{v:avatar.move-speed}}` u/s | crosses the screen top to bottom in two thirds of a second |
| Dash speed | `{{v:avatar.dash-speed}}` u/s | {{v:avatar.dash-to-walk-ratio}} times faster than walking |
| Dash duration | `{{v:avatar.dash-time}}` s | |
| Dash distance | `{{v:avatar.dash-distance}}` units | speed × duration, three quarters of the screen height |
| Dash cooldown | `{{v:avatar.dash-cooldown}}` s | counted from the start of the dash |
| Dash invulnerability | `{{v:avatar.dash-invulnerability}}` s | also from the start, so it lasts {{v:avatar.dash-invulnerability-margin}} s longer than the movement itself |
| Shortest dash | `{{v:avatar.arrival-distance}}` units | the same as the arrival distance, any closer and you are already standing on the target |
| Knockback speed | `{{v:avatar.knockback-speed}}` u/s | {{v:avatar.knockback-to-walk-ratio}} times faster than walking, [[7_damage]] |
| Knockback duration | `{{v:avatar.knockback-time}}` s | no control during it |
| Damage timeout | `{{v:avatar.damage-timeout}}` s | every further hit inside it is ignored |
| Body size | `{{v:avatar.body-size}}` units | the drawn square |
| Hitbox | radius `{{v:avatar.hitbox-radius}}` units | {{v:avatar.hitbox-scale}} of the body, deliberately smaller than what you see |
| Appearing and disappearing | `{{v:avatar.spawn-time}}` s | grows in and shrinks to a point |
| Effect of player size on speed | full, `{{v:avatar.size-speed-influence}}` | a larger avatar moves proportionally faster. This is the level's player size track, not the camera zoom |
| Turn speed | `{{v:avatar.turn-speed}}` /s | cosmetic: where the body faces |
| Arrival distance | `{{v:avatar.arrival-distance}}` units | closer than this to the cursor counts as standing on it |

Derived from them, and these are what decide a dodge:

| What | Value |
|---|---|
| Shortest dash: distance | `{{v:avatar.arrival-distance}}` units |
| Shortest dash: duration | well under a frame |
| Shortest dash: cooldown and invulnerability | well under a frame, each |
| Most frequent dashes | no more often than every other frame |
| Knockback distance | `{{v:avatar.knockback-distance}}` units |

What happens on a hit - [[7_damage]]

## Moving

You control the avatar in one of two ways, and the game never mixes them:
- **Direction**: WASD, a gamepad stick, the gyroscope. The avatar moves where you push, at walk speed. A stick pushed halfway gives half the speed, and there is no other "slow walk"
- **Cursor**: the mouse or a finger. The avatar chases the point rather than teleporting to it. It moves at its own walk speed and lags behind a fast mouse

Movement is instant in both cases: no acceleration, sliding or inertia. You stop on the same frame you stop moving

## The dash

Invulnerability lasts {{v:avatar.dash-invulnerability-margin}} s longer than the movement. That margin after landing is what lets you dash *through* an obstacle

You steer during a dash. The dash goes where you ask: along the held direction or to the aim point, and it can change mid-dash. A dash with no direction held moves nowhere

With a cursor the dash goes where you point and stops there:

| Distance to the cursor | What happens |
|---|---|
| farther than {{v:avatar.dash-distance}} units | a full dash toward it. You stop short of the cursor |
| from {{v:avatar.arrival-distance}} to {{v:avatar.dash-distance}} units | a shortened dash that ends exactly on the cursor |
| closer than {{v:avatar.arrival-distance}} units | no dash |

A shortened dash is the same dash at a smaller scale. Path, invulnerability and cooldown shrink together: a dash half as long protects half as long and recharges twice as fast. It never comes cheaper. Two half dashes cost exactly as much as one full dash and cover the same distance

A dash that does not happen costs nothing: the cooldown does not start, nothing is spent. A direction player holding nothing gets the same answer - no dash

The body turns a deeper blue while you dash, then returns to its normal colour over the next {{v:avatar.dash-tint-fade}} s. Nothing else changes the body's colour, not even a hit - a dash is your own movement, so only it does

The dash trail and that blue depend on the dash length: a full dash shows them in full, the shortest one at `{{v:avatar.dash-effect-min}}` of that, everything in between proportionally. A short dash throws its particles slower, so the trail looks exactly as long as the dash

### Two styles, one budget

- In `{{ui:field_common_direction}}` mode a dash always goes the full {{v:avatar.dash-distance}} units. A reliable distance with no aiming, but no stopping halfway either
- With a cursor you pick the length and can stop exactly on a point. A short dash means shorter protection and one more vulnerable frame per dash. Point far away and the full dash comes back

In a straight line both cover the same distance in the same time. Neither style is stronger: one gives precision, the other simplicity

### Dashing over and over

**A held dash is not invulnerability.** Cooldown and protection are the same length, so a held button gives a continuous chain of dashes. But between two dashes there is always exactly one frame in which you can be hit, at any frame rate, on a slow phone the same as on a fast PC.
The tightest chain is a dash no more often than every other frame

## The hitbox

The ring of dots on the avatar is drawn exactly along the hitbox. A bullet grazed the outline and did nothing? That is intended

While you are invulnerable (in a dash or right after a hit), there is no hitbox at all

The same ring shows your lives: a lit dot is a life in reserve

The ring's visibility is set by `{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_hitbox-ring-opacity}}`. `0` hides it, but levels are balanced for someone who sees it

The body is a grid of {{v:avatar.grid-cells}} squares, {{v:avatar.grid-side}} by 5. As health is lost, squares from the edge to the centre do not disappear but fade: a lost square stays as a pale ghost, so the grid always shows all {{v:avatar.grid-cells}}, and health reads as the number still lit.
The ghost squares are transparent enough to show the hitbox ring under the body.
At zero health exactly one square is lit - the last one.
Any loss of health is shown over `{{v:avatar.health-loss-time}}` s, any recovery over `{{v:avatar.health-gain-time}}` s, however many lives it is.
If you turn off `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics_avatar-render}}`, the body becomes a single square that fades. This is for weak devices

## Arriving and leaving

The avatar grows into the level over `{{v:avatar.spawn-time}}` s and shrinks to a point over `{{v:avatar.spawn-time}}` s on death. In both cases it does not respond to input, and while appearing it cannot be hit

## Scaling

A level can animate the avatar's size and speed with its own tracks. It can also take control away for a while or turn collisions off

- Walk, dash and knockback speeds are multiplied by one number. So at half speed the dash is also half as long ({{v:avatar.half-speed-dash-distance}} units)
- A larger avatar moves proportionally faster, because its dodges grew too. Size here is the avatar's own size from the player size track. Camera zoom changes neither speed, nor distances, nor windows: the avatar covers {{v:avatar.move-speed}} units per second whatever the camera does
- The hitbox is a fraction of the drawn body, so it grows and shrinks with the avatar
- Dash aiming uses the current distance, not the table's 7.5. On a half-speed level a cursor {{v:avatar.half-speed-dash-distance}} units away already asks for a full dash, and the {{v:avatar.arrival-distance}}-unit threshold becomes {{v:avatar.half-speed-arrival-distance}}, because the dash above it is also half as long
- Windows in seconds do not scale: cooldown, invulnerability, damage timeout, appearing. Only the length of the dash itself scales its two own windows

Bots follow the same rules, [[9_bots]]
