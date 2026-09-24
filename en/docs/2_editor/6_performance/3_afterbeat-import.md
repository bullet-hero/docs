---
title: Importing from Afterbeat
date: 2026-09-24
tags: [level_author]
---

# Importing from Afterbeat

What crosses over from Project Arrhythmia, what does not, and what to repair by hand afterwards

**Afterbeat**, formerly **Project Arrhythmia**, is this game's closest relative in the genre.
The import works both ways: levels, metadata, themes and prefabs (`vgd`, `vgm`, `vgt`, `vgp`) are read and written

How the conversion works inside, and every field it maps - [[9_afterbeat-interop]]

## Import and export

**A level coming in:** create a new level with the `Afterbeat Level` generator and pick the level's folder with `Choose Afterbeat Level Folder...`. The folder import is not available on Android yet

**A level going out:** `Export to Afterbeat` in the level settings

**Themes and prefabs** cross one at a time:
- `Import .vgt` and `Export .vgt` sit next to the level's themes
- `Import .vgp` and `Export .vgp` sit next to the level's prefabs

## What crosses

**Well:** objects, their lifetimes, the hierarchy, transform keyframes, themes and colours, prefabs

**Badly or not at all:** everything that depends on how the other engine is built. Hierarchy and draw order work differently here. The event side differs. Some visual capabilities of one game have no counterpart in the other

The level loads either way. What did not cross is listed in the conversion report after the import.
The full list of what the converter never carries, in either direction, is in [[9_afterbeat-interop#Limits|the SDK's limits]]

## After an import

1. Run the `Rules` check and read what it found
2. Watch the level end to end without playing it, at more than one speed
3. Check readability. The renderer and the avatar size are different here, so what read clearly there may not read here
4. Check performance. Objects are built differently, so a level that ran there can cost something else here

## Rights

> [!caution] Caution
> An imported level is somebody else's work. Locally you can do whatever you like with it. To publish it, the same rules apply as to any content that is not yours. More - [[2_legal-resource-paths|Two ways a resource qualifies]]

> [!caution] Caution
> Licensing, age rating and attribution are lost on export: `.vgm` has no fields for them. A level exported to Afterbeat carries no record of whose resources it uses. Keep that record yourself

## Other games

There is no *Geometry Dash* import and none is planned yet. Level logic there is too different: an honest import needs this engine to get more flexible first. No date is given for that

*Just Shapes and Beats* has neither an open format nor an editor for players. There is nothing to import from it

Next: [[3_how-the-editor-thinks|How the editor thinks]], [[1_level-budget|The level's budget]]
