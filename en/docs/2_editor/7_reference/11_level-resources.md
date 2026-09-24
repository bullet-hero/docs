---
title: Level resources
date: 2026-09-24
tags: [level_author]
---

# Level resources

The library, the resource tabs, resource metadata, the theme and shape editors, licences

## Library

Resources saved on **this device**. They are shared by every level you open here

Importing copies the resource *into the level*.
A level is a folder of files, and it carries everything it needs. That is what keeps it portable

So the library is a convenience for you. Whoever plays your level never depends on it

More - [[2_reuse]]

## Textures

Images this level carries.
**The game itself ships no textures.** Every texture a level uses was added here

A level is just a folder of files. A texture lives in it and travels with the level: zip the folder, send it, unzip, play

Shapes are **not** textures, they are real geometry. They need nothing from this tab

More - [[3_images-and-fonts]]

## Shapes

The level's own shapes. They come on top of the ~500 shapes the game generates

A shape is **real geometry**, not a picture.
It is fitted to its bounding box, and its longer side measures exactly 1. So the object's rect matches what it draws

> [!tip] Tip
> **A shape and a hitbox are the same kind of data.** An object carries two references: one for what is drawn, one for what is hit. Neither derives from the other. So a harmless telegraph beam, a hitbox simpler than its art and an invisible wall are all ordinary content

More - [[1_level-needs]]

## Themes

A theme is a **palette**. The level's colours can point at it instead of holding literal values

Swapping the active theme restyles everything that points at it at once.
The active theme can be animated on the Events timeline. That is how a level changes its whole look mid-song

Themes can be saved to the device-wide library and reused in other levels

More - [[6_themes]], [[5_color-and-postprocessing]]

## Effects

`VFX Graph` particle effects the level can place

Effects are **optional enrichment**. A level that never uses one plays exactly as designed

An effect uses the same seeded randomness as everything else in the level. So it replays identically on any device.
Effects can be saved to the device-wide library and reused in other levels

More - [[1_level-budget]]

## Prefabs

Reusable groups of objects.
A prefab holds its own template objects. Placing a prefab writes real copies of them into the level

Editing the template later carries over to every placement.
A placement can still differ from the template through per-instance overrides

> [!warning] Warning
> Prefabs have **no game-defined presets**, unlike themes, effects and colliders. The device-wide library is the only way to share a prefab between levels

More - [[2_reuse]]

## Resource metadata

Title, description, sources, licence and authors of one resource

This is how attribution survives.
A texture, font or audio file taken from somewhere carries, inside the level, where it came from and under what terms. That record goes wherever the level goes

> [!tip] Recommendation
> Fill it in when you add the resource. That is the only moment you still remember where it came from

More - [[4_resource-record]]

## Theme editor

The slots of a theme and the colours in them

> [!caution] Caution
> Level content points at a slot by its position. So **renumbering slots restyles everything that references them**

> [!tip] Tip
> Save a finished theme to the device-wide library. Then you can use it in other levels

More - [[6_themes]], [[5_color-and-postprocessing]]

## Theme colour reference

Points this colour at a **slot in the level's theme** instead of a literal value

When the theme changes, everything referencing a slot restyles at once.
Themes can be animated on the Events timeline. That is how a level changes its whole palette mid-song without touching a single object

> [!tip] Tip
> The swatches show the palette at the frame of the key you are editing, never at the playhead. The window names the themes on either side of that frame. To pick against a later look, edit a key that sits later

More - [[6_themes]], [[5_color-and-postprocessing]]

## Shape editor

Builds a shape from points and the edges between them

You edit points and edges. **Triangles are derived automatically and never edited.**
So a corner shared by three triangles is one point to drag, not three that come apart

> [!warning] Warning
> Edges exist only in the editor, the format stores triangles. So an edge that closes no loop is dropped on save. The editor reports it rather than dropping it silently

More - [[3_images-and-fonts]]

## Licences

The terms this level and its resources come under

A level carries every file it needs: images, fonts, audio. Each file can come with its own conditions.
**Those conditions are recorded per resource**, not just for the level as a whole. So a level made of borrowed parts can say exactly what was borrowed and under what terms

> [!tip] Recommendation
> Read them before reusing anything from someone else's level

More - [[1_licensing-basics]]
