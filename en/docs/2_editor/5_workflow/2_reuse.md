---
title: "Reuse: prefabs, copying, generators"
date: 2026-09-24
tags: [level_author]
---

# Reuse: prefabs, copying, generators

Four tools that all mean "do not build this twice", and which one fits which job

## Which one to pick

Ask two questions:
1. Will these objects need changing all at once later? Then a prefab, whatever the count
2. Can the content be described by a rule rather than drawn by hand? Then a generator, even for eight objects

If both answers are "no", just copy

Why a generator even for eight objects: a generator run is one operation to undo.
Eight hand-placed objects are eight chances to misalign one of them

## Copy and paste

For a shape you want again a few times, with no link to the original afterwards

There are five clipboard buffers, one per timeline. Clips copied on one timeline can never be pasted over keys on another

Copy and paste are routed differently:
- **A paste** always goes into the timeline you are looking at
- **A copy** takes what is selected. The open timeline wins when it has a selection of its own. Otherwise the selection is copied from wherever it is, so an object selected while the Local timeline is open is still copied

Duplicate (`Ctrl+D`) writes to no buffer at all. What you copied earlier is not lost

Duplicate and paste treat the parent differently:
- **A duplicate** keeps the parent. The copy sits beside the original in the hierarchy
- **A paste** drops the parent, so pasted objects land at the top level. The exception is a parent of `Camera` or `Local Player`: at level scope it survives a paste

Both look for a free layer only on the frames each copied object lands on. A paste onto an empty stretch of the timeline keeps the layers the objects had

A copy's name is renumbered. A trailing `_` with digits is the object's own id, so `Shape_12` becomes `Shape_` plus the new id. A name with no such suffix gets none, and a suffix that is not purely digits (`Wave_2b`) is left alone. Audio tracks are renamed the same way

Objects copied inside Prefab Mode paste back into a template, not into the level

> [!caution] Caution
> Buffers are cleared when a level loads. Every id and frame in them belongs to the level that was open

## Prefabs

For a thing you want many times and want to change everywhere at once

A prefab is a template plus placements of it. When you point a placement at a template, the placement gets real copies of its objects with permanent ids. The level file keeps only the placement itself: the template, the ids of the copies and your overrides. The copies are rebuilt from the template every time the level loads

Editing the template spreads to every placement that references it.
Editing a copy in one placement (outside template editing) records an override for that instance only.
Overrides survive later edits to the template. That is what makes a prefab usable for variations, not only for clones

Prefabs can be nested. A nested template can be edited from inside another: templates open on top of each other and close in reverse order

### Making a prefab from a selection

Select the objects and press `Ctrl+G` (`Create Prefab From Selection`). The same action is in:
- the command palette
- the viewport's context menu, while something is selected
- a hierarchy row's menu, as `Create Prefab From This`
- Level Settings, the `Prefabs` tab, `From Selection`

The selected objects move into a new template, and one placement of it takes their place and is selected. It is one operation to undo.
A single object names the template after itself. Several objects make a template called `Prefab`

A placement, or an object that belongs to one, cannot be packed again. Its menus offer `Open in Prefab` instead, which opens its template.
Inside Prefab Mode packing is not available

## Generators and modifiers

**Generators** create content from a rule: a spiral, a grid, a fractal, a wave, a rain of bullets, a fan of lasers. You give a window of frames, a layer and a seed, and get objects. The estimate is shown before you press anything

**Modifiers** do the same with content that already exists: fit spans, stagger them, quantise keys, remap the framerate, remove content in a window

## Across levels: the device-wide libraries

Everything above works inside one level. Only the device-wide libraries cross from one level to another

Themes, effects, shapes and prefabs are exported out of a level and imported into another.
The libraries live beside the levels folder, so a level you send carries its own copy

Next: [[3_speed-and-shortcuts|Speed and shortcuts]], [[4_level-folder-and-backups|The level folder and backups]]
