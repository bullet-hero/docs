---
title: What a level needs
date: 2026-09-24
tags: [level_author]
---

# What a level needs

The minimum is a track. Everything else is optional, and nearly all of it you bring yourself

## What a level can use

| What | Details | Where it lives |
|---|---|---|
| Audio | at least one track, there can be several | the level's `resources` folder |
| Images | when a shape is not enough | the level's `resources` folder |
| Fonts | `ttf`, `otf`, `ttc` | the level's `resources` folder |
| Shapes | 497 built-in ones and any drawn in the `Shape editor` | built into the game or into the level |
| Themes, effects, prefabs | data rather than files | inside `level.json` |

Audio, images and fonts are real files.
Only they add weight to the folder, need a record of their origin before publishing and can get lost in a move

With no font of its own, text is drawn with whatever the system has

**The developers ship no textures at all.** Built-in shapes are geometry rather than pictures. They have no pixels, they weigh nothing, and there is nowhere to load them from

> [!tip] Recommendation
> Reach for a shape before an image, every time. An image is a file you can lose in a move, memory at load time and a line in a licence record. A shape costs none of those

## The weight of the folder

There is no hard limit. But a level travels by copying, and the folder's weight is what the person receiving it sees

A 4-minute track in `ogg` is 4 to 6 MB. The same track in `wav` is around 40 MB

## Several sources for one resource

A resource can carry a list of places to fetch it from: a file beside the level, an absolute path, a direct url.
The game walks that list until something loads

> [!tip] Recommendation
> Keep a url as an addition to the file rather than instead of it. A site can go down, move or start serving something else. A file in the folder sits exactly where the level does

## Rights to the files

If the level leaves your disk, every file in it needs a licence that allows it.
That is decided by the resources you pick at the very start

More - [[2_editor/3_rights/index]]

Next: [[2_preparing-the-track]], [[3_images-and-fonts]]
