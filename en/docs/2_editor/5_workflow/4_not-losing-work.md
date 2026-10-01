---
title: Not losing your work
date: 2026-10-01
tags: [level_author]
---

# Not losing your work

Your work is protected by autosave, undo and a copy of the level folder. Only a copy of the folder is a complete snapshot of the level. Changing the file format and deleting a level cannot be undone

Each safeguard covers what the others do not. Autosave and undo do not replace a copy of the folder, because the whole level is one folder

## The habit

> [!tip] Recommendation
> `Ctrl+S` after every finished section. A copy of the level folder before every restructure. The `Rules` check before you consider the level done

## Autosave

Autosave is on by default. It works like this:
1. An unsaved edit appears - a `60` second countdown starts
2. The game writes a copy of the level to `backups/<level id>/` in the game's folder, outside `levels`
3. Then it saves the level itself, as `Ctrl+S` would

An editor opened with no changes writes nothing.
Everything changed since the last save, yours or automatic, exists only in memory

`25` copies are kept, the oldest is deleted first.
A copy holds only the level file, with no metadata, track or images. It survives the level being deleted.
A copy of a protected level is locked with that level's own password

The switch, the interval and the number of copies are set in `Settings` → `Game Editor`

**Restoring:** level settings, the `Dangerous Zone` tab, `Restore from backup`. Copies go from newest to oldest, each named by the moment it was taken.
The current file is first copied into `backups` itself, so a restore can be rolled back too

You can also restore by hand: copy the backup into the level folder as `level.json` (or `level.blob`)

## Unsaved changes

An action that would replace the open level or leave it first asks what to do with unsaved edits:
- opening another level from the level list, including copying a level and opening the copy
- creating a level
- `Exit to Menu` from the editor settings and from the level settings
- `Restore from backup`
- in `Dangerous Zone`: copying the level and opening the copy, changing the file format, setting a password

The dialog has three answers:
- `Save` - saves the level and continues the action
- `Discard and continue` - the red button, the only answer that loses edits
- `Cancel` - does nothing

Playing from the level settings asks too, but with two answers: `Save and play` and `Cancel`. Edits cannot be discarded here, because on return from the game the level is read from disk again.
If nothing is unsaved, the dialog does not appear

## What undo covers

Undo covers edits to the level, and only them. Every change to objects, keyframes, resources, themes, prefabs and settings goes through one operation buffer

What does not change the level is not undone:
- the selected gizmo, the timeline tool, whether snapping and the grid are on
- the panel layout, the open tab, the playhead position
- the clipboards
- a regenerated session seed. Reloading the level picks it again
- **saving**. Undo rolls back the level in memory, not the file on disk

## What has no undo at all

Two actions write straight to disk:
- **Changing the level's file format.** Writing the level as `Blob` deletes the previous `Json`. And a `Blob` cannot be read or repaired by eye
- **Deleting a level.** That is why it is hidden in `Dangerous Zone`

## The Raw tab

The `Raw Data` tab shows the whole saved file as a tree of fields. It checks nothing: no rules, no limits

It is the last resort. All edits of a session are applied as one operation, and it can be undone

> [!caution] Caution
> Nothing has checked what you wrote in the `Raw Data` tab. Keep a copy of the level folder at hand. More - [[4_level-folder-and-backups#Backups and recovery]]

## Rules

The check worth running is the `Rules` tab. It shows what validation found: broken references, duplicate ids, parent cycles, prefabs nested too deep, overlapping beat segments

The game can fix some findings: one at a time or all at once with the `Fix All` button.
Fixes are applied with the `Save` button, as one operation that can be undone. `Discard` throws them away.
Graph findings have no fix

A child's span running past its parent is not an error. It is normal data, and it behaves as intended.
To fit lifetimes, run the `span-fit` modifier

Next: [[4_level-folder-and-backups|The level folder and backups]], [[1_order-of-work|The order of work]]
