---
title: Not losing your work
date: 2026-09-24
tags: [level_author]
---

# Not losing your work

What autosave and undo cover and what they do not, which actions have no undo at all, and how to get a level back

Three things protect your work: autosave, undo and a copy of the level folder. Each covers something the others do not.
The complete snapshot of a level is only a copy of its folder, because the whole level is one folder

## The habit

> [!tip] Recommendation
> `Ctrl+S` after every section you finish. A copy of the level folder before every restructure. The `Rules` check before you call the level done

## Autosave

Autosave is on by default. It works like this:
1. An unsaved edit appears - a `60` second countdown starts
2. The game writes a copy of the level to `backups/<level id>/` in the game's folder, outside `levels`
3. Then it saves the level itself, as `Ctrl+S` would

An editor left open with nothing changed writes nothing.
Whatever you changed since the last save, yours or autosave's, lives only in memory

`25` copies are kept, the oldest is dropped first.
A copy holds the level file alone, with no metadata, no track and no images. It survives the level being deleted.
A copy of a protected level is protected with that level's password

The switch, the interval and the number of copies are in `Settings` → `Game Editor`

**Restoring:** Level Settings, the `Dangerous Zone` tab, `Restore from backup`. Copies are listed newest first, each named by the moment it was taken.
The file being replaced is copied into `backups` first, so a restore can itself be undone

You can also restore by hand: copy the backup into the level folder as `level.json` (or `level.blob`)

## What undo covers

Undo covers edits to the level, and only those. Every change to objects, keys, resources, themes, prefabs and settings goes through one operation buffer

Anything that does not change the level is not undone:
- which gizmo, which timeline tool, whether snapping and the grid are on
- panel layout, which tab is open, where the playhead is
- the clipboard buffers
- the session's regenerated seed. Reloading the level picks it again
- **saving**. Undo walks the level in memory back, not the file on disk

## What has no undo at all

Two actions write straight to disk:
- **Changing the level's file format.** Writing the level as `Blob` deletes the `Json` it replaced. And a `Blob` cannot be read or repaired by eye
- **Deleting a level.** That is why it sits in the `Dangerous Zone`

## The Raw tab

The `Raw Data` tab shows the entire saved file as a tree of fields. It checks nothing: no rules, no clamps

It is the last resort. Its whole session commits as one operation, and that operation can be undone

> [!caution] Caution
> What you wrote inside the `Raw Data` tab was never checked by anything. Keep a copy of the level folder at hand. More - [[4_level-folder-and-backups#Backups and recovery]]

## Rules

The check worth running is the `Rules` tab. It shows what validation found: broken references, duplicate ids, parent cycles, prefabs nested too deep, overlapping beat segments

The game can repair some findings: one at a time, or all at once with `Fix All`.
Repairs are applied with `Save`, as one operation that can be undone. `Discard` throws them away.
Graph findings carry no repair

An overhanging child span is not an error. It is legal data behaving as designed.
To fit lifetimes, run the `span-fit` modifier

Next: [[4_level-folder-and-backups|The level folder and backups]], [[1_order-of-work|The order of work]]
