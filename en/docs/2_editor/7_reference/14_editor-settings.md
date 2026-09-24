---
title: Editor settings
date: 2026-09-24
tags: [level_author]
---

# Editor settings

The editor's settings tab, creating a level and using someone else's work

## Game Editor

Autosave, the camera, selection and file formats are set here

| Setting | What it does | Default |
|---|---|---|
| `Autosave` | turns autosave on | on |
| `Autosave Rate` | seconds from an unsaved edit to the autosave | 60 |
| `Max Autosave Files` | how many copies are kept. The oldest is dropped when the limit is reached | 25 |

The timer counts only while there are unsaved edits

One autosave does two things:
1. Writes a copy of the level to `<game folder>/backups/<level id>/`
2. Saves the level itself, as `Ctrl+S` would

A copy holds the level file alone. There are two ways to restore it:
- in the level settings: `Dangerous Zone` → `Restore from backup`
- by hand: copy it into the level folder as `level.json` (or `level.blob`)

More - [[4_not-losing-work#Autosave]]

`Camera Min Size` and `Camera Max Size` cap how far the editor viewport may zoom in and out

`Multi Select Requires Hold` and `Pick Invisible AABB` change what a click in the viewport means.
Check them when selection suddenly behaves differently than you remember

`Level Serialize Mode` and `Resources Serialize Mode` set the default format for writing to disk

More - [[3_speed-and-shortcuts]]

## Create a level

`Level Presets` decide what a new level starts with: empty, or a small scaffold.
Without a preset you would build that scaffold by hand every time

> [!caution] Caution
> `Parameters` set the things that are awkward to change later: frame length and framerate

> [!tip] Tip
> The `"level" File Format` and `"metadata" File Format` dropdowns pick how the level and its metadata are written to disk. Both can be changed later from the level's `Dangerous Zone`

More - [[2_first-level]]

## Using someone else's work

Every external resource in a level (music, images, fonts, texts) has to meet one of two options:
- a licence at least as free as `CC BY-NC`
- the rights holder's own permission covering public non-commercial redistribution

> [!caution] Caution
> A private "sure, go ahead" is not enough. A level under `CC BY-NC` is redistributed publicly. The permission has to cover that, not just your personal use

Nothing is checked on a level that stays on your device.
The rules apply at one moment: when a level is offered to a service

The full rules, the accepted licence list, the request template and where to find resources:
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
