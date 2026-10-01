---
title: "Reuse: prefabs, copying, generators"
date: 2026-10-01
tags: [level_author]
---

# Reuse: prefabs, copying, generators

Objects you will later have to change all at once make a prefab, however many there are. Content that can be described by a rule makes a generator. In every other case just copy

A generator is worth it even for eight objects: a generator run is one operation to undo.
Eight objects placed by hand are eight chances to miss with one of them

## Copying

For a shape you need to repeat a few times and no longer link to the original

There are five clipboard buffers, one per timeline. Clips copied on one timeline will not paste over keyframes on another

Copy and paste are routed differently:
- **A paste** always goes into the timeline you are looking at
- **A copy** takes what is selected. The open timeline wins if it has a selection of its own. Otherwise the selection is copied wherever it is, so an object selected while the local timeline is open is still copied

Duplicate (`Ctrl+D`) writes to no buffer. What you copied earlier is not lost

Duplicate and paste treat the parent differently:
- **A duplicate** keeps the parent. The copy sits next to the original in the hierarchy
- **A paste** drops the parent, and the pasted objects end up at the top level. The exception is a `Camera` or `Local Player` parent: at level scope it survives a paste

Both look for a free layer only on the frames each copied object lands on. A paste onto an empty stretch of the timeline keeps the layers the objects had

A copy's name is renumbered. A tail of `_` and digits is the object's id, so `Shape_12` becomes `Shape_` with a new id. A name without such a tail does not get one, and a tail that is not only digits (`Wave_2b`) stays as is. Audio tracks are renamed the same way

Objects copied in Prefab Mode are pasted back into the template, not into the level

> [!caution] Caution
> The buffers are cleared when a level loads. All ids and frames in them belong to the level that was open

## Prefabs

For something you need many times and want to change everywhere at once

A prefab is a template and its placements. When you give a placement a template, the placement gets real copies of its objects with permanent ids. The level file stores only the placement itself: the template, the ids of the copies and your overrides. The copies are rebuilt from the template every time the level loads

An edit to the template spreads to every placement that references it.
An edit to a copy in one placement (outside template editing) is recorded as an override of that instance only.
Overrides survive later edits to the template. That is why a prefab works for variations too, not only for clones

Prefabs can be nested inside each other. A nested template can be edited from inside another: templates open on top of each other and close in reverse order

### A prefab from a selection

Select objects and press `Ctrl+G` (`Create Prefab From Selection`). The same action is also:
- in the command palette
- in the viewport's context menu, while something is selected
- in a hierarchy row's menu, as `Create Prefab From This`
- in the level settings, the `Prefabs` tab, `From Selection`

The selected objects move into a new template, one placement of it takes their place, and that placement is selected. It is one operation to undo.
One object gives the template its name. Several objects give a template named `Prefab`

A placement and an object that belongs to it cannot be packed again. Their menus offer `Open in Prefab` instead, and their template opens.
In Prefab Mode packing is not available

## Generators and modifiers

**Generators** create content by a rule: a spiral, a grid, a fractal, a wave, a rain of bullets, a fan of beams. You set a window of frames, a layer and a seed and get objects. The estimate of the result is visible before you press anything

**Modifiers** work the same way, but with what already exists: they fit spans, spread them apart, quantise keyframes, recompute the framerate, delete content in a window

## Between levels: the device libraries

Everything above works inside one level. Only the device libraries and collections carry over from level to level

Themes, effects, shapes and prefabs are exported from a level and imported into another.
The libraries sit next to the levels folder, so a level you send carries its own copy

A collection holds resources of any of seven kinds, textures, fonts and audio included, and travels as an archive or through Steam Workshop. More - [[16_library-and-collections]]

Next: [[3_speed-and-shortcuts|Speed and shortcuts]], [[4_level-folder-and-backups|The level folder and backups]]
