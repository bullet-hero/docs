---
title: Mobile devices
date: 2026-09-24
tags: [level_author]
---

# Mobile devices

A finger instead of a mouse, edges the system has taken, and what sinks a weak phone first

Mobile is a first-class target alongside PC, which means a level that only plays on a PC is half made

**A finger covers the screen.** A mouse is a point, a finger is a blob you cannot see under

> [!tip] Recommendation
> Do not build a pattern that requires looking exactly where the player is. On a PC it works, on a phone that is a blind spot

**Control is different in kind.** On a PC the cursor sets the target and the avatar drives to it. On a phone precision is lower and the finger carries more inertia. A gap passable first time with a mouse becomes its own test on a phone

> [!tip] Recommendation
> Make a tight gap short in TIME rather than narrow in space

> [!caution] Caution
> The edges belong to the system - the camera cutout, the rounded corners, the navigation gestures. The game's interface insets itself out of the unsafe area, level content does not. Keep what matters away from the edges, and especially away from the top one

**Aspect ratio.** A phone is roughly 20:9, noticeably narrower and longer than whatever you are working on

> [!tip] Recommendation
> Look at the level in the device simulator at least once in that shape before calling it finished

**What sinks a phone first**, in order:
1. Full-screen translucency in several layers
2. Post-processing, Bloom above all - it scales with resolution rather than with the object count
3. Large textures. A 4096 image is 64 MB of memory before anything is drawn, and a quarter of that only if the player's own settings compress it
4. Effects with a lot of particles
5. And only then the number of shapes

> [!info] Worth knowing
> Anti-aliasing costs differently on a phone. `MSAA` resolves per sample, so its cost grows with translucent overdraw - exactly where a weak phone already suffers. `FXAA` is one full-screen pass regardless. That is the player's setting, but it explains why the same level behaves differently on two similar phones

> [!caution] Caution
> The device simulator shows proportions and cutouts and tells you nothing about performance. One run on a real weak device is worth more than any amount of reasoning

Next: [[4_composition-and-camera|Composition and the camera]], [[1_level-budget|The level's budget]]
