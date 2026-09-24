---
title: Timelines
date: 2026-09-24
tags: [level_author]
---

# Timelines

Every timeline of the editor and the beat grid, one section per panel

## Level timeline

One clip per object, and the lane it sits in is its **layer**

A clip is a **span**: half-open, so an object covering frames 10-19 ends exactly where one starting at 20 begins, and the two never both draw on the shared frame

> [!info] Worth knowing
> A child's span must lie inside its parent's, but that is **resolved on read, never stored** - shrinking a parent clips what its children play without touching what you authored, so growing it back restores them. A root object running past the end of the level is legal - it simply never plays

> [!tip] Tip
> The three tools live in the button strip: **Selection** picks and drags, **Edges** reshapes an edge, **Scissors** splits a clip at the cursor. Right-clicking *empty space* opens the menu - a press on a clip belongs to the drag you came for

More: [[3_how-the-editor-thinks|How the editor thinks]], [[4_composition-and-camera|Composition and the camera]]

## Local timeline

The keyframes of the **selected object**, one lane per animatable track - position, rotation, scale, size, anchors, pivot, colour, UV, font size

Frames here are **local to the object's span**, so moving the object moves its whole animation with it

> [!info] Worth knowing
> An **empty track is valid data**, not missing data: a track with no keyframes uses the project default for that field, which is why a brand-new object animates nothing until you add a key

Blending happens between neighbouring keyframes only - the span decides which frames exist, never how they interpolate

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Prefab timeline

Prefab Mode's own timeline, over the **template's** objects

> [!info] Worth knowing
> It is bounded by the template's own frame length, not by any placement's span - a template is edited as a self-contained little level, and one template can be placed many times at different lengths

> [!warning] Warning
> It shares no selection with the rest of the editor and shows no live preview tied to a specific placement. Editing here changes the template, and the change propagates to every placement that references it

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Audio timeline

The level's audio tracks, drawn with their waveforms so you can line content up with what you hear

> [!tip] Tip
> **Span Fit** in the inspector resizes a track to its clip's real length - it is disabled without a resolvable clip, and at speed 0, because a frozen track has no length to fit

> [!caution] Caution
> The inspector's **Volume** slider is the track's fader. It is not the keyframed volume: that one is authored on the Local timeline's Volume track, and the two multiply at playback

More: [[2_preparing-the-track|Preparing the track]]

## Events timeline

Level-wide keyframes that belong to no object:
- camera position, rotation, zoom, pivot and shake
- markers and checkpoints
- the screen limit
- background and theme
- every post-processing effect
- the player's visibility, control, collision, size and speed

> [!info] Worth knowing
> The **Beat** lane is the exception on this screen: its items carry a span, which makes it the only lane Edges and Scissors act on

> [!tip] Tip
> A themeable colour can reference the level's theme instead of holding a literal, so changing the theme restyles everything that points at it at once

More: [[4_composition-and-camera|Composition and the camera]], [[6_themes]]

## Beat grid

Authoring metadata, not a game mechanic - **nothing in playback reads it**. It exists so you can place content on the music and so generators can act on the beats you actually see

The map is a list of **segments**, each a stretch of constant tempo (BPM, phase offset, beats per bar). Segments never overlap, and the gaps are the point: an intro with no percussion, a break, the tail after the song - a single tempo track could not express any of those

> [!tip] Tip
> **TAP** records taps at the playhead. **Create from taps** turns them into one segment spanning the first tap to the last. Where the beats fall is always derived from the segment's own start, never accumulated, so the error stays under half a frame instead of drifting

More: [[2_rhythm-and-structure|Rhythm and structure]]

## Beat segment

One stretch of constant tempo: BPM, phase offset in fractional frames, beats per bar, plus a name and colour

Exactly one segment is shown even when several are selected - every field but the name is unique to one segment, so editing them together would collapse them onto each other

> [!caution] Caution
> A segment is addressed by its own start frame, so **moving it changes its identity**: after a move, reselect it at its new start

> [!tip] Tip
> The tapper here re-phases the selected segment (BPM and offset in one undo step) instead of creating a new one

More: [[2_rhythm-and-structure|Rhythm and structure]]
