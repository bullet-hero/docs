---
title: Performance
date: 2026-09-24
tags: [level_author]
---

# Performance

How much a level can hold, what phones can take and importing from Afterbeat

This section answers two questions: will the level run on the devices its players actually have, and what changes when a level arrives from another game. Mobile is a first-class target alongside PC, so a level that only plays on a PC is half made. Read it before you target phones, and again when a finished level runs slow

## What is counted

The unit is **shapes** alive in one frame at once. The numbers are approximate, but the orders are right:

| Device | Fine | The edge |
|---|---|---|
| Phone | 1000 | 2000 |
| Weak PC | 5000 to 10000 | 20000 to 40000 |
| Average PC (Steam's own survey) | 50000 | 100000 |

Text and effects are converted into the same unit: a text object costs 2 to 100 shapes, and an effect costs 10 shapes plus 0.1 per particle, so a thousand-particle effect is about 110

## The count is not the main cost

**Overdraw is** - the same pixel painted over and over. On a mid-range mobile chip a 1000-object scene spends 95 to 97 percent of GPU time shading pixels. One translucent full-screen fill therefore costs more than a hundred projectiles, and a slow level is fixed by finding what covers the whole screen rather than by counting objects

On a weak phone the order of what sinks it first is full-screen translucency in several layers, then post-processing (Bloom above all), large textures (a 4096 image is 64 MB before anything is drawn), effects with many particles, and only then the number of shapes

## A phone is a different player

A finger covers the screen where a mouse is a point, precision is lower, the edges belong to the system and the screen is roughly 20:9. A gap passable first time with a mouse becomes its own test on a phone, which is why a tight gap is better made short in time than narrow in space

## Levels from Afterbeat

*Afterbeat*, formerly *Project Arrhythmia*, is this game's closest relative, and its `vgd`, `vgm`, `vgt` and `vgp` files are read and written. The import runs as an ordinary level generator. Objects, lifetimes, the hierarchy, transform keys, themes and prefabs cross well, while hierarchy and draw order work differently here, so an imported level needs its readability and performance checked again. Publishing it falls under the same rules as any content that is not yours, described in the section [[2_editor/3_rights/index]]

> [!tip] Recommendation
> Check on the weakest device you can reach. The device simulator shows proportions and cutouts but says nothing about performance, and a level that is fine on your own PC proves nothing
