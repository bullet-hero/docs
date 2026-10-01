---
title: Level budget
date: 2026-10-01
tags: [level_author]
---

# Level budget

A phone comfortably holds about 1000 shapes in one frame, a weak PC 5000-10000. Overdraw costs more than the count: translucent things over the whole screen, layer upon layer

## How many shapes a device holds

What counts is **shapes** alive at the same time in one frame. The numbers are approximate, but the order of magnitude is right

| Device | Comfortable | Limit of playable |
|---|---|---|
| Phone | 1000 | 2000 |
| Weak PC | 5000-10000 | 20000-40000 |
| Average PC (per the Steam survey) | 50000 | 100000 |

Test on the weakest device you can reach.
On your own PC everything will be fine, and that means nothing

## Text and effects

Text and effects are counted in shapes too

**Text:** from 2 to 100 shapes per text object. The cost depends on the complexity of the font, the number of characters, the number of styles and whether the text is animated

**Effect:** 10 shapes for the object itself plus 0.1 shapes for each particle. An effect with a thousand particles is about 110 shapes

## Overdraw

**What costs a lot is not the count but overdraw.** That is when the same pixel is painted again and again

What follows from this:
- one translucent fill over the whole screen costs more than a hundred projectiles
- layers of translucent decoration on top of each other are the most expensive thing you can build
- if the level lags, look for what covers the whole screen instead of counting objects

> [!info] Worth knowing
> On an average mobile chip a scene of 1000 objects with 60-70x overlap spends 95-97 percent of GPU time painting pixels. A thousand small shapes all over the screen are cheaper than ten translucent full-screen shapes on top of each other

## Opaque and translucent

A shape has a choice of draw path: `Auto`, `Opaque`, `Transparent`.
The opaque path is cheaper: the GPU throws away covered pixels in advance

`Auto` decides by itself, once at load. Its hard condition is to never change how the level looks.
Anything that cannot be proven opaque becomes translucent

> [!warning] Warning
> Set the path by hand only if you know exactly what you are doing. An object declared opaque that is not opaque will not be faster, it will look wrong

## Capacity hint

On save, the level records how many objects its heaviest frame needed.
This is a hint for the loader, not a limit. A generator recalculates it

Next: [[2_mobile-devices|Mobile devices]], [[3_images-and-fonts|Images and fonts]]
