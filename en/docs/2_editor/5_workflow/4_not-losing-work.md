---
title: Not losing your work
date: 2026-09-24
tags: [level_author]
---

# Not losing your work

What autosave and undo cover and what they do not, which actions have no undo at all, and how to get a level back

Three things stand between an edit and its loss: autosave, undo and a copy of the level folder. Each covers something the others do not

## Autosave

Autosave is on by default. Once there are unsaved edits it counts `60` seconds, then writes a copy of the level to `backups/<level id>/` in the game's folder, outside `levels`, and saves the level itself. An editor left open with nothing changed writes nothing

`25` copies are kept, the oldest is dropped first. A copy holds the level alone - no metadata, no track, no images - and it survives the level being deleted. A copy of a protected level is protected with that level's password. The switch, the interval and the number of copies are in Settings, `Game Editor`

**Restoring** is in Level Settings, the Dangerous Zone tab, `Restore from backup`: copies are listed newest first, named by the moment they were taken. The file being replaced is copied into `backups` first, so a restore can itself be undone

## What undo covers

Edits to the level, and only those. Every change to objects, keys, resources, themes, prefabs and settings goes through one operation buffer

Not covered, because none of it is a change to the level:
- which gizmo, which timeline tool, whether snapping is on, whether the grid is on
- panel layout, which tab is open, where the playhead is
- the clipboard buffers
- the session's regenerated seed. Reloading the level resolves it from scratch again
- **saving**. Undo walks the model back, it does not un-write a file

## What has no undo at all

Two things touch the disk directly:
- **Changing the level's file format.** Writing the level as `Blob` deletes the `Json` it replaced, and a blob cannot be read or repaired by eye
- **Deleting a level.** It is behind a dangerous-actions panel for that reason

## The Raw tab

The Raw tab is the last resort and it validates nothing. It shows the entire saved file as a tree of fields and applies no rules, no clamps and no checks. Its whole session commits as one undoable operation, so getting out is easy

> [!caution] Caution
> What you wrote inside the Raw tab was never checked by anything. Keep a copy of the level folder beside you, see [[4_level-folder-and-backups#Backups and recovery]]

## Rules

Rules is the check worth running. It reports what validation found - broken references, duplicate ids, parent cycles, prefabs nested too deep, overlapping beat segments

No finding carries a repair, and that is deliberate. Every one of them is a content decision only you can make, and an automatic fix would quietly pick one of several valid answers

An overhanging child span is not reported. That is legal authored data behaving as designed. To fit lifetimes, run the `span-fit` modifier

## The habit

> [!tip] Recommendation
> `Ctrl+S` after every section you finish, a copy of the level folder before every restructure, and Rules before you call it done

Next: [[4_level-folder-and-backups|The level folder and backups]], [[1_order-of-work|The order of work]]
