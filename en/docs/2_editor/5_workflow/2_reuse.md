---
title: "Reuse: prefabs, copying, generators"
date: 2026-09-24
tags: [level_author]
---

# Reuse: prefabs, copying, generators

Four tools that all mean "do not build this twice", and which one fits which job

Four tools overlap here, and picking the wrong one costs an evening

**Copy and paste** - for a shape you want again a few times, with no relationship to the original afterwards. There are five independent buffers, one per timeline, and which one a copy lands in is decided by the timeline you are looking at. Clips copied on one timeline can never be pasted over keys on another

> [!info] Worth knowing
> Duplicate writes to no buffer at all. Clobbering what you copied earlier is the surprise every other editor avoids by keeping the two apart

> [!caution] Caution
> Buffers are cleared when a level loads, because every id and frame in them belongs to the level that was open

**Prefabs** - for a thing you want many times AND want to change everywhere at once. A prefab is a template plus placements of it. A placement is materialised rather than resolved at load time: the moment you point it at a template, real permanent copies of its objects are written into the level

Editing the template re-propagates to every placement referencing it. Editing a materialised child outside template editing records a per-instance override instead

> [!tip] Tip
> Overrides survive re-propagation, which is what makes a prefab usable for variations rather than only for clones

> [!info] Worth knowing
> Nested prefabs work, and so does editing one from inside another - templates open on top of each other and close back in the same order

**Generators** - for content described by a rule rather than placed by hand: a spiral, a grid, a fractal, a wave, a rain of bullets, a fan of lasers. You give a window of frames, a layer and a seed, and get objects. The estimate is shown before you press anything

**Modifiers** - the same machinery pointed at content that already exists: fit spans, stagger them, quantise keys, remap the framerate, remove content in a window

> [!tip] Recommendation
> Ask two questions. Will these need changing all at once later? If yes, a prefab, whatever the count. Can this be described by a rule rather than drawn? If yes, a generator, even for eight objects - a generator run is one operation to undo, and eight hand-placed objects are eight chances to misalign one

**The device-wide libraries** are the fifth kind of reuse and the only one that crosses levels. Themes, effects, shapes and prefabs can be exported out of a level and imported into another. They live beside the levels folder, so a level you send carries its own copy

Next: [[3_speed-and-shortcuts|Speed and shortcuts]], [[4_level-folder-and-backups|The level folder and backups]]
