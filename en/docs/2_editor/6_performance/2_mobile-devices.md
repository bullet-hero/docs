---
title: Mobile devices
date: 2026-09-24
tags: [level_author]
---

# Mobile devices

A finger instead of a mouse, edges the system has taken, and what sinks a weak phone first

Phones are as much a target as the PC.
A level that only plays on a PC is half made

## A finger instead of a mouse

**A finger covers the screen.** A mouse is a point, a finger is a blob you cannot see under.
Do not build a pattern that requires looking exactly where the player is. On a PC it works, on a phone it is a blind spot

**Control is different.** On a PC the cursor sets the target and the character drives to it. On a phone precision is lower and the finger carries more inertia.
A gap passable first time with a mouse becomes its own test on a phone

**Make a tight gap short in time,** not narrow in space

## The screen's edges and shape

> [!caution] Caution
> The edges belong to the system: the camera cutout, the rounded corners, the navigation gestures. The game's interface insets itself out of the unsafe area, level content does not. Keep what matters away from the edges, especially the top one

**Aspect ratio.** A phone is roughly 20:9, noticeably narrower and longer than whatever you are working on.
Look at the level in the device simulator in that shape at least once before calling it finished

> [!caution] Caution
> The device simulator shows proportions and cutouts but tells you nothing about performance. One run on a real weak device is worth more than any amount of reasoning

## What sinks a phone first

In order:
1. Full-screen translucency in several layers
2. Post-processing, Bloom above all. Its cost grows with resolution, not with the object count
3. Large textures. A 4096 image takes 64 MB of memory before anything is drawn. A quarter of that only if the player's own settings compress it
4. Effects with a lot of particles
5. And only then the number of shapes

## Anti-aliasing

Anti-aliasing is the player's setting, not the level's.
But it explains why the same level behaves differently on two similar phones:
- `MSAA` resolves per sample. Its cost grows with translucent overdraw, exactly where a weak phone already suffers
- `FXAA` is one full-screen pass, its cost does not depend on anything

Next: [[4_composition-and-camera|Composition and the camera]], [[1_level-budget|The level's budget]]
