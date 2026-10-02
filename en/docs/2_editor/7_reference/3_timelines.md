---
title: Timelines
date: 2026-10-02
tags: [level_author]
---

# Timelines

Timelines show the level over time: objects, the selected object's keyframes, a prefab's template, audio and events. The beat grid helps you place all of it on the music

## Level timeline

Shows every object of the level over time. Each object is one clip. The lane a clip sits in is the object's **layer**

A clip is a half-open **span**. An object on frames 10-19 ends exactly where an object starting at frame 20 begins. The two never both draw on a shared frame

> [!info] Worth knowing
> A child's span must lie inside its parent's. That is **resolved on read and never stored**. Shrink the parent and the children are clipped, but their values do not change. Stretch it back and everything returns. A root object past the end of the level is valid data, it simply does not play

> [!tip] Tip
> Four tools sit in the button strip: `Selection` selects and moves, `Edges` drags an edge, `Scissors` cut the clip under the cursor, `Marquee` adds every clip a dragged box touches to the selection. The menu opens with a right click on *empty space*. A press on a clip starts a drag

A prefab placement and the objects it brings are drawn in the prefab's colour

How the tools treat a placement:
- Its length comes from the template by default. A different length on one placement is recorded as an override of that placement only
- If you drag its start edge with `Edges`, the place it reads the template from moves along with it. So the picture inside stays where it was
- `Scissors` cut it into two placements of the same template, and each plays its own part. The template itself does not change
- The objects a placement brought cannot be cut. Cut the placement itself, or cut those objects in Prefab Mode

More: [[3_how-the-editor-thinks|How the editor works]], [[4_composition-and-camera|Composition and the camera]]

## Local timeline

Shows the keyframes of the **selected object**. Each animatable property has its own track: position, rotation, scale, size, anchors, pivot, colour, UV, font size

Frames here count **from the start of the object's span**. Move the object and its whole animation moves with it

> [!info] Worth knowing
> **An empty track is valid data**, not a gap. A track with no keyframes takes the default value. That is why a new object animates nothing until you place a keyframe

A value blends only between neighbouring keyframes. The span decides which frames exist, but not how the values blend

On an object from a prefab, a track that still matches the template is drawn in the prefab's colour. Add, move or edit a keyframe on it and the colour goes: the track now holds an override

In Prefab Mode, with the template's root selected, this timeline is as long as the whole template

More: [[3_how-the-editor-thinks|How the editor works]]

## Prefab timeline

Prefab Mode's own timeline. Shows the **template's** objects

> [!info] Worth knowing
> Its length is the template's own length, not the span of one of its placements. A template is edited as a small standalone level. It can be placed many times and at different moments

One row is the template's **root**, and it runs the length of the whole template. Every other object of the template hangs off it:
- the root row can be selected. The inspector and the Local timeline then show the root
- it cannot be dragged, stretched or cut
- it folds like any parent. A folded root hides the whole template on this timeline

> [!warning] Warning
> The selection is not shared with the rest of the editor. There is no live preview of a specific placement. Edits change the template and spread to every placement that references it

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Audio timeline

Shows the level's audio tracks with their waveform. It makes it easy to line content up with what you hear

> [!tip] Tip
> `Fit Track` in the inspector fits the track to the clip's real length. The button is unavailable if there is no clip or the speed is 0: a frozen track has no length

> [!caution] Caution
> The `Volume` slider in the inspector is the track's fader. Keyframed volume is a separate Volume track on the Local timeline. At playback the two multiply

More: [[2_preparing-the-track|Preparing the track]]

## Events timeline

Shows the level's keyframes that belong to no object:
- camera position, rotation, zoom, pivot and shake
- markers and checkpoints
- the screen limit
- background and theme
- every post-processing effect
- the player's visibility, control, collision, size and speed

> [!info] Worth knowing
> The **Beat** track is the exception here. Its items have a span, and it is the only track `Edges` and `Scissors` act on

> [!tip] Tip
> A colour can refer to the level's theme instead of a fixed value. Then changing the theme recolours everything that refers to it at once

More: [[4_composition-and-camera|Composition and the camera]], [[6_themes]]

## Beat grid

Helps you place content on the music. Generators work on the same beats you see

It is authoring metadata, not a mechanic. **Playback does not read the grid**

The grid is a list of **segments**. Each has a constant tempo: BPM, phase offset, beats per bar.
Segments do not overlap. The gaps between them are needed: an intro without drums, a break, the tail after the track. A single tempo track could not express that

> [!tip] Tip
> `TAP` records taps at the playhead. `Create from taps` turns them into one segment from the first tap to the last. Beats are always counted from the segment's start and do not accumulate, so the error is under half a frame

More: [[2_rhythm-and-structure|Rhythm and structure]]

## Beat segment

One stretch of constant tempo: BPM, phase offset in fractional frames, beats per bar, a name and a colour

Exactly one segment is shown, even if several are selected. Every field but the name is unique to a segment. Editing them together would collapse them into each other

> [!caution] Caution
> A segment is identified by its start frame. So **moving it changes its identity**. After a move, select the segment again at its new start

> [!tip] Tip
> Taps here re-phase the selected segment instead of creating a new one. BPM and offset change in one undo step

More: [[2_rhythm-and-structure|Rhythm and structure]]
