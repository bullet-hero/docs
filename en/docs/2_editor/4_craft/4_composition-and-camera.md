---
title: Composition and the camera
date: 2026-10-01
tags: [level_author]
---

# Composition and the camera

Keep meaningful content off the edge: other screens put the edge elsewhere, and a phone cutout can cover a projectile. Camera shake is good for one bar, fast spin and sharp zoom make people sick

## Every screen is different

The level is built on a 16:9 monitor. On a 20:9 phone it shows more in width and less in height, on a 4:3 tablet the other way round.
An object that sat exactly on the edge ends up either deep inside the frame or outside it

**The `Screen Limit` track** sets how the visible area is constrained:
- not at all
- a fixed aspect ratio
- a range of aspect ratios

Fixed is the most predictable. Everyone sees exactly what you saw, but other screens get bars at the edges.
Choose deliberately. "Not at all" is a choice too, and it means you do not know what the player will see.
A new empty level or a level from an audio file already starts with a fixed 16:9 key on the first frame, unless you untick `Pin Screen Aspect` when creating it

> [!caution] Caution
> The game's interface moves out of the unsafe area of the screen, level content does not. The camera frames the level against the whole screen, so a phone cutout can cover a projectile. Keep meaningful content away from the edge

## The camera is a tool

The camera is not a backdrop. It has keyframe tracks: `Camera Position`, `Camera Rotation`, `Camera Zoom`, `Camera Pivot`, `Camera Shake`

A 15-degree rotation makes a simple pattern hard without a single new object.
It breaks every direction the player had got used to

That power works against you too. The camera can make a level impassable, and you will not notice, because you know where to look

> [!warning] Warning
> Fast rotation, constant shake and sharp zoom make a level physically impossible to finish. Not by difficulty, but by how the player feels. Shake is good for one bar on a drop and unbearable for a minute

## Layers

Draw order is relative: an object's layer is summed with the layers of all its parents.
If you drag an object to a different parent, what draws over what changes. Even if the layer number was never touched

Keep decoration and danger in different layer ranges. Then decoration will not cover a projectile by accident

## Readability beats beauty

A player who did not see a projectile because of decoration is your mistake, not theirs.
When you have to choose, cut the decoration

Next: [[2_mobile-devices|Mobile devices]], [[1_readability-and-fairness|Readability and fairness]]
