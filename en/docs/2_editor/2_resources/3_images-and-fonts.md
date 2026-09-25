---
title: Images and fonts
date: 2026-09-24
tags: [level_author]
---

# Images and fonts

Which images load, what size is sensible, and why a built-in shape nearly always beats an image

## The main points

- If a shape will do - use a shape
- The ceiling for an image is 2048 on a mobile level and 4096 overall
- Make an image roughly the size it will have on screen. Round up to the next power of two

## Formats and size

Anything the engine can decode from a file's bytes loads. In practice that means `png` and `jpg`

The game puts no limit on the file, the hardware does:

| Device | Largest side |
|---|---|
| Android, guaranteed | 4096 |
| Android, usually | 8192-16384 |
| desktop PC | up to 32768 |

## Memory

**The real limit is memory.** In memory an image is stored as raw pixels, whatever the file weighs.
A `png` takes 4 bytes per pixel. A `jpg` takes 3, because it has no transparency

| Size | Memory (`png`) |
|---|---|
| 512 by 512 | 1 MB |
| 1024 by 1024 | 4 MB |
| 2048 by 2048 | 16 MB |
| 4096 by 4096 | 64 MB |
| 8192 by 8192 | 256 MB |

> [!caution] Caution
> An 8192 texture is a quarter of a gigabyte for one picture. On a phone that is not slow, it is a crash

## What the player decides

Three of every player's graphics settings decide how much memory an image takes:
- whether images are compressed as they load. Compression divides the numbers above by 4 to 8
- the largest side an image may take in memory. Half the side - a quarter of the memory
- whether to build mip-maps, reduced copies for drawing small

A phone compresses images and caps them at 2048 by default. A desktop keeps the full image and caps it at 4096

**Your part is one field on the image: what kind of picture it is.** The field sits beside the image in the resources list.
A photograph survives scaling and compression best. A drawing with hard edges survives them less well

`Pixel Art` is never compressed, never mip-mapped and never smoothed, whatever the device would prefer

## Mip-maps

Mip-maps stop a small image from shimmering. They are reduced copies drawn instead of the full picture while it is small on screen.
They cost a third more memory

Without mip-maps an image scaled down does not smooth, it crawls. A player can turn them off, and `Pixel Art` never gets any

A 4096 image that occupies 200 pixels on screen costs 256 times the memory of the same image resized to 256 beforehand

## Shapes before images

A shape is cheaper than an image in every way: no file, no memory, no rights question.
Built-in shapes are real geometry rather than a picture on a rectangle. They have no transparent padding that gets drawn and thrown away

This matters on a phone. On a mid-range mobile chip a 1000-object scene spends 95-97% of its GPU time shading pixels.
A shape covers 29.4% of its own rectangle. The rest of a textured quad is transparent waste

An image is needed when you really need a picture: a logo, a photograph, hand-drawn art.
For a geometric form, take a shape. If the form does not exist, draw it in the `Shape editor`

## Fonts

Fonts load as `ttf`, `otf`, `ttc`. With no font of its own, text is drawn with whatever the system has, and that differs between devices

The `Font Cache` is the set of characters prepared for drawing in advance. A generator rebuilds it from the text the level contains.
Run the generator once the text stops changing

Next: [[1_level-budget]], [[2_mobile-devices]]
