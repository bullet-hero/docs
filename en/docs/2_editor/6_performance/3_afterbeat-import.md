---
title: Importing from Afterbeat
date: 2026-10-01
tags: [level_author]
---

# Importing from Afterbeat

A level from Afterbeat always loads, but not everything carries over: the report after the import lists what was lost. Then check the rules, readability and performance

**Afterbeat**, formerly **Project Arrhythmia**, is this game's closest relative in the genre.
The import works both ways: levels, metadata, themes and prefabs (`vgd`, `vgm`, `vgt`, `vgp`) are read and written

How the conversion works inside and which fields it maps to what - [[9_afterbeat-interop]]

## Import and export

**A level into the game:** create a new level with the `Afterbeat Level` generator and pick the level folder with `Choose Afterbeat Level Folder...`. Folder import is not available on Android yet

**A level out of the game:** the `Publication` tab in the level settings, the `Afterbeat` method. On a computer only. More - [[17_publishing#Afterbeat]]

**Themes and prefabs** carry over one at a time:
- `Import .vgt` and `Export .vgt` - next to the level's themes
- `Import .vgp` and `Export .vgp` - next to the level's prefabs

## What carries over

**Well:** objects, their lifetimes, the hierarchy, transform keyframes, themes and colours, prefabs

**Badly or not at all:** everything that depends on how the other engine is built. The hierarchy and draw order work differently here. The event side is different. Some visual features of one game have no counterpart in the other

The level loads in any case. What did not carry over is listed in the conversion report after the import.
The full list of what the converter does not carry in either direction is in [[9_afterbeat-interop#Limitations|the SDK limitations]]

## After the import

1. Run the `Rules` check and read what it found
2. Watch the whole level without playing, at different speeds
3. Check readability. The renderer and the character size are different here, and what read well there may not read here
4. Check performance. Objects are built differently, and a level that ran there may cost something different here

## Rights

> [!caution] Caution
> An imported level is someone else's work. Locally you can do anything with it. For publishing, the same rules apply as to any content that is not yours. More - [[2_legal-resource-paths|Two ways to a legal resource]]

> [!caution] Caution
> Export loses licenses, the age rating and attribution: `.vgm` has no fields for them. A level exported to Afterbeat does not remember whose resources it uses. Keep that record yourself

## Other games

There is no import from *Geometry Dash*, and none is planned yet. The level logic there is too different: for an honest import the engine first has to become more flexible. There is no date

*Just Shapes and Beats* has neither an open format nor an editor for players. There is nothing to import from it

Next: [[3_how-the-editor-thinks|How the editor works]], [[1_level-budget|Level budget]]
