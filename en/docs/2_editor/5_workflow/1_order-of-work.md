---
title: The order of work
date: 2026-09-24
tags: [level_author]
---

# The order of work

What to do before what, and which decisions are cheap now and expensive later

The order below is sorted by how expensive each step is to redo once the next ones are built on top of it

## The foundation

1. **The track, finished.** Converted, normalised, trimmed. Everything after this is measured against it, so replacing the file later moves every frame in the level
2. **The level's fps and length.** Both are changeable, but the fps is the expensive one - changing it later means recomputing every key. `60` is the default and there is rarely a reason to move
3. **The beat map.** Segments, tempo, offset, bars. Nothing downstream snaps correctly until this is right, and everything placed before it has to be nudged afterwards
4. **Markers on the structure.** Intro, verse, chorus, break, drop, outro. Ten minutes of work, visible on every timeline

## The skeleton and its playtest

5. **The skeleton.** The main patterns, plain shapes, no decoration, no theme, no effects
6. **Playtest the skeleton.** Before decoration, because decoration is what makes you reluctant to delete a section

> [!caution] Caution
> The skeleton is the stage where the level is actually designed, and the stage people skip. A skeleton that is not fun does not become fun with decoration on top - it becomes a decorated level that is not fun

## Filling it out

7. **Content proper.** Fill out the patterns, add the objects that were only implied
8. **Themes and colour.** References rather than literals from the start
9. **Effects and post-processing.** Last, because they are the easiest thing to overdo and the hardest to judge while the level is still changing
10. **Metadata.** Name, description, authors, age rating. Resource records are not part of this step - fill each one in when you add its resource

## Cheap and expensive changes

**Cheap to change late:** colours through the theme, decoration, post-processing, the level's description

> [!warning] Warning
> Expensive: the fps, the track, the beat map and the hierarchy. Reparenting an object changes its transform, its lifetime and its draw order at once, so restructuring a finished level is rarely one edit

Save at every step. What autosave and undo cover, and what they do not, is on the page [[4_not-losing-work]]

Next: [[2_reuse|Reuse: prefabs, copying, generators]], [[4_not-losing-work|Not losing your work]]
