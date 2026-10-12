---
title: Keyframes and easing
date: 2026-10-12
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
| text | colour, font size, `{{ui:editor_dummy_text-11}}` (how much of the text is written), `{{ui:editor_dummy_text-12}}` (how much of it is hidden behind the mask) |
| camera | position, rotation, zoom, pivot, shake |
| level | background, theme, screen limit, each of the 12 post-processing effects |
| player | size, speed, visibility, control, collision |

A shape's colour key can also be a gradient over the object's rect. Its `{{ui:editor_keyframe-color_layout}}` field picks the layout: `{{ui:enum_color4-x4-key-type_value}}` (one colour), `{{ui:enum_color4-x4-key-type_vertical}}` (bottom to top), `{{ui:enum_color4-x4-key-type_horizontal}}` (left to right) or `{{ui:enum_color4-x4-key-type_bari-centrical}}` (a colour in each corner)

A font size key is either one number, a fixed size in world units, or a band with `{{ui:field_common_auto-size}}` on. The text is drawn at the band's `{{ui:field_common_max}}` and shrinks toward its `{{ui:field_common_min}}` until it fits its rect

An object's keys are counted from the start of its span. So moving the object in time carries its whole animation along

Position is set relative to the parent. A key stores the value itself, not an increment over the previous key

The player's visibility, control and collision are either on or off. Those keys have no easing: there is nothing to blend

The first key on an empty player track changes nothing on screen: visibility, control and collision start on, size and speed start at the player's usual values. With control off, or the player hidden, the player cannot be steered: the cursor disappears and a press is not picked up. A hidden player is still hit: only collision decides that

## Text: fill and appearing

Two text tracks hide characters in different ways. Both take a share from 0 to 1 and count the characters of the text

**`{{ui:editor_dummy_text-11}}`** is the share of the text that is written: 0 - nothing, 1 - all of it. A character that is not written is not drawn at all, so the line gets shorter. An empty track writes the whole text. Each key sets the direction:
- `{{ui:enum_text-fill-direction_forward}}` (the default) - from the first character, like a typewriter
- `{{ui:enum_text-fill-direction_backward}}` - from the last character
- `{{ui:enum_text-fill-direction_from-center}}` - grows out of the middle
- `{{ui:enum_text-fill-direction_to-center}}` - grows in from both ends and meets in the middle

**`{{ui:editor_dummy_text-12}}`** is the share of the characters hidden behind the mask: 0 - all shown, 1 - all masked. A hidden character keeps its place and is drawn as a mask character, `{{v:text.appearing-mask-default}}` by default. The mask is the text object's `{{ui:editor_inspector-appearing_mask}}` field, and with several characters in it each hidden character takes one of them. An empty track hides nothing. Each key sets the mode:
- `{{ui:enum_text-appearing-mode_random}}` (the default) - scattered, but the same scatter on every run. A character hidden at 0.3 is still hidden at 0.6, so the text resolves instead of flickering
- `{{ui:enum_text-appearing-mode_forward}}` - the hidden characters are at the end, the text appears from its start
- `{{ui:enum_text-appearing-mode_backward}}` - the hidden characters are at the start

To type a line in, animate `{{ui:editor_dummy_text-11}}` from 0 to 1. To decode it out of noise, animate `{{ui:editor_dummy_text-12}}` from 1 to 0

## Advice

- Key only what moves. A track with no keys takes the default value
- For a change exactly on a beat, use `Constant`, for example a theme switch on the drop
- Rotation does not wrap: a key at 0 degrees and a key at 720 spin the object twice. In radians, as the file and the AI assistant write it, that is 0 and 12.566

## Between two keys

Before the first key and after the last one the value holds still.
Between two keys the game takes the share of time that has passed, runs it through the easing and blends the two values

The share is counted in time, not in drawn frames. So the curve is the same at 30 and at 144 fps

**The easing belongs to the later key of the pair.** A key's easing sets the stretch that arrives at this key from the previous one.
So the easing of the first key on a track never shows. A new key gets `Linear`

The `{{ui:hint_editor_inspector_ease_header}}` field opens the `{{ui:editor_search-title_ease}}` window, where every easing is drawn as its own curve.
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
- a number: `{{ui:field_common_value}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_float-type_random-min-max-step}}`
- a vector (position, scale and the like): `{{ui:field_common_value}}`, `{{ui:enum_vector-type_random-rect}}`, `{{ui:enum_vector-type_random-rect-step}}`, `{{ui:enum_vector-type_random-circle}}`, `{{ui:enum_color-type_random-lerp}}`, `{{ui:enum_vector-type_random-lerp-step}}`
- a colour: `{{ui:field_common_value}}`, `{{ui:editor_events-timeline_track_theme}}`, `{{ui:enum_color-type_random-min-max}}`, `{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}` picks each axis separately. `{{ui:enum_color-type_random-lerp}}` picks one number for all axes, so the point lands on the line between A and B.
The forms with a step round the result down to a multiple of the step. A step of 0 turns the grid off, and the value behaves like the form without a step.
After that the key is blended like any other

The same seed gives the same level. The random number is computed from the seed, the key's frame, the layer, the object's start frame, the track and the channel. More - [[8_determinism]]

Next: [[2_rhythm-and-structure|Rhythm and structure]], [[6_themes|Themes]]
