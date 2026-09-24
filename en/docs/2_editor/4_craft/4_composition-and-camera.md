---
title: Composition and the camera
date: 2026-09-24
tags: [level_author]
---

# Composition and the camera

Where meaningful content must not go, how screen limits work, and why a moving camera makes people ill

## Every screen is different

A level is built on a 16:9 monitor. On a 20:9 phone it shows more width and less height, on a 4:3 tablet the other way round.
An object sitting exactly on the edge ends up either deep inside the frame or outside it

**The `Screen Limit` track** sets how the visible area is constrained:
- not at all
- a fixed aspect ratio
- a range of aspect ratios

Fixed is the most predictable. Everyone sees exactly what you saw, but other screens get bars at the edges.
Pick one deliberately. "Not at all" is also a choice, and it means you do not know what the player will see

> [!caution] Caution
> The game's interface insets itself out of the unsafe area of the screen, level content does not. The camera frames the level against the whole screen, so a phone cutout can cover a projectile. Keep meaningful content away from the edge

## The camera is a tool

The camera is not a backdrop. It has keyframe tracks: `Camera Position`, `Camera Rotation`, `Camera Zoom`, `Camera Pivot`, `Camera Shake`

A 15 degree rotation makes a simple pattern hard without a single new object.
It breaks every direction the player had got used to

The same power cuts the other way. The camera can make a level impassable, and you will not notice, because you know where to look

> [!warning] Warning
> Fast rotation, constant shake and sharp zoom make a level impossible to finish physically. Not by difficulty, by how it feels. Shake is good for one bar on a drop and unbearable for a minute

## Layers

Draw order is relative: an object's layer is summed with the layers of all its parents.
Dragging an object under a different parent changes what draws over what. Even when the layer number was never touched

Keep decoration and danger in different layer ranges. Then decoration cannot cover a projectile by accident

## Readability beats beauty

A player failing to see a projectile because of decoration is your mistake, not theirs.
When you have to choose, cut the decoration

Next: [[2_mobile-devices|Mobile devices]], [[1_readability-and-fairness|Readability and fairness]]
