---
title: Generators
date: 2026-09-24
tags: [level_author]
---

# Generators

What generators are and what each of the built-in ones makes

## Generators

Procedural content, run against the level as one undoable operation

> [!info] Worth knowing
> There are two families. **Generators** (*gen_*) create content - bullet waves, radial patterns, the font cache, an Afterbeat level import. **Modifiers** (*mod_*) rewrite what is already there - fitting spans, quantising keyframes

Each generator declares its own fields and the form is built from them, so no interface is written per generator

> [!caution] Caution
> Anything that rewrites or deletes existing content asks for confirmation first

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Levels

### Empty Level

Clears the level to nothing. Everything authored is removed, which is what makes it the one to reach for when starting over rather than editing

More: [[2_first-level|Your first level: the route]]

### Level From Audio File

Starts a level from a track: brings the audio in, sizes the level to its length and leaves you at the beginning of an empty timeline

More: [[2_preparing-the-track|Preparing the track]]

### Import Afterbeat Level

Converts a level from Afterbeat (formerly Project Arrhythmia) into this format

> [!warning] Warning
> Not everything crosses. What did not is listed in the conversion report afterwards - the level loads either way, and the report says where it differs from the original

More: [[3_afterbeat-import|Importing from Afterbeat]]

### Import Level Archive

Opens a level archive written by this game - a .tar.gz or a .zip, either of them optionally behind a password - and builds a level out of what is inside it

What the file is gets read from its bytes rather than from its name, so an archive somebody renamed still opens. 7z is recognised and refused by name: this build does not read that format yet

> [!tip] Tip
> An archive written by an older build opens as today's format. The document is migrated on the way in, so nothing has to be converted first

> [!warning] Warning
> The imported level is given an id of its own by default, so it cannot overwrite a level already on this machine. Turn that off only to bring back a level this machine used to hold

## Bullets

### Bullet Wave

A row of bullets advancing together. The staple pattern, and the one worth reading first: its parameters name the ideas the other bullet generators reuse

More: [[1_readability-and-fairness|Readability and fairness]]

### Bullet Spiral

Bullets emitted along a rotating arm, producing the classic spiral wall

More: [[1_readability-and-fairness|Readability and fairness]]

### Bullet Rain

Bullets falling across an area over a stretch of time. Density and spread are parameters. Where each one lands is drawn from the level's seed, so a run is reproducible

More: [[1_readability-and-fairness|Readability and fairness]]

### Homing Bullets

Bullets that curve towards where the player is expected to be. The curve is authored, not computed at playback: the result stays identical on every device

More: [[1_readability-and-fairness|Readability and fairness]]

### Laser Sweep

A beam that sweeps across the field. Its telegraph and its lethal phase are separate objects, so the warning can be drawn without being able to kill

More: [[1_readability-and-fairness|Readability and fairness]]

## Geometry

### Polygon

Places shapes around the vertices or edges of a regular polygon

More: [[2_reuse|Reuse: prefabs, copying, generators]]

### Radial

Distributes copies around a circle. The base of most symmetric patterns

More: [[2_reuse|Reuse: prefabs, copying, generators]]

### Spiral

Distributes copies along a spiral, with radius and angle advancing together

More: [[2_reuse|Reuse: prefabs, copying, generators]]

### Grid

Fills a rectangle with evenly spaced copies of a shape

More: [[2_reuse|Reuse: prefabs, copying, generators]]

### Fractal

Repeats a shape into itself at shrinking scales. Depth costs objects exponentially, so raise it a step at a time

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Audio and effects

### Audio Waveform

Builds objects that trace the shape of an audio track, so the level visibly follows what is heard

More: [[2_reuse|Reuse: prefabs, copying, generators]]

### Beat Flash

Places a flash on every beat. The beats come from the level's beat map, and from its markers when there is no map - so what flashes is exactly what you see on the grid

More: [[2_rhythm-and-structure|Rhythm and structure]]

## Resources and service

### Texture Objects

Turns an image into objects, one per cell, so a picture becomes level content that can be animated like anything else

More: [[3_images-and-fonts|Images and fonts]]

### Font Cache

Collects every character the level's text actually uses and bakes it, so no glyph has to be prepared the first time it appears

> [!tip] Recommendation
> Run it after the text is final. A character added later and not re-baked costs a hitch the moment it is first shown

More: [[3_images-and-fonts|Images and fonts]]

### Capacity Hint

Writes the level's advisory limits - how many objects and effects it expects to need at once

> [!info] Worth knowing
> It changes nothing you can see. The runtime uses it to reserve buffers up front instead of growing them mid-level, which is where a stutter would otherwise come from

More: [[1_level-budget|The level's budget]]
