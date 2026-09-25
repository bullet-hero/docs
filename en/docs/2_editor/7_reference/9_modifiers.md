---
title: Modifiers
date: 2026-09-24
tags: [level_author]
---

# Modifiers

What each of the built-in modifiers does to an existing level

## Remove Content

Deletes level content that matches the conditions you set

> [!caution] Caution
> The modifier changes what already exists rather than adding to it. One undo step is the only way back. Read the parameters before running it

It works on the frame window of the generators window. Inverted, it deletes what shares no frame with the window instead. Inverted, or with `Whole Level` on, it can delete far more than you see on screen, so it asks for confirmation first

More - [[2_reuse]]

## Remap Framerate

Rescales every frame number to a different framerate.
Timings stay at the same seconds

> [!warning] Warning
> Frames are whole numbers. Anything that does not divide evenly is rounded. So a level remapped twice may not return to where it started

The form shows the level's current framerate for reference, read-only. Any real change of framerate asks for confirmation first. The modifier needs the whole level, so it is not available in Prefab Mode

More - [[4_frames-and-time]]

## Flatten Prefabs

Turns every prefab placement in this scope into ordinary objects.
The link to the template goes. The objects stay exactly where they were

> [!info] Worth knowing
> The level looks the same as before: nothing is deleted or moved. Per-placement overrides are already written onto the objects and are not lost. The templates stay in the level unless you ask for them to be removed

## Quantize Keyframes

Snaps keyframes onto a regular step.
This is how loose hand-placed animation is pulled onto the beat

It acts on the selection and needs one

> [!warning] Warning
> Two keyframes on the same frame collapse into one. So coarse quantizing loses detail rather than compressing it

More - [[2_rhythm-and-structure]]

## Fit Spans

Makes child lifetimes fit inside their parent's lifetime.
Two ways: clamp the children in or expand the parents out.
Anchors are left untouched either way

> [!info] Worth knowing
> A child that overhangs its parent is legal data. It simply plays clipped. Fitting is a content decision, not a repair, so nothing runs it for you

More - [[4_frames-and-time]]

## Stagger

Offsets a selection in time.
Objects that started together arrive one after another

It acts on the selection and needs one

More - [[2_reuse]]
