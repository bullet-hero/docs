---
title: Speed and shortcuts
date: 2026-09-24
tags: [level_author]
---

# Speed and shortcuts

Every shortcut in the editor, how to rebind them, and the four things that save the most time

## The four biggest time savers

- **`Run Command`** (`Ctrl+Shift+P`) - everything the editor can do, searchable by name. Faster than remembering which panel a button is on
- **`Search Content`** (`Ctrl+F`) - jump to an object or an audio track by name. The playhead goes with you
- **`Ping`** - the viewport frames the selection, the timeline and the hierarchy scroll to it, all at once. Pressing it again steps to the next object of a multi-selection
- **Arrow keys on a timeline** - they move by direction, not by position in a list. Stepping between neighbouring keys needs no mouse

## The defaults

| Group | Key | Action |
|---|---|---|
| Playback | `Space` | play and pause |
| Editing | `Ctrl+Z` | undo |
| Editing | `Ctrl+Y` or `Ctrl+Shift+Z` | redo |
| Editing | `Ctrl+S` | save |
| Editing | `Ctrl+C`, `Ctrl+V` | copy and paste |
| Editing | `Ctrl+D` | duplicate |
| Selection | `Delete` | delete the selection |
| Selection | `Ctrl` held | multi-select |
| Finding things | `Ctrl+F` | search content |
| Finding things | `Ctrl+Shift+P` | run a command |
| Timeline | `Shift+T` | the Beat Grid window, where tempo is tapped in. `Tap Tempo` itself ships with no key, bind one if you want it |
| Timeline | `Ctrl` held with the wheel | pan |
| Timeline | `Shift` held with the wheel | zoom |
| Gizmos | `1-7` | selection, position, rotation, scale, size, anchors, pivot |
| Gizmos | `0` | hidden: the selection stays selected, but no handles and no border are drawn |
| Navigation | the arrow keys | move on whichever surface you last clicked into |

## Rebinding

Any shortcut can be rebound: `Settings` → `Keybindings`

Only the shortcuts you changed are stored. The rest come from the defaults.
So an improved default reaches you if you never rebound that shortcut.
`Reset Keybindings` simply removes your changes, and every shortcut goes back to its default

> [!tip] Tip
> Key labels are not hard-coded into the interface. After a rebind, the command palette and every context menu show the new key immediately

## Pressed and held shortcuts

A pressed shortcut fires only when its modifiers match exactly.
`Ctrl+Shift+P` cannot also fire what `Ctrl+P` would, and a bare `T` does not fire while `Ctrl` is down

A held shortcut fires when its modifiers are among the ones held down. It refines a gesture already happening

> [!info] Worth knowing
> That is why two held shortcuts may share a key on purpose. Multi-select and the timeline's pan are both on `Ctrl` and do not conflict

Next: [[1_order-of-work|The order of work]], [[2_reuse|Reuse: prefabs, copying, generators]]
