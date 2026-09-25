---
title: Timelines
date: 2026-09-24
tags: [level_author]
---

# Timelines

Every timeline of the editor and the beat grid, one section per panel

## Level timeline

Shows every object of the level over time. Each object is one clip. The lane a clip sits in is the object's **layer**

A clip is a half-open **span**. An object covering frames 10-19 ends exactly where one starting at 20 begins. The two never both draw on the shared frame

> [!info] Worth knowing
> A child's span must lie inside its parent's. That is **resolved on read, never stored**. Shrink a parent and its children are clipped, but their values do not change. Grow it back and everything returns. A root object running past the end of the level is valid data - it simply never plays

> [!tip] Tip
> The three tools live in the button strip: `Selection` picks and drags, `Edges` reshapes an edge, `Scissors` splits a clip at the cursor. Right-click *empty space* to open the menu. A press on a clip starts a drag

A prefab placement and the objects it brings are drawn in the prefab tint

How the tools treat a placement:
- Its length is its template's by default. Setting a different length on one placement records an override for that placement only
- Dragging its start edge with `Edges` also moves where it starts reading the template. So the picture inside it stays where it was
- `Scissors` cuts it into two placements of the same template, each playing its own part. The template itself is not edited
- The objects a placement brings cannot be cut. Cut the placement, or cut those objects in Prefab Mode

More: [[3_how-the-editor-thinks|How the editor thinks]], [[4_composition-and-camera|Composition and the camera]]

## Local timeline

Shows the keyframes of the **selected object**. Each animatable property has its own lane: position, rotation, scale, size, anchors, pivot, colour, UV, font size

Frames here count **from the start of the object's span**. Move the object and its whole animation moves with it

> [!info] Worth knowing
> An **empty track is valid data**, not missing data. A track with no keyframes uses the default value. That is why a new object animates nothing until you add a key

Values blend between neighbouring keyframes only. The span decides which frames exist, never how values blend

On an object that comes from a prefab, a track that still matches its template is drawn in the prefab tint. Add, move or edit a keyframe on it and the tint goes: the track now holds an override

In Prefab Mode, with the template's root selected, this timeline is as long as the whole template

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Prefab timeline

Prefab Mode's own timeline. Shows the **template's** objects

> [!info] Worth knowing
> Its length is the template's own length, not the span of one of its placements. A template is edited as a small self-contained level. It can be placed many times, at different times

One row is the template's **root**, and it spans the whole template. Every other object of the template hangs off it:
- the root row can be selected. The inspector and the Local timeline then show the root
- it cannot be dragged, resized or cut
- it folds like any parent. Folding it hides the whole template on this timeline

> [!warning] Warning
> The selection is not shared with the rest of the editor. There is no live preview of a specific placement. Edits change the template and spread to every placement that references it

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Audio timeline

Shows the level's audio tracks with their waveforms. They make it easy to line content up with what you hear

> [!tip] Tip
> `Fit Track` in the inspector resizes a track to its clip's real length. The button is disabled without a clip, or at speed 0: a frozen track has no length

> [!caution] Caution
> The inspector's `Volume` slider is the track's fader. The keyframed volume is a separate Volume track on the Local timeline. The two multiply at playback

More: [[2_preparing-the-track|Preparing the track]]

## Events timeline

Shows level-wide keyframes that belong to no object:
- camera position, rotation, zoom, pivot and shake
- markers and checkpoints
- the screen limit
- background and theme
- every post-processing effect
- the player's visibility, control, collision, size and speed

> [!info] Worth knowing
> The **Beat** lane is the exception here. Its items carry a span, and it is the only lane `Edges` and `Scissors` act on

> [!tip] Tip
> A colour can reference the level's theme instead of holding a fixed value. Then changing the theme recolours everything that points at it at once

More: [[4_composition-and-camera|Composition and the camera]], [[6_themes]]

## Beat grid

Helps you place content on the music. Generators act on the same beats you see

It is authoring metadata, not a game mechanic. **Playback does not read the grid**

The grid is a list of **segments**. Each has a constant tempo: BPM, phase offset, beats per bar.
Segments never overlap. The gaps are useful: an intro with no percussion, a break, the tail after the song. A single tempo track could not express them

> [!tip] Tip
> `TAP` records taps at the playhead. `Create from taps` turns them into one segment from the first tap to the last. Beats are always counted from the segment's start and never accumulated, so the error stays under half a frame

More: [[2_rhythm-and-structure|Rhythm and structure]]

## Beat segment

One stretch of constant tempo: BPM, phase offset in fractional frames, beats per bar, a name and a colour

Exactly one segment is shown even when several are selected. Every field but the name is unique to one segment. Editing them together would collapse them onto each other

> [!caution] Caution
> A segment is identified by its start frame. So **moving it changes its identity**. After a move, reselect it at its new start

> [!tip] Tip
> Taps here re-phase the selected segment instead of creating a new one. BPM and offset change in one undo step

More: [[2_rhythm-and-structure|Rhythm and structure]]
