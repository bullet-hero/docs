---
title: Mobile devices
date: 2026-10-01
tags: [level_author]
---

# Mobile devices

On a phone a finger covers the screen, and the system takes the edges. Keep what matters away from the edges and test the level on a weak phone: full-screen translucency drains it first

Phones are as much a target as the PC.
A level that plays only on a PC is half made

## A finger instead of a mouse

**A finger covers the screen.** A mouse is a point, a finger is a blob with nothing visible under it.
Do not build a pattern that requires looking exactly where the player is. On a PC it works, on a phone it is a blind spot

**Control is different.** On a PC the cursor sets the target, and the character moves to it. On a phone precision is lower, and a finger has more inertia.
A gap a mouse takes on the first try becomes a test of its own on a phone

**Make a narrow gap short in time,** not narrow in width

## Edges and screen shape

> [!caution] Caution
> The edges belong to the system: the camera cutout, rounded corners, navigation gestures. The game's interface keeps clear of the unsafe area, level content does not. Keep what matters away from the edges, especially the top one

**Aspect ratio.** A phone is about 20:9, noticeably narrower and longer than what you work on.
At least once, look at the level in the device simulator in this shape before you consider it done

> [!caution] Caution
> The device simulator shows proportions and cutouts but says nothing about performance. One run on a real weak device is worth more than any reasoning

## What drains a phone first

In order:
1. Full-screen translucency in several layers
2. Post-processing, Bloom above all. Its cost grows with resolution, not with the number of objects
3. Large textures. A 4096 image takes 64 MB of memory before anything is drawn. A quarter of that only if the player's own settings compress it
4. Effects with many particles
5. And only then the number of shapes

## Anti-aliasing

Anti-aliasing is a player setting, not a level setting.
But it explains why the same level behaves differently on two similar phones:
- `MSAA` is computed per sample. Its cost grows with translucent overdraw, exactly where a weak phone already struggles
- `FXAA` is one pass over the screen, its cost does not depend on anything

Next: [[4_composition-and-camera|Composition and camera]], [[1_level-budget|Level budget]]
