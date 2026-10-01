---
title: Object properties
date: 2026-10-01
tags: [level_author]
---

# Object properties

The object inspector edits the selected object's fields, the keyframe inspector edits the selected keyframes, on every track the selection touches at once

## Object inspector

Shows the selected object's fields. Every type has the shared fields of a rect. Shape, Effect, Text and Prefab add their own below

`Active` turns off both rendering *and* collision. Children inherit it. An object hidden here cannot kill the player

> [!caution] Caution
> `Layer` is set relative to the parent, not absolutely. Beside it is the global layer, read-only. That is the one the renderer uses: your layer plus the layers of all ancestors

> [!tip] Tip
> Editing a field on an object from a prefab records an **instance override**. The checkbox beside it shows the override and reverts it

The parent button shows what the object hangs off, `No Parent` included. It opens the `Select Parent` window: every object of the scope, with fixed options on top:
- in the level - `No Parent` and `Camera`. `Camera` is the level's camera, and its child moves with it
- inside a prefab template - one `Prefab Root` row. It means both "no parent" and the template's root: there they are the same thing. The camera and the player cannot be parents inside a template

A reserved parent is shown with its id: `Camera (-1)`, `Local Player (-2)`, `Prefab Root (-3)`

The button beside it selects the parent. On an object at a template's top level it selects the template's root. It is unavailable when several objects are selected and when there is nothing to select: no parent, or the parent is the camera or the player

A right-panel tab with nothing to show is hidden. If the open tab empties, the panel switches to the first tab that has something. If every tab is empty, the panel reads `No inspectors`

More: [[3_how-the-editor-thinks|How the editor works]]

## Keyframe inspector

Shows the selected keyframes. **Every track the selection touches is visible at once**, not only the last one you clicked.
A selection can hold position and rotation keyframes, keyframes of different objects, and object, audio and event keyframes together

> [!tip] Tip
> The `Ease` choice acts on all tracks at once and takes **one undo step**. A selection of position and rotation changes in one operation, not two

> [!info] Worth knowing
> The `Frame` field is locked when several keyframes are selected. On one track a frame is unique. One number for all keyframes would collapse them into one and silently delete the rest. To move several keyframes at once, drag them on the timeline

A blank value means the selected keyframes **differ** in it

More: [[3_how-the-editor-thinks|How the editor works]]

## Span

Sets when the object exists. The range is half-open: the start frame is in it, the end frame is not.
An object that ends at 20 and an object that starts at 20 never both draw on that frame

> [!info] Worth knowing
> **A child's span must lie inside its parent's. That is resolved on read and never stored.** Shrink the parent and the children are clipped, but what is written here does not change. Stretch it back and everything returns. A root object past the end of the level is valid data, it simply does not play

> [!info] Worth knowing
> **Anchors** mean "this edge follows the parent's edge", and they decide what plays. An anchored edge sits on the parent's edge, so an anchored child stretches along with a growing parent. Its animation keeps the authored timing

A prefab placement's length comes from the template by default, but it can be typed in like any other. A different value records an override of this placement. The checkbox beside the span shows it and brings back the template's length

A prefab template's root has no span block. In its place is a `Frame Length` row: the length of the whole template, the same value as `Frame Length` on the `Prefab` tab. The root's `Active` and `Layer` are read-only, and the root cannot be deleted or given a parent

More: [[4_frames-and-time|Frames, time and the length of a level]]

## Easing

Sets how the value arrives at this keyframe from the previous one

> [!info] Worth knowing
> Easing belongs to the **incoming** side of a keyframe. It sets the stretch from the previous keyframe to this one, and that is exactly how playback reads it. So on the first keyframe of a track easing has no effect

> [!tip] Tip
> If several keyframes are selected, the choice applies to all of them at once in **one undo step**. Even if the keyframes are on different tracks and belong to different objects. A blank choice means the selected keyframes differ

More: [[5_keyframes-and-easing]]

## Layer

Sets draw order **relative to the parent**, not absolutely

> [!caution] Caution
> The renderer uses this number plus the layers of all ancestors. The sum is shown read-only in the `Global` field below. So the same layer means different things under different parents. Changing the parent changes where the object draws

> [!info] Worth knowing
> The layer also takes part in randomness. A random value is tied to the resulting layer, so moving an object in the hierarchy changes the numbers it rolled. Two objects with the same resulting layer AND the same start frame get the same numbers

More: [[3_how-the-editor-thinks|How the editor works]]

## Shape

Sets what the object **draws**

> [!info] Worth knowing
> A shape is real geometry, not a picture. It is fitted into its box, and its long side equals exactly 1. So the object's box is exactly what is seen on screen

> [!info] Worth knowing
> The game generates around 500 shapes along four axes: form, sector, thickness and inversion. A level can add its own. An empty value is valid: an object with no picture but with a hitbox is an invisible wall

More: [[1_readability-and-fairness|Readability and fairness]]

## Collider

Sets what the object **hits** with. It is a separate choice and does not depend on what the object draws

> [!info] Worth knowing
> One is not derived from the other on purpose. A harmless warning beam, a hitbox simpler than the picture and an invisible wall are ordinary content, not tricks

> [!tip] Tip
> Both fields pick from the same two collections. A shape the level created works for either one

In the hitbox display modes an object with no collider draws nothing, and neither does an inactive object. That is how decoration differs from danger. How they are drawn is set in [[14_editor-settings]]

More: [[1_readability-and-fairness|Readability and fairness]]

## Shader type

Sets which path the object is rendered by

> [!caution] Caution
> `Auto` decides once, when the level loads. The rule is strict: the level's look must not change. Anything that cannot be proven opaque becomes transparent. Geometry is not considered, only alpha

> [!tip] Tip
> The label beside it shows what `Auto` actually resolved to. It is read straight from the render data, not calculated again. That way the label cannot disagree with what is on screen

More: [[1_level-budget|The level's budget]]

## Current values

Shows what the selected objects **are** on the current frame, not what you wrote into them. Every number is read from the running simulation. So it matches what is seen in the viewport

The square at the end of a row is the keyframe state of that field:
- blue - a keyframe sits on this frame. Clicking the square selects it
- amber - the frame is between two keyframes, the value is interpolated
- grey - the track has keyframes, but the frame is outside them. The value is held
- hollow - the track is empty, the field takes the engine's default value

The arrows move the playhead to the previous or next keyframe of that track

A UV row reads as two pairs: tiling first, then offset

Below the line come the composed values: the summed layer, the inherited activity and the transform with parents taken into account. No keyframe sets them, so they have no indicator

> [!info] Worth knowing
> An empty keyframe track is valid data, not missing data. It means the object uses the default value for that field

> [!info] Worth knowing
> In Prefab Mode this section is hidden. A template does not play its own frames, so there is nothing to show on a frame
