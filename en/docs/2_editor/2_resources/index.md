---
title: Resources
date: 2026-09-24
tags: [level_author]
---

# Resources

The track, images, fonts and the level folder: what a level is made of on disk

This section is about the files a level carries: which formats load, what size is sensible and where everything lies in the level folder. The minimum level is one track, and nearly everything else you bring yourself, because the developers ship no image of their own

## Files and data

A level uses two kinds of material, and they behave differently:

| Kind | What | Where it lives |
|---|---|---|
| Files | audio, images, fonts | the `resources` folder inside the level folder |
| Data | themes, effects, prefabs | inside `level.json` |

Only files add weight to the folder, need a record of their origin before publishing and can get lost in a move. The 497 built-in shapes are geometry rather than pictures, so they cost no file, no memory and no rights question. [[1_level-needs]] lists what a level can use and how one resource can name several sources

## The short version

- **Track.** `ogg`, `mp3`, `wav`, `aiff` and the tracker modules load, `flac` does not. Convert to `ogg`: it weighs 8 to 10 times less than `wav`, and unlike `mp3` it adds no silence to the start of the file that shifts the beat map. The rest is in [[2_preparing-the-track]]
- **Images.** In practice `png` and `jpg`. Memory is counted in raw pixels, so a 4096 by 4096 picture takes 64 MB whatever the file weighs. Treat 2048 as the ceiling for a mobile level, and see [[3_images-and-fonts]] for how the player's graphics settings change those numbers
- **Fonts.** `ttf`, `otf`, `ttc`. With no font of its own, text is drawn with whatever the device has
- **Folder.** A level lives in `levels` inside the game's folder, and a copy of that folder is the only backup there is. [[4_level-folder-and-backups]] shows what lies inside and what not to touch

> [!tip] Recommendation
> Reach for a built-in shape before an image, and keep a url as an addition to a file in the folder rather than instead of it. A shape costs nothing to carry, and a file sits exactly where the level does, while a site can go down or start serving something else

> [!caution] Caution
> Do not rename files in `resources` by hand. References to them are stored by name, so a renamed file is a missing file

## Where this leads

A file that leaves your disk inside a level needs a licence that allows it, and that is covered in [[2_editor/3_rights/index]]. How much a phone and a PC can hold is counted in [[1_level-budget]]
