---
title: Images and fonts
date: 2026-10-02
tags: [level_author]
---

# Images and fonts

If a shape will do, use a shape: it has no file, no memory cost and no rights question. Make an image the size of its place on screen, no more than {{v:texture.mobile-max-side}} for a mobile level and {{v:texture.desktop-max-side}} overall

Round the image size up to a power of two

## Formats and size

Anything the engine can decode from a file's bytes loads. In practice that is `png` and `jpg`

The game puts no limit on the file size, the hardware does:

| Device | Largest side |
|---|---|
| Android, guaranteed | 4096 |
| Android, usually | 8192-16384 |
| desktop PC | up to 32768 |

## Memory

**The real limit is memory.** In memory an image is stored as raw pixels, however much the file weighs.
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

Three items in every player's graphics settings decide how much memory an image takes:
- whether images are compressed on load. Compression divides the numbers above by 4-8
- the largest side of an image in memory. Half the side - a quarter of the memory
- whether to build mip-maps, reduced copies for drawing small

A phone compresses images and caps them at {{v:texture.mobile-max-side}} by default. A desktop PC keeps the full image and caps it at {{v:texture.desktop-max-side}}

**Your part is the fields on the image, first of all what it depicts.** They sit next to the image in the resources list.
A photograph survives scaling down and compression best. A drawing with hard edges survives them worse

`{{ui:enum_texture-kind_pixel-art}}` never gets mip-maps, whatever the device would prefer. It also starts out uncompressed and unsmoothed, and the `{{ui:level_resources_texture-compression}}` and `{{ui:level_resources_texture-sampling}}` fields can change that

## Mip-maps

Mip-maps stop a small image from shimmering. They are reduced copies drawn instead of the full image while it is small on screen.
They cost a third more memory

Without mip-maps a scaled-down image does not smooth out, it ripples. A player can turn them off, and `{{ui:enum_texture-kind_pixel-art}}` never gets them

A 4096 image that takes 200 pixels on screen costs 256 times the memory of the same image scaled down to 256 in advance

## Shapes before images

A shape is cheaper than an image in every way: no file, no memory, no rights question.
Built-in shapes are real geometry, not a picture on a rectangle. They have no transparent margins that get drawn and thrown away

This shows on a phone. On a mid-range mobile chip a scene of 1000 objects spends 95-97% of the GPU's time shading pixels.
A shape covers 29.4% of its rectangle. The rest of a textured quad is transparent waste

An image is needed when you need exactly a picture: a logo, a photograph, hand-drawn art.
For a geometric form, take a shape. If the one you need does not exist, draw it in the `{{ui:hint_level_shape-editor_header}}`

## Fonts

Fonts load as `ttf`, `otf`, `ttc`. With no font of its own, text is drawn with whatever the system has, and that differs between devices

The `{{ui:settings_level-settings_fontcache}}` is the set of characters prepared for drawing in advance. A generator rebuilds it from the text the level contains.
Run the generator once the text stops changing

Next: [[1_level-budget]], [[2_mobile-devices]]
