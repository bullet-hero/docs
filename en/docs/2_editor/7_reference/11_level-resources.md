---
title: Level resources
date: 2026-09-24
tags: [level_author]
---

# Level resources

The library, every resource tab, resource metadata, the theme and shape editors and licences

## Library

Resources saved on **this device**, shared by every level you open here

> [!info] Worth knowing
> Importing copies the resource *into the level*, which is what keeps a level portable: it is a folder of files, and it has to carry everything it needs

> [!info] Worth knowing
> The library is therefore a convenience for you, never a dependency for whoever plays your level

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Textures

Images this level carries. **The game itself ships no texture** - every texture a level sees is its own, added here

> [!tip] Tip
> A level is just a folder of files the game interprets, so a texture lives beside the level and travels with it: zip the folder, send it, unzip, play

> [!info] Worth knowing
> Shapes are **not** textures. They are real geometry, so a shape needs nothing from this tab

More: [[3_images-and-fonts|Images and fonts]]

## Shapes

The level's own shapes, on top of the ~500 the game generates

> [!info] Worth knowing
> A shape is **real geometry**, not a picture: it is fitted to its bounding box, so it measures exactly 1 across its longer axis and the object's rect really is what it draws

> [!tip] Tip
> **A shape and a hitbox are the same kind of data**, and an object carries two references: one for what is drawn, one for what is hit. Neither derives from the other, which is what makes a harmless telegraph beam, a hitbox simpler than its art, and an invisible wall all ordinary content

More: [[1_level-needs|What a level needs]]

## Themes

A theme is a **palette the level's colours can point at** instead of holding literal values

> [!info] Worth knowing
> Because a colour can be a reference, swapping the active theme restyles everything pointing at it at once - and the active theme is itself animatable on the Events timeline, which is how a level changes its whole look mid-song

> [!tip] Tip
> Themes can be saved to the device-wide library and reused across levels

More: [[6_themes]], [[5_color-and-postprocessing|Colour, themes and post-processing]]

## Effects

`VFX Graph` particle effects the level can place

> [!info] Worth knowing
> They are **optional enrichment**, not load-bearing: a level that never uses one plays exactly as designed

An effect is seeded from the same addressed randomness everything else uses, so it replays identically on any device. Effects can be saved to the device-wide library and reused

More: [[1_level-budget|The level's budget]]

## Prefabs

Reusable groups of objects. A prefab holds its own template objects, and placing one writes real copies of them into the level

> [!info] Worth knowing
> Editing the template later re-propagates to every placement, and a placement can still diverge through per-instance overrides

> [!warning] Warning
> Prefabs have **no game-defined presets**, unlike themes, effects and colliders - the device-wide library is the only way to share one between levels

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Resource metadata

Title, description, sources, licence and authors for one resource

> [!info] Worth knowing
> This is how attribution survives: a texture, font or audio file taken from somewhere carries where it came from and under what terms, inside the level, wherever the level goes

> [!tip] Recommendation
> Fill it in when you add the resource - that is the only moment you still remember

More: [[4_resource-record|A resource's record]]

## Theme editor

The slots a theme provides and the colours filling them

> [!caution] Caution
> Slots are what level content points at, so **renumbering them restyles everything that references them** - a slot's position is its identity

> [!tip] Tip
> Save a finished theme to the device-wide library to reuse it in other levels

More: [[6_themes]], [[5_color-and-postprocessing|Colour, themes and post-processing]]

## Theme colour reference

Point this colour at a **slot in the level's theme** instead of giving it a literal value

> [!info] Worth knowing
> Everything referencing a slot restyles at once when the theme changes, and themes can be animated on the Events timeline - which is how a level changes its whole palette mid-song without touching a single object

> [!tip] Tip
> The swatches show the palette blended at the frame of the key you are editing, never at the playhead, and the window names the themes on either side of that frame. To pick against a later look, edit a key that sits later

More: [[6_themes]], [[5_color-and-postprocessing|Colour, themes and post-processing]]

## Shape editor

Build a shape from points and the edges between them

> [!info] Worth knowing
> You edit points and edges. **Triangles are derived, never edited**. That is what makes a corner shared by three triangles one thing to drag instead of three that come apart

> [!warning] Warning
> Edges are an editor concept - the format stores triangles - so an edge that closes no loop is dropped on save and reported rather than silently swallowed

More: [[3_images-and-fonts|Images and fonts]]

## Licences

The terms this level and its resources come under

A level carries every file it needs - images, fonts, audio - and each of those can come from somewhere with its own conditions. **Those conditions are recorded per resource**, not just for the level as a whole, which is what lets a level made of borrowed parts still say exactly what was borrowed and under what terms

> [!tip] Recommendation
> Worth reading before reusing anything from a level someone else made

More: [[1_licensing-basics|Licensing: the whole thing in three minutes]]
