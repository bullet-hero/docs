---
title: Importing from Afterbeat
date: 2026-09-24
tags: [level_author]
---

# Importing from Afterbeat

What crosses over from Project Arrhythmia, what does not, and what to repair by hand afterwards

**Afterbeat**, formerly **Project Arrhythmia**, is this game's closest relative in the genre. The import works both ways: `vgd`, `vgm`, `vgt` and `vgp` are read and written - levels, metadata, themes, prefabs

It runs as an ordinary level generator: pick it when creating a level and point it at the file

**What crosses well:** objects, their lifetimes, the hierarchy, transform keyframes, themes and colours, prefabs

**What crosses badly or not at all:** everything that depends on how the other engine is built. Hierarchy and draw order work differently here, the event side differs, and some visual capabilities of one game have no counterpart in the other

> [!tip] Tip
> The full list of what crosses the border lives in the importer itself, which carries its own description. That description is more precise than any summary

**After an import:**
1. Run the level's validation and read what it found
2. Watch the level end to end without playing it, at more than one speed
3. Check readability - what read clearly in another game, with another renderer and another avatar size, may not read here
4. Check performance - objects are built differently, so a level that ran there can cost something else here

> [!info] Worth knowing
> There is no Geometry Dash import and none is planned yet. Level logic there is different enough that an honest import needs this engine to get more flexible first, and no date is being given for that

> [!info] Worth knowing
> Just Shapes and Beats has no open format and no editor for players, so there is nothing there to import out of

> [!caution] Caution
> An imported level is somebody else's work. Locally you can do whatever you like with it, but the moment you want to publish it, the same rules apply as to any content that is not yours - see [[2_legal-resource-paths|Two ways a resource qualifies]]

Next: [[3_how-the-editor-thinks|How the editor thinks]], [[1_level-budget|The level's budget]]
