---
title: How the editor works
date: 2026-10-12
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

## Coordinates

Positions, sizes and distances are in world units. The point (0, 0) is the centre of the screen while the camera has no keys of its own. X grows to the right, y grows up

The camera's zoom is the height of the visible area in units, {{v:camera.default-height}} by default. So a 16:9 screen shows x from about -{{v:camera.default-half-width}} to {{v:camera.default-half-width}} and y from -{{v:camera.default-half-height}} to {{v:camera.default-half-height}}. A wider or narrower screen changes the width only

A position key is relative to the parent. It is the offset of the object's pivot from the parent's anchor point, and it turns and scales along with the parent. An object with no parent is placed in world coordinates. A child of the camera moves with the camera

- **pivot** - the point of the object's own box that the position places and that rotation and scale act around. `(0.5, 0.5)`, the centre, by default
- **anchors** - the point of the parent's box the position counts from, from `(0, 0)` (bottom left) to `(1, 1)` (top right). The centre by default. Two different anchors stretch the child along with the parent

Rotation turns counter-clockwise. The file stores it in radians, and the AI assistant writes radians too. The inspector shows degrees by default, the `{{ui:settings_game-editor_interface-rotation-unit}}` editor setting switches it to radians

Next: [[4_frames-and-time]], [[5_keyframes-and-easing]], [[1_readability-and-fairness]]
