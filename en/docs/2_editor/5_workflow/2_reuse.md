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

There are five clipboard buffers, one per timeline. A copy lands in the buffer of the timeline you are looking at.
Clips copied on one timeline can never be pasted over keys on another

Duplicate writes to no buffer at all. What you copied earlier is not lost

> [!caution] Caution
> Buffers are cleared when a level loads. Every id and frame in them belongs to the level that was open

## Prefabs

For a thing you want many times and want to change everywhere at once

A prefab is a template plus placements of it. When you point a placement at a template, real permanent copies of its objects are written into the level. They are not rebuilt at load time, they are already in the level

Editing the template spreads to every placement that references it.
Editing a copy in one placement (outside template editing) records an override for that instance only.
Overrides survive later edits to the template. That is what makes a prefab usable for variations, not only for clones

Prefabs can be nested. A nested template can be edited from inside another: templates open on top of each other and close in reverse order

## Generators and modifiers

**Generators** create content from a rule: a spiral, a grid, a fractal, a wave, a rain of bullets, a fan of lasers. You give a window of frames, a layer and a seed, and get objects. The estimate is shown before you press anything

**Modifiers** do the same with content that already exists: fit spans, stagger them, quantise keys, remap the framerate, remove content in a window

## Across levels: the device-wide libraries

Everything above works inside one level. Only the device-wide libraries cross from one level to another

Themes, effects, shapes and prefabs are exported out of a level and imported into another.
The libraries live beside the levels folder, so a level you send carries its own copy

Next: [[3_speed-and-shortcuts|Speed and shortcuts]], [[4_level-folder-and-backups|The level folder and backups]]
