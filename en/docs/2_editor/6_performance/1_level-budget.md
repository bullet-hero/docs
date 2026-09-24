---
title: "The level's budget"
date: 2026-09-24
tags: [level_author]
---

# The level's budget

How many shapes a phone and a PC hold, what text and effects cost in shapes, and why the count is not what kills you

## How many shapes a device holds

What is counted is **shapes** alive in one frame at once. The numbers are approximate, but the orders are right

| Device | Fine | The edge of playable |
|---|---|---|
| Phone | 1000 | 2000 |
| Weak PC | 5000-10000 | 20000-40000 |
| Average PC (Steam's own survey) | 50000 | 100000 |

Check on the weakest device you can reach.
It will be fine on your own PC, and that means nothing

## Text and effects

Text and effects are counted in shapes too

**Text:** 2 to 100 shapes per text object. The cost depends on how complex the font is, how many characters and styles there are, and whether the text animates

**An effect:** 10 shapes for the object itself plus 0.1 shapes per particle. A thousand-particle effect is about 110 shapes

## Overdraw

**The count is not what costs you, overdraw is.** That is the same pixel being painted over and over

What follows:
- one full-screen translucent fill costs more than a hundred projectiles
- layers of translucent decoration on top of each other are the most expensive thing you can build
- when a level runs slow, look for what covers the whole screen, do not count objects

> [!info] Worth knowing
> On a mid-range mobile chip a 1000-object scene at 60-70 times overdraw spends 95-97 percent of GPU time shading pixels. A thousand small shapes spread over the screen are cheaper than ten translucent full-screen shapes stacked on each other

## Opaque and transparent

A shape chooses its draw path: `Auto`, `Opaque`, `Transparent`.
The opaque path is cheaper: the GPU throws away covered pixels early

`Auto` decides by itself, once at load. Its hard rule is never to change how the level looks.
Anything that cannot be proven opaque becomes transparent

> [!warning] Warning
> Set the path by hand only when you know exactly what you are doing. An object forced opaque that is not opaque looks wrong rather than fast

## The capacity hint

On save, a level records how many objects its heaviest frame needed.
That is a hint for the loader, not a limit. A generator recomputes it

Next: [[2_mobile-devices|Mobile devices]], [[3_images-and-fonts|Images and fonts]]
