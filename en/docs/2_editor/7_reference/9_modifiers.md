---
title: Modifiers
date: 2026-09-24
tags: [level_author]
---

# Modifiers

What each of the built-in modifiers does to an existing level

## Remove Content

Deletes level content matching what you select here

> [!caution] Caution
> It rewrites what already exists rather than adding to it, so read the parameters before running: the undo step is one, but it is the only way back

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Remap Framerate

Rescales every frame number in the level to a different framerate, so timings land in the same place in seconds as before

> [!warning] Warning
> Frames are whole numbers, so anything that does not divide evenly is rounded - a level remapped twice is not guaranteed to return to where it started

More: [[4_frames-and-time|Frames, time and the length of a level]]

## Flatten Prefabs

Turns every prefab placement in this scope into an ordinary object: the link to the template goes, the objects it created stay exactly where they are

> [!info] Worth knowing
> The level looks identical afterwards - a flatten deletes nothing and moves nothing. Per-placement overrides are already written onto those objects, so none of them is lost. The templates themselves stay in the level unless you ask for them to be swept

## Quantize Keyframes

Snaps keyframes onto a regular step, which is how loose hand-placed animation is pulled onto the beat

> [!warning] Warning
> Two keyframes landing on the same frame collapse into one, so quantizing coarsely loses detail rather than compressing it

More: [[2_rhythm-and-structure|Rhythm and structure]]

## Fit Spans

Makes child lifetimes fit inside their parents', either by clamping the children in or by expanding the parents out

> [!info] Worth knowing
> An overhanging child is legal data that simply plays clipped, so this is a content decision rather than a repair - which is why nothing runs it for you. Anchors are left untouched either way

More: [[4_frames-and-time|Frames, time and the length of a level]]

## Stagger

Offsets a selection in time so objects that started together arrive one after another

More: [[2_reuse|Reuse: prefabs, copying, generators]]
