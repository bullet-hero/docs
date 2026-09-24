---
title: Speed and shortcuts
date: 2026-09-24
tags: [level_author]
---

# Speed and shortcuts

Every shortcut in the editor, how rebinding works, and the four things that save the most time

## Every shortcut is a setting

There is a catalog of defaults and your own overrides on top of it, stored sparsely - only what you actually moved. An improved default therefore reaches everyone who never rebound it, and reset is a removal rather than a write. The Keybindings tab in Settings is where they live

> [!tip] Tip
> Labels are resolved rather than hard-coded. Rebind something and the command palette and every context menu say the new key immediately

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
| Timeline | `Shift+T` | the Beat Grid window, where tempo is tapped in. Tap Tempo itself ships with no key, bind one if you want it |
| Timeline | `Ctrl` held with the wheel | pan |
| Timeline | `Shift` held with the wheel | zoom |
| Gizmos | `1-7` | selection, position, rotation, scale, size, anchors, pivot |
| Gizmos | `0` | hidden: the selection stays selected, but no handles and no border are drawn |
| Navigation | the arrow keys | move on whichever surface you last clicked into |

## Pressed and held shortcuts

A pressed shortcut matches its modifiers exactly, a held one matches them as a subset. `Ctrl+Shift+P` cannot also fire what `Ctrl+P` would, and a bare `T` does not fire while `Ctrl` is down. A held modifier refines a gesture already happening

> [!info] Worth knowing
> That is why two held shortcuts may share a key on purpose - multi-select and the timeline's pan modifier are both on `Ctrl` and do not conflict

## The four biggest time savers

- **Run a command** - everything the editor can do, searchable by name. Faster than remembering which panel a button is on
- **Search content** - jump to an object or an audio track by name, and the playhead goes with you
- **Ping** - the viewport frames it, the timeline scrolls to it, the hierarchy scrolls to it, all at once. Pressing it again walks a multi-selection
- **Arrow keys on a timeline** - they move by direction rather than by index, so stepping between neighbouring keys needs no mouse

Next: [[1_order-of-work|The order of work]], [[2_reuse|Reuse: prefabs, copying, generators]]
