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

The groups and names below are the ones `Settings` → `Keybindings` shows

### Playback

| Key | Name in settings | Action |
|---|---|---|
| `Space` | `Play / Pause` | play and pause |

### Edit

| Key | Name in settings | Action |
|---|---|---|
| `Ctrl+Z` | `Undo` | undo |
| `Ctrl+Y` or `Ctrl+Shift+Z` | `Redo` | redo |
| `Ctrl+S` | `Save Level` | save |
| `Ctrl+C` | `Copy` | copy |
| `Ctrl+V` | `Paste` | paste |
| `Ctrl+D` | `Duplicate` | duplicate |
| `Ctrl+G` | `Create Prefab From Selection` | create a prefab from the selection |

### Selection

| Key | Name in settings | Action |
|---|---|---|
| `Del` | `Delete Selection` | delete the selection |
| `Ctrl` held | `Multi-Select Modifier` | multi-select |
| `Ctrl+Shift+A` | `Deselect All` | drop every selection at once: objects, keyframes, audio and beat |
| `Ctrl+Shift+E` | `Exit Prefab Mode` | leave prefab mode and go back out to the level |

### View

| Key | Name in settings | Action |
|---|---|---|
| `Ctrl+F` | `Search Content` | search content |
| `Ctrl+Shift+P` | `Run Command` | run a command |
| `Ctrl+Left` | `Toggle Left Panel` | show or hide the left panel |
| `Ctrl+Right` | `Toggle Right Panel` | show or hide the right panel |
| `Ctrl+Down` | `Toggle Bottom Panel` | show or hide the bottom panel |
| `Ctrl+Up` | `Toggle Viewport Tools` | show or hide the tool groups over the viewport |
| `` ` `` held | `Preview (hold)` | preview: the editor's interface is hidden while the key is down |

### Timeline

| Key | Name in settings | Action |
|---|---|---|
| `Z` | `Tool: Cycle Folding` | cycle folding: every subtree, only the chosen kinds, nothing |
| `X` | `Tool: Snapping` | switch snapping on or off |
| `C` | `Tool: Selection` | the selection tool |
| `V` | `Tool: Marquee` | the marquee tool |
| `B` | `Tool: Scissors` | the scissors tool |
| `N` | `Tool: Edges` | the edges tool |
| `Ctrl+E` | `Fold Selection in Timeline` | fold the selected objects on the timeline |
| `Q` | `Tab: Level Timeline` | open the level timeline |
| `W` | `Tab: Local Timeline` | open the local timeline |
| `E` | `Tab: Audio Timeline` | open the audio timeline |
| `R` | `Tab: Events Timeline` | open the events timeline |
| `T` | `Tab: Prefab Timeline` | open the prefab timeline |
| `Shift+T` | `Beat Grid Window` | the Beat Grid window, where tempo is tapped in. `Tap Tempo` itself ships with no key, bind one if you want it |
| `Ctrl` held with the wheel | `Pan Modifier (wheel)` | pan |
| `Shift` held with the wheel | `Zoom Modifier (wheel)` | zoom |

`Z X C V B N` follow the timeline toolbar from left to right, and `Q W E R T` follow the tab strip. A timeline with fewer tools drops them from the right: the local timeline has only `Z X C V`. A letter the open timeline has no tool for does nothing

### Gizmos

| Key | Name in settings | Action |
|---|---|---|
| `1` | `Gizmo: Selection` | selection |
| `2` | `Gizmo: Position` | position |
| `3` | `Gizmo: Rotation` | rotation |
| `4` | `Gizmo: Scale` | scale |
| `5` | `Gizmo: Size` | size |
| `6` | `Gizmo: Anchors` | anchors |
| `7` | `Gizmo: Pivot` | pivot |
| `0` | `Gizmo: Hidden` | hidden: the selection stays selected, but no handles and no border are drawn |

### Window

| Key | Name in settings | Action |
|---|---|---|
| `F11` | `Toggle Fullscreen` | switch fullscreen on or off. Works on every screen, on desktop only |

### Navigation

| Key | Name in settings | Action |
|---|---|---|
| `Up` | `Navigate Up` | move up on whichever surface you last clicked into |
| `Down` | `Navigate Down` | move down on whichever surface you last clicked into |
| `Left` | `Navigate Left` | move left on whichever surface you last clicked into |
| `Right` | `Navigate Right` | move right on whichever surface you last clicked into |

Bare keys such as the gizmo digits, the timeline letters and `Space` do nothing while you type in a text field. Typing a `2` into a frame field does not switch the gizmo

## Arrow keys on a timeline

An arrow picks the nearest item in that direction on screen. The same press finds the same item at any zoom

- From a multi-selection, an arrow starts at the item furthest along the pressed direction. It never steps back into the block you selected
- An arrow move always replaces the selection. It never adds to it
- The timeline scrolls only as much as it needs to show the new item. Clicking the playhead readout still centres the view
- While the preview player is on, the arrows steer it, not the timeline. The hierarchy and the `Raw Data` tab keep their arrows once you click into them

## Seeing the level

**Preview.** Hold `` ` `` to hide the editor's interface and look at the level alone. It is a hold, not a switch: release the key and everything is back. The level, the letterbox bars, the player and the camera bounds stay visible.
There is no button or setting for it. The key is rebindable as `Preview (hold)`

**The viewport grid** is switched with its toolbar button or the `Viewport Grid` command. It starts off. `Settings` → `Game Editor` → `Grid On By Default` changes that, and whether you switched it on is not remembered between sessions

**The gizmo magnet** snaps what a gizmo drags to the grid. It is on by default and does not depend on the gizmo mode. Its toolbar button and the `Gizmo Magnet` command switch it

**Paused is the normal state for looking.** The grid, the colliders, the bot overlay, the gizmo handles and the selection border all keep drawing while playback is paused. Grabbing a gizmo handle pauses playback

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
