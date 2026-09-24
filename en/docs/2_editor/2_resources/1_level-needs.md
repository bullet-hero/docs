---
title: What a level needs
date: 2026-09-24
tags: [level_author]
---

# What a level needs

The minimum is a track. The developers ship no image of their own, so everything else you bring yourself

A minimal level is a track and nothing else. Everything else is optional, and nearly everything else you bring yourself

## What a level can use

**The developers ship no texture of their own.** The 497 built-in shapes are geometry rather than pictures: they have no pixels, they weigh nothing, and there is nowhere to load them from

What a level can use:
- **Audio** - at least one track, though there can be several
- **Images** - for the cases a shape cannot cover
- **Fonts** - `ttf`, `otf`, `ttc`. With no font of its own, text is drawn with whatever the system has
- **Shapes** - the 497 built-in ones plus any drawn in the shape editor
- **Themes, effects, prefabs** - data rather than files, living inside `level.json`

The first three are real files on disk. The last three never leave the level

## Several sources for one resource

A resource carries a list of places it can be fetched from - a file beside the level, an absolute path, a direct url - and the game walks that list until something loads

> [!tip] Recommendation
> Keep a url as an addition to the file rather than instead of it. A site can go down, move, or start serving something else, while a file in the folder sits exactly where the level does

## The weight of the folder

There is no formal limit, but a level travels by copying, and the folder's weight is what the person receiving it sees. A 4-minute track in `ogg` is 4 to 6 MB, the same track in `wav` is around 40 MB

> [!tip] Recommendation
> Reach for a shape before an image, every time. An image is a file to not lose in a move, memory at load time, and a line in a licence record if the level ever leaves your disk. A shape costs none of those

Next: [[2_preparing-the-track]], [[3_images-and-fonts]]
