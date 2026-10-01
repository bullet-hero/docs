---
title: Modifiers
date: 2026-10-01
tags: [level_author]
---

# Modifiers

A modifier changes what is already in the level: it removes content, recalculates fps, flattens prefabs, quantizes keyframes, fits and shifts spans. A run is undone in one step

## Remove Content

Removes level content that matches the given conditions

> [!caution] Caution
> The modifier changes what exists instead of adding. Everything can be brought back only with one undo step. Read the parameters before running it

It works on the frame window from the generators window. In inverse mode it instead removes what shares no frame with the window. In inverse mode or with `Whole Level` on it can remove far more than is visible on screen, so it asks for confirmation first

More - [[2_reuse]]

## Remap Framerate

Recalculates every frame number for a different frame rate.
The timings stay on the same seconds

> [!warning] Warning
> Frames are whole numbers. Anything that does not divide evenly is rounded. So after two recalculations the level may not return to the original

The form shows the level's current frame rate for reference, read-only. Any real change of frame rate asks for confirmation first. The modifier needs the whole level, so it is unavailable in prefab mode

More - [[4_frames-and-time]]

## Flatten Prefabs

Turns every prefab placement in this scope into ordinary objects.
The link to the template is gone. The objects stay exactly where they were

> [!info] Worth knowing
> The level looks the same as before the run: nothing is deleted or moved. Edits to individual placements are already written into the objects themselves and are not lost. The templates stay in the level unless you ask to delete them

## Quantize Keyframes

Pulls keyframes onto a regular step.
That way uneven hand animation lands on the beat

Works on the selection, and does not run without one

> [!warning] Warning
> Two keyframes on the same frame collapse into one. So coarse quantizing loses detail rather than compressing it

More - [[2_rhythm-and-structure]]

## Fit Spans

Places the lifetimes of children inside the lifetime of their parent.
Two ways: shrink the children or stretch the parents.
Anchors do not change in either of them

> [!info] Worth knowing
> A child that goes past its parent is valid data. It simply plays cut off. Fitting is a decision about content, not a bug fix, so it never runs on its own

More - [[4_frames-and-time]]

## Stagger

Shifts the selection in time.
Objects that started together appear one after another

Works on the selection, and does not run without one

More - [[2_reuse]]
