---
title: How the editor thinks
date: 2026-09-24
tags: [level_author]
---

# How the editor thinks

Object, frame, span, layer, parent, key - the six ideas everything else is built on

Six ideas. Once they sit in your head the rest of the editor reads itself

**Object** - the thing that is drawn and the thing that kills, and those are not the same field. It has a shape (what you see) and a collider (what hits you). A beam that glows but never touches you is an ordinary object with a shape and no collider. An invisible wall is the other way round

**Frame** - a cell, not a moment. Frame 30 occupies a stretch of time, not a point on it. A level 900 frames long holds frames 0 to 899, and 900 is the end boundary rather than a frame

**Span** - an object's lifetime, half-open: a start and a duration. Two objects placed back to back do not overlap on the frame they share, because the end is excluded

**Layer** - draw order, and it is relative. An object's layer is summed with the layers of all its parents

> [!caution] Caution
> Dragging an object under a different parent changes its draw order even when you never touched the number

**Parent** - a child inherits its transform, its active state and its lifetime. A child's span has to lie inside its parent's, but the editor never clips what you wrote: it keeps your value and resolves the effective one separately. That is what makes shrinking a parent reversible - widen it back and the child returns

**Key** - a field's value on one frame. The game interpolates between two keys. An object has many fields (position, rotation, scale, size, anchors, pivot) and each carries its own independent set of keys

> [!info] Worth knowing
> Having no keys at all is normal. A field with zero keys is not broken, it uses the default value. There is no need to key everything for the sake of tidiness

**How this compares to what you may be used to.** In Project Arrhythmia (Afterbeat) an object also lives on a stretch of time, but hierarchy and draw order are arranged differently, so an import does not carry those over one to one. Just Shapes and Beats ships no editor for players, so there is nothing there to compare

Next: [[4_frames-and-time|Frames, time and the length of a level]], [[1_readability-and-fairness|Readability and fairness]]
