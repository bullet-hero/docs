---
title: Generators
date: 2026-10-01
tags: [level_author]
---

# Generators

A generator creates content and applies it to the level in one operation that can be undone in one step. Every generator is run from the "Generators" window on the toolbar

## Generators

A generator's form is built from its own fields. There is no separate interface for each generator

> [!caution] Caution
> Anything that rewrites or deletes existing content asks for confirmation first

> [!info] Worth knowing
> There are two families. **Generators** (*gen_*) create content: bullet waves, radial patterns, a font cache, an Afterbeat level import. **Modifiers** (*mod_*) change what is already there: fitting spans, quantizing keyframes. Modifiers are described separately - [[9_modifiers]]

More - [[2_reuse]]

## The generators window

Content generators and modifiers are run from the `Generators` window on the toolbar. Its `Base Parameters` block is shared by all generators: `Start Frame`, `End Frame`, `Layer` and `Seed`. They belong to the window, not to any one generator

How the block behaves:
- The window opens on one second from the playhead, with the seed at 0. `Random` rolls a new seed
- The frames stay inside the timeline you are working on, from frame 1 to its last frame. In prefab mode that is the template's length
- Editing `Start Frame` pushes `End Frame` along with it. Editing `End Frame` stops at `Start Frame`. They never cross
- `Layer` stays inside the allowed range of layers
- Each frame field has a pin that holds it at the edge of the timeline. `Whole Level` sets both, and the window runs from frame 1 to the last frame. The fields stay editable, and typing into a field removes the pin from that edge

`Group Into One Object` and `Layer Per Object` are on by default. The group is named after the generator. Both affect only content generators: a modifier creates nothing, so there is nothing to group

Generated content never goes under the selected object. It lands at the top level of the scope or in its own group

Before you press `Generate`, the window shows what a run will add. The button is unavailable, and the reason is written instead of the estimate, if:
- the generator needs the whole level and you are in prefab mode. These are Beat Flash, Font Cache, Capacity Hint and Remap Framerate
- the generator needs a selection and nothing is selected
- after the run the level would have more than 262 144 objects
- a content generator would add nothing. A modifier is not rejected for this

A generator that needs external data (an audio track, beats, an image) creates nothing without it, and the estimate says so

`Generate` closes the window. The generated content stays selected, in the same undo step

The window remembers which generator you were on and which parameters you entered when it is closed and opened again. `Reset` returns the defaults

## Levels

### Empty Level

Clears the level completely. Everything created is deleted.
Suits starting over rather than editing

`Pin Screen Aspect` (on by default) puts a keyframe with a fixed 16:9 on the `Screen Limit` track at the first frame

More - [[2_first-level]]

### Level From Audio File

Starts a level from a track.
Connects the audio, fits the level's length to the track and puts you at the start of an empty timeline

`Pin Screen Aspect` (on by default) puts a keyframe with a fixed 16:9 on the `Screen Limit` track at the first frame

More - [[2_preparing-the-track]]

### Import Afterbeat Level

Converts an Afterbeat level (formerly *Project Arrhythmia*) into the Bullet Hero format

> [!warning] Warning
> Not everything carries over. The level loads in any case. What did not carry over and how the level differs from the original is written in the conversion report

More - [[3_afterbeat-import]]

### Import Level Archive

Builds a level from an archive this game made.
Formats: `.tar.gz` and `.zip`. Both may be password protected

The file type is detected by content, not by name. A renamed archive still opens.
The game recognises `7z` but does not read it yet and rejects it

> [!tip] Tip
> An archive from an old build opens without preparation. The game converts it to the current format itself on import

> [!warning] Warning
> By default an imported level gets a new id. So it does not overwrite a level already on this device. Clear this checkbox only to restore a level that used to be on this device

## Bullets

More on all bullet generators - [[1_readability-and-fairness]]

### Bullet Wave

A row of bullets that move together.
The basic pattern, and the one to start with. Its parameters repeat in the other bullet generators

### Bullet Spiral

Bullets fly out along a rotating ray. The result is the classic spiral wall

### Bullet Rain

Bullets fall onto an area over a set time.
Density and scatter are adjustable.
Where each bullet falls comes from the level seed. So a run can be repeated exactly

### Homing Bullets

Bullets curve toward where the player is expected to be.
The path is calculated in advance, not during play. So the result is the same on any device

### Laser Sweep

A beam passes across the field.
The warning and the damaging phase are different objects. So the warning can be shown, and it does not kill

## Geometry

More on all geometry generators - [[2_reuse]]

### Polygon

Places shapes on the vertices or edges of a regular polygon

### Radial

Places copies around a circle. The basis of most symmetric patterns

### Spiral

Places copies along a spiral. The radius and the angle grow together

### Grid

Fills a rectangle with copies of a shape at equal distances

### Fractal

Repeats a shape inside itself, smaller each time.
The object count grows exponentially with depth. Raise the depth one step at a time

## Audio and effects

### Audio Waveform

Builds objects from the shape of an audio track. The level visibly follows what is heard

More - [[2_reuse]]

### Beat Flash

Puts a flash on every beat.
The beats come from the level's beat map. If there is no map, from the markers.
So exactly what you see on the grid is what flashes

More - [[2_rhythm-and-structure]]

## Resources and utilities

### Texture Objects

Turns an image into objects, one per cell.
The picture becomes level content and is animated like everything else

More - [[3_images-and-fonts]]

### Font Cache

Collects every character the level's text uses and bakes them in advance.
Then no character is prepared at the moment it is first shown

> [!tip] Recommendation
> Run it when the text is done. A character added later without rebaking causes a stutter the first time it is shown

More - [[3_images-and-fonts]]

### Capacity Hint

Records the level's recommended limits: how many objects and effects it needs at the same time

> [!info] Worth knowing
> It does not affect what is shown. The game allocates buffers for these limits in advance. Otherwise the buffers would grow in the middle of the level, and that would cause a stutter

More - [[1_level-budget]]
