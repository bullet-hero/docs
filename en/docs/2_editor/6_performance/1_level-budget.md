---
title: "The level's budget"
date: 2026-09-24
tags: [level_author]
---

# The level's budget

How many shapes a phone and a PC hold, what text and effects cost in shapes, and why the count is not what kills you

## How many shapes a device holds

The numbers below are approximate but the orders are right. What is counted is **shapes** alive in one frame at once

**Phone:** 1000 shapes is fine, 2000 is the edge of playable

**PC** depends on the machine:
- weak: 5000 to 10000 fine, 20000 to 40000 the edge
- average by Steam's own survey: 50000 fine, 100000 the edge

## What text and effects cost

**Text** counts in shapes: 2 to 100 shapes per text object, depending on how complex the font is, how many characters there are, how many styles, and whether it animates

**An effect** counts as 10 shapes for the object itself plus 0.1 shapes per particle. A thousand-particle effect is about 110 shapes

## Overdraw

**The count is not what costs you. Overdraw is** - the same pixel being painted over and over

> [!info] Worth knowing
> On a mid-range mobile chip a 1000-object scene spends 95 to 97 percent of GPU time shading pixels at 60 to 70 times overdraw. A thousand small shapes spread over the screen is cheaper than ten translucent full-screen shapes stacked on each other

What follows:
- one full-screen translucent fill costs more than a hundred projectiles
- layers of translucent decoration on top of each other are the most expensive thing you can build
- when a level runs slow, look for what covers the whole screen, not for the object count

## Opaque and transparent

Opaque and transparent are two different paths. A shape chooses: `Auto`, `Opaque`, `Transparent`. The opaque path is cheaper, because the GPU can throw away covered pixels early

`Auto` resolves itself once at load under a hard contract - it never changes how the level looks. Anything it cannot prove opaque becomes transparent

> [!warning] Warning
> Set the path by hand only when you know exactly what you are doing. An object forced opaque that is not looks wrong rather than fast

## The capacity hint

On save, a level records how many objects its heaviest frame needed. That is a hint for the loader rather than a limit, and a generator recomputes it

## Where to check

Check on the weakest device you can reach. It will be fine on your own PC, and that means nothing

Next: [[2_mobile-devices|Mobile devices]], [[3_images-and-fonts|Images and fonts]]
