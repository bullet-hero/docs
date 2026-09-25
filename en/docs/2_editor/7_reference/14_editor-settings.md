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

## Grid

The viewport grid is drawn behind the level to help you place objects

| Setting | What it does | Default |
|---|---|---|
| `Grid On By Default` | whether the grid is on when the editor opens. It is only the starting state | off |
| `Grid Size` | the side of one cell, in world units | 1 |
| `Grid Opacity` | how strongly the lines show, from 0 to 1 | 0.25 |

The grid button on the toolbar turns it on and off. That state is not saved between sessions

How the grid looks:
- It has no edge. The cell changes in steps of 10 as you zoom, and the finer grid fades in
- When a grid level would need too many lines, that level is switched off rather than thinned
- The line colour is always the inverse of the current frame's camera background, so the grid stays visible when the background changes. Only the opacity is yours

With snapping on, dragging a position snaps to half a cell: to the crossings and to the cell centres. It uses the grid you can see. With the grid off, a position drag snaps to a fixed step

## Selection

| Setting | What it does | Default |
|---|---|---|
| `Multi Select Requires Hold` | on: in multi-select mode a click adds only while `Ctrl` is held, and a plain click replaces the selection. Off: once the mode is on, every click adds | on |
| `Preview Collider On Select` | draws the hitbox of every selected object as a translucent fill | off |
| `Pick Invisible AABB` | a click picks an object by its whole rect instead of by what it draws | off |
| `Long Press Delay` | how long a hold waits before it opens a menu, in seconds | 0.5 |
| `Long Press Travel` | how far the pointer may drift during that hold before it counts as a drag | 8 |
| `Selected Hitbox Opacity` | how solid a selected object's hitbox is drawn | 0.5 |
| `Hitbox View Opacity` | the same for the view of every hitbox, fainter because hundreds of them overlap there | 0.25 |

Releasing `Ctrl` in multi-select mode clears nothing and does not leave the mode. Only the next plain click replaces the selection. More on the mode - [[4_hierarchy-and-clipboard]]

The collider button on the toolbar shows the hitbox of everything in the frame, the player's circle included. That state is not saved between sessions. With too many hitboxes on screen, the view switches itself off with a message rather than drawing only some of them

An object with no collider draws no hitbox in either view, and neither does an inactive one

## Gizmos

| Setting | What it does | Default |
|---|---|---|
| `Gizmo Handle Scale` | how big the viewport drag handles are, from 0.1 to 10. A handle sized for a mouse is hard to hit with a thumb | 1 |

The handles keep the same size on screen at any zoom

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
