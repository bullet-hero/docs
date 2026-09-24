---
title: Working in the editor
date: 2026-09-24
tags: [level_author]
---

# Working in the editor

How to work in the editor fast and without losing work, from the first object to sharing

This section is about habits rather than design: in what order to build, how not to build the same thing twice, how to move fast, how to keep what you made and how to hand the result to another person. What makes a level good to play is the subject of the section [[2_editor/4_craft/index]]. It is written for level authors who have already built a first level and now spend hours in the editor rather than minutes

## Order by the cost of redoing

The order of work is sorted by how expensive each step is to redo once the next ones rest on it. The track, the level's fps and the beat map come first: replacing the track moves every frame in the level, and changing the fps means recomputing every key. Colours through the theme, decoration, post-processing and the description come last, because they stay cheap to change at any point

The step that gets skipped is the skeleton: the main patterns in plain shapes, played through before anything is added on top. A skeleton that is not fun does not become fun with decoration

## Nothing saves for you

> [!caution] Caution
> Autosave is configured in the settings but does not run yet. `Ctrl+S` is yours to press, and nothing in the editor will press it for you

Undo covers edits to the level and only those. It does not un-write a saved file, and two actions touch the disk with no undo at all: changing the level's file format (writing `Blob` deletes the `Json` it replaced) and deleting a level. The only backup method is a copy of the level folder, and it is a complete snapshot because the whole level is one folder

## Do not build it twice

Copy and paste, prefabs, generators and modifiers overlap, and the choice comes down to two questions:
- will these objects need changing all at once later? Then a prefab, whatever the count
- can the content be described by a rule rather than drawn? Then a generator, even for eight objects, because one run is one operation to undo

Themes, effects, shapes and prefabs can also be exported into device-wide libraries, which is the only kind of reuse that crosses from one level to another

## Speed, testing and sharing

**Every shortcut is a setting** and can be rebound in the Keybindings tab of Settings. The biggest savers are the command palette (`Ctrl+Shift+P`), content search (`Ctrl+F`), ping and the arrow keys on a timeline

**A bot plays the level with your own controls** and cannot do anything a player cannot. It is a readability check rather than a difficulty check: a place where it is hit again and again is usually a hazard with no room to leave

**A level travels as its folder** or as an archive made with standard tools (tar, zip, gpg), so the other side needs nothing special to open it

> [!tip] Recommendation
> `Ctrl+S` after every section you finish, a copy of the folder before every restructure, and the Rules check before you call the level done
