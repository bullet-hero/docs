---
title: How the editor works
date: 2026-10-02
tags: [level_author]
---

# How the editor works

Object, frame, span, layer, parent, key - the six ideas the whole editor rests on

Once these six ideas are clear, the rest of the editor reads itself:

| Idea | In short |
|---|---|
| Object | a shape (what you see) and a collider (what hits), two separate fields |
| Frame | a cell of time, not a moment |
| Span | an object's lifetime: a start and a duration, the end excluded |
| Layer | draw order, summed with the layers of all parents |
| Parent | passes its transform, active state and lifetime down to its children |
| Key | a field's value on one frame, the game moves the value between keys by itself |

An unfamiliar word - [[1_glossary]]

## Object

An object is the thing that is drawn and the thing that hits. Those are two different fields: a shape (what you see) and a collider (what hits).
A beam that glows but never touches you is an object with a shape and no collider. An invisible wall is the other way round

## Frame and span

A frame is a cell of time, not a moment. Frame 30 occupies a stretch, not a point.
The timeline counts from one. A level 900 frames long holds frames 1 to 900. The number 901 is the end boundary, not a frame

A span is an object's lifetime: a start and a duration. The end is not part of the span.
So two objects placed back to back do not overlap on a shared frame

More - [[4_frames-and-time]]

## Layer and parent

A layer is draw order. It is relative: an object's layer is summed with the layers of all its parents

> [!caution] Caution
> Dragging an object under a different parent changes its draw order even if you never touched the number

A parent passes its transform, active state and lifetime down to its children.
A child's span has to lie inside its parent's span

The editor never clips what you wrote. It keeps your value and computes the effective one separately.
That is why shrinking a parent is reversible: widen it back and the child returns

## Key

A key is a field's value on one frame. The game moves the value between two keys by itself.
Every field has its own set of keys: position, rotation, scale, size, anchors and pivot

> [!info] Worth knowing
> A field with no keys is not broken, it takes the default value. There is no need to key everything for the sake of tidiness

What a key stores and how the value travels between keys - [[5_keyframes-and-easing]]

Next: [[4_frames-and-time]], [[5_keyframes-and-easing]], [[1_readability-and-fairness]]
