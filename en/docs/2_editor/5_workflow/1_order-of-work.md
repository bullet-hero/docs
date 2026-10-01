---
title: The order of work
date: 2026-10-01
tags: [level_author]
---

# The order of work

First the track, the fps, the beat map and the markers, then a skeleton of plain shapes and its playtest. Decoration, the theme and effects come last

The steps go from the most expensive to the cheapest.
The earlier a step, the more it costs to redo once everything is built on it

## The foundation

1. **The finished track.** Converted, normalised, trimmed. Everything else is measured from it. Replacing the track later shifts every frame of the level
2. **FPS and level length.** Both can be changed, but the fps is the expensive one: after a change every keyframe is recomputed. The default is `60`, and there is usually no reason to change it
3. **The beat map.** Segments, tempo, offset, time signature. While the beat map is wrong, nothing snaps to the beats correctly. Everything placed before it will have to be moved later
4. **Markers on the structure.** Intro, verse, chorus, break, drop, outro. It is ten minutes of work, and the markers are visible on every timeline

## The skeleton and its playtest

5. **The skeleton.** The main patterns in plain shapes. No decoration, no theme, no effects
6. **Playtest the skeleton.** Before decoration: once a section is decorated, you will not want to delete it

> [!caution] Caution
> The skeleton is the stage where the level is actually designed. And it is the stage most often skipped. A skeleton that is not fun to play will not become fun through decoration. It will become a decorated level that is not fun to play

## Filling it out

7. **Content.** Fill out the patterns and add the objects that so far were only implied
8. **Themes and colour.** From the very start, set colours as references to the theme, not as fixed values
9. **Effects and post-processing.** Last. They are the easiest to overdo, and they are hard to judge while the level is still changing
10. **Metadata.** Name, description, authors, age rating. Fill in a resource's card as soon as you add the resource, not at this step

## What is cheap and what is expensive to change

**Cheap to change at the end:** colours through the theme, decoration, post-processing, the level's description

**Expensive:** the fps, the track, the beat map and the hierarchy

> [!warning] Warning
> Changing an object's parent changes its transform, lifetime and draw order at once. That is why restructuring a finished level rarely takes just one edit

Save at every step. What autosave and undo cover - [[4_not-losing-work]]

Next: [[2_reuse|Reuse: prefabs, copying, generators]], [[4_not-losing-work|Not losing your work]]
