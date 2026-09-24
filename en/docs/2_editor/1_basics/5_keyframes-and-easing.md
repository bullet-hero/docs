---
title: Keyframes and easing
date: 2026-09-25
tags: [level_author]
---

# Keyframes and easing

What a keyframe stores, which properties can be animated, how a value travels between two keys, and the 29 easings the game has

A keyframe is a value on one frame of one track, plus the easing that value is reached with. Everything in a level that moves, changes colour or switches on and off is a list of such keys. The ideas underneath (object, frame, span, key) are in [[3_how-the-editor-thinks]], and every field of the keyframe inspector is in [[5_object-properties]]

## What can be keyframed

Every track has its own keys, independent of the others:

| Owner | Tracks |
|---|---|
| any object | position, rotation, scale, size, anchors, pivot |
| shape | colour, UV |
| text | colour, font size, how much of the text is written, how much of it is hidden |
| camera | position, rotation, zoom, pivot, shake |
| level | background, theme, screen limit, each of the 12 post-processing effects |
| player | size, speed, visibility, control, collision |

An object's keys are counted from the start of its span, so moving the object in time carries its whole animation along. Position is local to the parent. A key stores the value itself, never an offset from the previous key

The player's visibility, control and collision are on or off. Those keys carry no easing, because there is nothing between on and off to blend

## Between two keys

Before the first key and after the last one the value is held. Between two keys the game takes the share of time that has passed, runs it through the easing and blends the two values by the result. The share is counted in time rather than in drawn frames, so the curve is the same at 30 and at 144 fps

**The easing belongs to the later key of the pair.** The easing stored on a key shapes the stretch that arrives at it from the previous key, which is what playback reads. The easing of the first key on a track therefore never shows. A new key gets `Linear`

> [!warning] Warning
> At the time of writing the in-game hint on the Easing field says the opposite, that a key's easing shapes the stretch after it. If the two disagree for you, trust playback: scrub between the keys and watch

The Easing field opens `Select Ease`, where every easing is drawn as its own curve. Several selected keys, even on different tracks, change in one undo step

## The 29 easings

`Linear` is a straight line. `Constant` holds the previous value and jumps on the key. The other 27 come in nine families of three, `In`, `Out` and `InOut`, for example `InSine`, `OutSine`, `InOutSine`:

| Family | Shape |
|---|---|
| `Sine` | the softest curve |
| `Quad`, `Cubic`, `Quart`, `Quint` | powers 2, 3, 4 and 5 |
| `Expo` | exponential |
| `Circ` | a quarter of a circle |
| `Back` | steps past the range and returns |
| `Elastic` | oscillates around the value |

`In` starts slowly and finishes fast, `Out` starts fast and settles, `InOut` is slow at both ends. From Sine to Expo each family is sharper than the one before it

> [!caution] Caution
> `Back` and `Elastic` leave the range between the two values: `Out` overshoots the target, `In` swings back past the start. On a position that moves the collider as well, so a projectile keyed to stop at the edge of a safe zone crosses into it for a few frames

## Random values

A value in a key does not have to be a fixed number:
- a number: `Value`, `Rnd Min-Max`, `Rnd Min-Max, Step`
- a vector (position, scale and the like): `Value`, `Rnd in Rect`, `Rnd in Rect, Step`, `Rnd in Circle`, `Rnd A to B`, `Rnd A to B, Step`
- a colour: `Value`, `Theme`, `Rnd Min-Max`, `Rnd A to B`

`Rnd in Rect` draws each axis separately. `Rnd A to B` draws one number for all of them, so the point lands on the line between A and B. The number is computed from the seed, the key's frame, the layer, the object's start frame, the track and the channel, so the same seed gives the same level (see [[8_determinism]]). After that the key is blended like any other

## Practical advice

- Key only what moves. A track with no keys uses the default value
- Use `Constant` for a change that must land exactly on a beat, a theme switch on the drop for example
- Rotation is not wrapped: a key at 0 degrees and one at 720 spin the object twice

Next: [[2_rhythm-and-structure|Rhythm and structure]], [[6_themes|Themes]]
