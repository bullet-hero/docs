---
title: The order of work
date: 2026-09-24
tags: [level_author]
---

# The order of work

What to do before what, and which decisions are cheap now and expensive later

The steps go from the most expensive to the cheapest.
The earlier a step, the more it costs to redo once everything else is built on it

## The foundation

1. **The track, finished.** Converted, normalised, trimmed. Everything else is measured against it. Replacing the track later moves every frame in the level
2. **The level's fps and length.** Both can be changed, but the fps is the expensive one: changing it recomputes every key. The default is `60`, and there is rarely a reason to move it
3. **The beat map.** Segments, tempo, offset, bars. Until the beat map is right, nothing snaps to the beats correctly. Everything placed before it has to be nudged afterwards
4. **Markers on the structure.** Intro, verse, chorus, break, drop, outro. It is ten minutes of work, and the markers show on every timeline

## The skeleton and its playtest

5. **The skeleton.** The main patterns in plain shapes. No decoration, no theme, no effects
6. **Playtest the skeleton.** Before decoration: once a section is decorated, you will not want to delete it

> [!caution] Caution
> The skeleton is the stage where the level is actually designed. It is also the stage people skip most often. A skeleton that is not fun does not become fun with decoration. It becomes a decorated level that is not fun

## Filling it out

7. **Content proper.** Fill out the patterns and add the objects that were only implied
8. **Themes and colour.** From the start, set colours as references to the theme, not as fixed values
9. **Effects and post-processing.** Last. They are the easiest thing to overdo, and they are hard to judge while the level is still changing
10. **Metadata.** Name, description, authors, age rating. Fill in a resource's record when you add the resource, not at this step

## Cheap and expensive changes

**Cheap to change late:** colours through the theme, decoration, post-processing, the level's description

**Expensive:** the fps, the track, the beat map and the hierarchy

> [!warning] Warning
> Reparenting an object changes its transform, its lifetime and its draw order at once. So restructuring a finished level is rarely one edit

Save at every step. What autosave and undo cover - [[4_not-losing-work]]

Next: [[2_reuse|Reuse: prefabs, copying, generators]], [[4_not-losing-work|Not losing your work]]
