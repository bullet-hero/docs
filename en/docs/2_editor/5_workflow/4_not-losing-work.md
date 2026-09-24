---
title: Not losing your work
date: 2026-09-24
tags: [level_author]
---

# Not losing your work

What undo covers and what it does not, which actions have no undo at all, and the one backup that works

> [!caution] Caution
> Autosave is configured in the settings but does not run yet. `Ctrl+S` is yours to press, and nothing in the editor will press it for you

**Undo covers edits to the level, and only those.** Every change to objects, keys, resources, themes, prefabs and settings goes through one operation buffer

**What undo does not cover**, because none of it is a change to the level:
- which gizmo, which timeline tool, whether snapping is on, whether the grid is on
- panel layout, which tab is open, where the playhead is
- the clipboard buffers
- the session's regenerated seed. Reloading the level resolves it from scratch again
- **saving**. Undo walks the model back, it does not un-write a file

**What has no undo at all.** Two things touch the disk directly:
- **Changing the level's file format.** Writing the level as `Blob` deletes the `Json` it replaced, and a blob cannot be read or repaired by eye
- **Deleting a level.** It is behind a dangerous-actions panel for that reason

**The Raw tab is the last resort and it validates nothing.** It shows the entire saved file as a tree of fields and applies no rules, no clamps and no checks. Its whole session commits as one undoable operation, so getting out is easy

> [!caution] Caution
> What you wrote inside the Raw tab was never checked by anything. Keep a copy of the folder beside you

> [!tip] Recommendation
> Make a copy of the level folder before every large rework and name them by date. The whole level is one folder, so a copy of it is a complete snapshot, and no other backup method exists

**Rules is the check worth running.** It reports what validation found - broken references, duplicate ids, parent cycles, prefabs nested too deep, overlapping beat segments

> [!info] Worth knowing
> No finding carries a repair, and that is deliberate. Every one of them is a content decision only you can make, and an automatic fix would quietly pick one of several valid answers

> [!tip] Tip
> An overhanging child span is not reported. That is legal authored data behaving as designed. To fit lifetimes, run the `span-fit` modifier

> [!tip] Recommendation
> `Ctrl+S` after every section you finish, a folder copy before every restructure, and Rules before you call it done

Next: [[4_level-folder-and-backups|The level folder and backups]], [[1_order-of-work|The order of work]]
