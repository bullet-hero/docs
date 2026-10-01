---
title: Keyframes and easing
date: 2026-10-01
tags: [level_author]
---

# Keyframes and easing

A key is a value on one frame of one track, plus the easing it is reached with. Everything in a level that moves, changes colour or switches on and off is a list of keys

The basic ideas - [[3_how-the-editor-thinks]]. Every field of the keyframe inspector - [[5_object-properties]]

## What can be animated

Every track has its own keys, independent of the others:

| Owner | Tracks |
|---|---|
| any object | position, rotation, scale, size, anchors, pivot |
| shape | colour, UV |
| text | colour, font size, how much of the text is written, how much of it is hidden |
| camera | position, rotation, zoom, pivot, shake |
| level | background, theme, screen limit, each of the 12 post-processing effects |
| player | size, speed, visibility, control, collision |

An object's keys are counted from the start of its span. So moving the object in time carries its whole animation along

Position is set relative to the parent. A key stores the value itself, not an increment over the previous key

The player's visibility, control and collision are either on or off. Those keys have no easing: there is nothing to blend

## Advice

- Key only what moves. A track with no keys takes the default value
- For a change exactly on a beat, use `Constant`, for example a theme switch on the drop
- Rotation does not wrap: a key at 0 degrees and a key at 720 spin the object twice

## Between two keys

Before the first key and after the last one the value holds still.
Between two keys the game takes the share of time that has passed, runs it through the easing and blends the two values

The share is counted in time, not in drawn frames. So the curve is the same at 30 and at 144 fps

**The easing belongs to the later key of the pair.** A key's easing sets the stretch that arrives at this key from the previous one.
So the easing of the first key on a track never shows. A new key gets `Linear`

The `Easing` field opens the `Select Ease` window, where every easing is drawn as its own curve.
You can select several keys, even on different tracks, and change them in one undo step

## 29 easings

`Linear` is a straight line. `Constant` holds the previous value and jumps on the key

The other 27 are nine families of three: `In`, `Out` and `InOut`. For example, `InSine`, `OutSine`, `InOutSine`

| Family | Shape |
|---|---|
| `Sine` | the softest curve |
| `Quad`, `Cubic`, `Quart`, `Quint` | powers 2, 3, 4 and 5 |
| `Expo` | exponential |
| `Circ` | a quarter of a circle |
| `Back` | goes past the range and comes back |
| `Elastic` | oscillates around the value |

`In` starts slowly and finishes fast. `Out` starts fast and settles. `InOut` is slow at both ends.
From `Sine` to `Expo` each family is sharper than the one before

> [!caution] Caution
> `Back` and `Elastic` leave the range: `Out` overshoots the target, `In` backs up past the start. The collider moves with the object. So a projectile told to stop at the edge of a safe zone enters it for a few frames

## Random values

A value in a key does not have to be a single number:
- a number: `Value`, `Rnd Min-Max`, `Rnd Min-Max, Step`
- a vector (position, scale and the like): `Value`, `Rnd in Rect`, `Rnd in Rect, Step`, `Rnd in Circle`, `Rnd A to B`, `Rnd A to B, Step`
- a colour: `Value`, `Theme`, `Rnd Min-Max`, `Rnd A to B`

`Rnd in Rect` picks each axis separately. `Rnd A to B` picks one number for all axes, so the point lands on the line between A and B.
After that the key is blended like any other

The same seed gives the same level. The random number is computed from the seed, the key's frame, the layer, the object's start frame, the track and the channel. More - [[8_determinism]]

Next: [[2_rhythm-and-structure|Rhythm and structure]], [[6_themes|Themes]]
