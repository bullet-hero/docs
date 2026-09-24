---
title: Object properties
date: 2026-09-24
tags: [level_author]
---

# Object properties

The object and keyframe inspectors and every property they show

## Object inspector

Shows the selected object's own fields. Every type has the shared rect fields. Shape, Effect, Text and Prefab objects add their own below them

`Active` turns off both rendering *and* collision. Children inherit it. An object hidden here cannot kill the player

> [!caution] Caution
> `Layer` is relative to the parent, never absolute. Beside it is the global layer, read-only. That is what the renderer uses: your layer plus every ancestor's

> [!tip] Tip
> Editing a field on an object from a prefab records a **per-instance override**. The checkbox beside it shows the override and reverts it

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Keyframe inspector

Shows the selected keyframes. **Every track the selection touches is shown at once**, not just the last one you clicked.
A selection can hold position and rotation keys, keys of several objects, and object, audio and event keys together

> [!tip] Tip
> The `Ease` picker works across all tracks and takes a **single undo step**. A selection of position and rotation keys changes in one operation, not two

> [!info] Worth knowing
> The `Frame` field is locked while several keys are selected. A frame is unique on a track. One number for many keys would collapse them into one and silently drop the rest. To move several keys at once, drag them on the timeline

A blank value means the selected keys **disagree** on it

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Span

Sets when the object exists. The range is half-open: the start frame is in, the end frame is not.
An object ending at 20 and one starting at 20 never both draw on that frame

> [!info] Worth knowing
> **A child's span must lie inside its parent's. That is resolved on read, never stored.** Shrink a parent and its children are clipped, but what you authored here does not change. Grow it back and everything returns. A root object running past the end of the level is valid data - it simply never plays

> [!info] Worth knowing
> **Anchors** mean "this edge follows the parent's edge". They are authoring intent only. They change nothing at playback

More: [[4_frames-and-time|Frames, time and the length of a level]]

## Easing

Sets how the value arrives at this keyframe from the previous one

> [!info] Worth knowing
> Easing belongs to the **incoming** side of a keyframe. It shapes the stretch from the previous key to this one, and that is how playback reads it. So on the first keyframe of a track the easing has no effect. The in-game hint says the opposite. Trust playback

> [!tip] Tip
> With several keyframes selected, the choice applies to all of them as a **single undo step**. That holds even across different tracks and different objects. A blank choice means the selected keyframes disagree

More: [[5_keyframes-and-easing]]

## Layer

Sets draw order **relative to the parent**, not absolute

> [!caution] Caution
> The renderer uses this number plus every ancestor's. The sum is shown read-only in the `Global` field below. So the same layer means different things under different parents. Reparenting changes where an object draws

> [!info] Worth knowing
> The layer also feeds randomness. A random value is tied to the effective layer, so moving an object in the hierarchy rerolls its numbers. Two objects with the same effective layer AND the same start frame get the same numbers

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Shape

Sets what this object **draws**

> [!info] Worth knowing
> A shape is real geometry, not a picture. It is fitted to its box and measures exactly 1 across its longer axis. So the object's rect is exactly what appears on screen

> [!info] Worth knowing
> The game generates around 500 shapes along four axes: form, sector, thickness and invert. A level can add its own. An empty value is valid: an object that draws nothing but has a hitbox is an invisible wall

More: [[1_readability-and-fairness|Readability and fairness]]

## Collider

Sets what this object **hits**. It is a separate choice and does not depend on what the object draws

> [!info] Worth knowing
> Neither derives from the other, on purpose. A harmless warning beam, a hitbox simpler than its art and an invisible wall are ordinary content, not tricks

> [!tip] Tip
> Both fields pick from the same two collections. A shape the level authored works for either or both

More: [[1_readability-and-fairness|Readability and fairness]]

## Shader Type

Sets which render path this object takes

> [!caution] Caution
> `Auto` decides once, when the level loads. The rule is strict: the level's look must not change. Anything that cannot be proven opaque becomes transparent. Geometry is not considered, only alpha

> [!tip] Tip
> The label beside this field shows what `Auto` actually resolved to. It is read straight from the renderer's data, not worked out again. That way the label cannot disagree with what is on screen

More: [[1_level-budget|The level's budget]]

## Resolved values

Shows what the selected objects **are** on the current frame, not what you authored onto them. Every number is read from the running simulation. So it matches what you see in the viewport

The square at the end of a row is that field's keyframe state:
- blue - a keyframe sits on this frame. Clicking the square selects it
- amber - the frame lies between two keys, the value is interpolated
- grey - the track has keys, but this frame is outside them. The value is held
- hollow - the track is empty, the field takes the engine default

The arrows move the playhead to the previous or the next keyframe of that track

A UV row reads as two pairs: tiling first, then offset

Below the rule sit the composed values: the summed layer, the inherited Active flag and the parent-composed transform. No keyframe sets them, so they carry no indicator

> [!info] Worth knowing
> An empty keyframe track is valid data, not missing data. It means the object uses the default for that field

> [!caution] Caution
> Inside Prefab Mode a template plays no frames of its own, so the values show as dashes. The keyframe indicators still work there: they read the level file, not the simulation
