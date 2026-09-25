---
title: Generators
date: 2026-09-24
tags: [level_author]
---

# Generators

What each of the built-in generators does

## Generators

A generator creates content and applies it to the level as one operation. One undo step reverts it

A generator's form is built from its own fields. No interface is written per generator

> [!caution] Caution
> Anything that rewrites or deletes existing content asks for confirmation first

> [!info] Worth knowing
> There are two families. **Generators** (*gen_*) create content: bullet waves, radial patterns, the font cache, an Afterbeat level import. **Modifiers** (*mod_*) change what is already there: fitting spans, quantising keyframes. Modifiers have their own page - [[9_modifiers]]

More - [[2_reuse]]

## The generators window

Content generators and modifiers run from the `Generators` window on the toolbar. Every generator shares its `Base Parameters` block: `Start Frame`, `End Frame`, `Layer` and `Seed`. They belong to the window, not to any one generator

How the block behaves:
- The window opens on one second from the playhead, with the seed at 0. `Random` rolls a new seed
- The frames stay inside the timeline you are working on, from frame 1 to its last frame. In Prefab Mode that is the template's length
- Editing `Start Frame` pushes `End Frame` along. Editing `End Frame` stops it at `Start Frame`. The two never cross
- `Layer` stays inside the legal layer range
- Each frame field has a pin that holds it on the timeline's edge. `Whole Level` sets both pins, so the window runs from frame 1 to the last frame. The fields stay editable, and typing into one unpins that edge

`Group Into One Object` and `Layer Per Object` are on by default. The group is named after the generator. Both apply to content generators only: a modifier creates nothing to group

A generated run is never put under the selected object. It lands at the top level of the scope, or inside its own group

The window shows what the run will add before you press `Generate`. The button is disabled, with the reason shown instead, when:
- the generator needs the whole level and you are in Prefab Mode. That is Beat Flash, Font Cache, Capacity Hint and Remap Framerate
- it needs a selection and nothing is selected
- the run would take the level past 262,144 objects
- a content generator would add nothing. A modifier is never refused for that

A generator that reads outside data (an audio track, the beats, an image) produces nothing without it, and the estimate says so

`Generate` closes the window. What was generated is left selected, in the same undo step

The window remembers the generator you were on and the parameters you typed when you close and reopen it. `Reset` puts the defaults back

## Levels

### Empty Level

Clears the level completely. Everything authored is removed.
Use it when you start over rather than edit

More - [[2_first-level]]

### Level From Audio File

Starts a level from a track.
Brings the audio in, sizes the level to the track and puts you at the start of an empty timeline

More - [[2_preparing-the-track]]

### Import Afterbeat Level

Converts a level from Afterbeat (formerly *Project Arrhythmia*) into the Bullet Hero format

> [!warning] Warning
> Not everything crosses over. The level loads either way. What did not cross and where the level differs from the original is listed in the conversion report

More - [[3_afterbeat-import]]

### Import Level Archive

Builds a level from an archive written by this game.
Formats: `.tar.gz` and `.zip`. Either can be behind a password

The file type is read from its contents, not its name. A renamed archive still opens.
`7z` is recognised, but this build does not read it yet and refuses it

> [!tip] Tip
> An archive from an older build opens with no preparation. The game migrates it to the current format on import

> [!warning] Warning
> By default the imported level gets a new id. So it cannot overwrite a level already on this device. Turn that off only to bring back a level this device used to hold

## Bullets

More on all bullet generators - [[1_readability-and-fairness]]

### Bullet Wave

A row of bullets moving together.
The staple pattern, and the one to start with. Its parameters recur in the other bullet generators

### Bullet Spiral

Bullets fly out along a rotating arm. The result is the classic spiral wall

### Bullet Rain

Bullets fall across an area over a set stretch of time.
Density and spread are parameters.
Where each bullet lands comes from the level's seed. So a run can be repeated exactly

### Homing Bullets

Bullets curve towards where the player is expected to be.
The path is computed in advance, not during play. So the result is identical on every device

### Laser Sweep

A beam sweeps across the field.
The telegraph and the lethal phase are separate objects. So the warning can be shown without being able to kill

## Geometry

More on all geometry generators - [[2_reuse]]

### Polygon

Places shapes on the vertices or edges of a regular polygon

### Radial

Places copies around a circle. The base of most symmetric patterns

### Spiral

Places copies along a spiral. Radius and angle grow together

### Grid

Fills a rectangle with evenly spaced copies of a shape

### Fractal

Repeats a shape inside itself, smaller each time.
The object count grows exponentially with depth. Raise the depth one step at a time

## Audio and effects

### Audio Waveform

Builds objects in the shape of an audio track. The level visibly follows what is heard

More - [[2_reuse]]

### Beat Flash

Places a flash on every beat.
The beats come from the level's beat map. With no map, they come from the markers.
So what flashes is exactly what you see on the grid

More - [[2_rhythm-and-structure]]

## Resources and service

### Texture Objects

Turns an image into objects, one per cell.
The picture becomes level content and animates like anything else

More - [[3_images-and-fonts]]

### Font Cache

Collects every character the level's text uses and bakes it in advance.
Then no glyph has to be prepared the first time it appears

> [!tip] Recommendation
> Run it when the text is final. A character added later and not re-baked causes a hitch the first time it is shown

More - [[3_images-and-fonts]]

### Capacity Hint

Writes the level's advisory limits: how many objects and effects it needs at once

> [!info] Worth knowing
> It changes nothing you can see. The game reserves buffers for these limits up front. Otherwise the buffers would grow mid-level, and that would cause a stutter

More - [[1_level-budget]]
