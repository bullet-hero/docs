---
title: Composition and the camera
date: 2026-09-24
tags: [level_author]
---

# Composition and the camera

Where meaningful content must not go, how screen limits work, and why a moving camera makes people ill

**Everyone's screen is different.** A level built on a 16:9 monitor shows more width and less height on a 20:9 phone, and the other way round on a 4:3 tablet. An object sitting exactly on the edge ends up either deep inside the frame or outside it

**The screen limit track** says how the visible area is constrained: not at all, a fixed aspect ratio, or a range of them. Fixed is the most predictable - everyone sees exactly what you saw, at the cost of bars on other screens

> [!tip] Recommendation
> Pick one deliberately. "Not at all" is also a choice, and it means you do not know what the player will see

> [!caution] Caution
> The game's interface insets itself out of the unsafe area, level content does not. The camera frames the level against the whole screen, so a phone cutout can cover a projectile. Keep meaningful content away from the edge

**The camera is a tool, not a backdrop.** Position, rotation, zoom, pivot and shake are all keyframe tracks

> [!tip] Tip
> A 15 degree rotation makes a simple pattern hard without adding a single object, because it breaks every direction the player had got used to

> [!caution] Caution
> The camera can make a level impassable and you will not notice, because you know where to look

> [!warning] Warning
> Fast rotation, constant shake and sharp zoom make a level impossible to finish physically - not by difficulty, by how it feels. Shake is good for one bar on a drop and unbearable for a minute

**Layers.** Draw order is relative: an object's layer is summed with the layers of all its parents. Dragging an object under a different parent changes what draws over what even when the number was never touched

> [!tip] Recommendation
> Keep decoration and danger in different layer ranges. Then decoration cannot accidentally cover a projectile

**Readability beats beauty.** The moment a player fails to see a projectile because of decoration is your mistake, not theirs. When you have to choose, cut the decoration

Next: [[2_mobile-devices|Mobile devices]], [[1_readability-and-fairness|Readability and fairness]]
