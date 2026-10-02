---
title: Speed and shortcuts
date: 2026-10-02
tags: [level_author]
---

# Speed and shortcuts

The command palette (Ctrl+Shift+P), content search (Ctrl+F), the Ping button and the arrow keys on a timeline save the most time. Any key can be rebound in the settings

## The four biggest time savers

- **`{{ui:editor_search-title_command}}`** (`Ctrl+Shift+P`) - everything the editor can do, searchable by name. Faster than remembering which panel a button is on
- **`Search Content`** (`Ctrl+F`) - jump to an object or an audio track by name. The playhead goes with you
- **`{{ui:cmd_editor_ping}}`** - the viewport frames the selection, the timeline and the hierarchy scroll to it, all at once. Pressing it again steps to the next object of a multi-selection
- **Arrow keys on a timeline** - they move by direction, not by position in a list. You can step between neighbouring keyframes without the mouse

## The defaults

The groups and names below are the ones `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}` shows

### Playback

| Key | Name in settings | Action |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | play and pause |

### Edit

| Key | Name in settings | Action |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | undo |
| `Ctrl+Y` or `Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | redo |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | save |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | copy |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | paste |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | duplicate |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | create a prefab from the selection |

### Selection

| Key | Name in settings | Action |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | delete the selection |
| `Ctrl` held | `{{ui:settings_keybindings_editor_multi_select}}` | multi-select |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | clear every selection at once: objects, keyframes, audio and beat |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | exit Prefab Mode back to the level |

### View

| Key | Name in settings | Action |
|---|---|---|
| `Ctrl+F` | `Search Content` | search content |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | run a command |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | show or hide the left panel |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | show or hide the right panel |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | show or hide the bottom panel |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | show or hide the tool groups over the viewport |
| `` ` `` held | `{{ui:settings_keybindings_editor_preview}}` | preview: the editor's interface is hidden while the key is down |

### Timeline

| Key | Name in settings | Action |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | cycle folding: every subtree, only the chosen kinds, nothing |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | switch snapping on or off |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | the selection tool |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | the marquee tool |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | the scissors tool |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | the edges tool |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | fold the selected objects on the timeline |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | open the level timeline |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | open the local timeline |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | open the audio timeline |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | open the events timeline |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | open the prefab timeline |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | the beat grid window, where the tempo is tapped out. `{{ui:settings_keybindings_editor_beat_tap}}` itself has no default key, bind one if you need it |
| `Ctrl` held with the wheel | `{{ui:settings_keybindings_timeline_pan_modifier}}` | pan |
| `Shift` held with the wheel | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | zoom |

`Z X C V B N` follow the timeline toolbar from left to right, and `Q W E R T` follow the tab strip. A timeline with fewer tools drops them from the right: the local timeline has only `Z X C V`. A letter the open timeline has no tool for does nothing

### Gizmos

| Key | Name in settings | Action |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | selection |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | position |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | rotation |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | scale |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | size |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | anchors |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | pivot |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | hidden: the selection stays, but neither handles nor the border are drawn |

### Window

| Key | Name in settings | Action |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | switch fullscreen on or off. Works on any screen, on desktop only |

### Navigation

| Key | Name in settings | Action |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | move up on whichever surface you last clicked into |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | move down on whichever surface you last clicked into |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | move left on whichever surface you last clicked into |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | move right on whichever surface you last clicked into |

Bare keys such as the gizmo digits, the timeline letters and `Space` do nothing while you type in a text field. A `2` in a frame field does not switch the gizmo

## Arrow keys on a timeline

An arrow picks the nearest item in that direction on screen. The same press finds the same item at any zoom

- From a multi-selection, an arrow starts at the item furthest along the pressed direction. It never steps back into the block you selected
- An arrow move always replaces the selection. It never adds to it
- The timeline scrolls only as much as it needs to show the new item. Clicking the playhead readout still centres the view
- While the test player is on, the arrows control it, not the timeline. The hierarchy and the `{{ui:settings_level-settings_raw}}` tab keep their arrows once you click into them

## Seeing the level

**Preview.** Hold `` ` `` to hide the editor's interface and look at the level alone. It is a hold, not a switch: release the key and everything is back. The level, the letterbox bars, the player and the camera bounds stay visible.
There is no button or setting for it. The key is rebindable as `{{ui:settings_keybindings_editor_preview}}`

**The viewport grid** is switched with its toolbar button or the `{{ui:cmd_editor_viewport-grid}}` command. It starts off. This is changed by `{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`, and whether you switched it on is not remembered between sessions

**The gizmo magnet** snaps what a gizmo drags to the grid. It is on by default and does not depend on the gizmo mode. It is switched by its toolbar button and the `{{ui:cmd_editor_gizmo-magnet}}` command

**Paused is the normal state for looking.** The grid, the colliders, the bot overlay, the gizmo handles and the selection border all keep drawing while playback is paused. Grabbing a gizmo handle pauses playback

## Rebinding

Any key can be rebound: `{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

Only the keys you changed are stored. The rest come from the defaults.
So an improved default reaches you if you have not touched that key.
`{{ui:settings_keybindings_reset}}` simply removes your changes, and all keys return to the defaults

> [!tip] Tip
> Key labels are not hard-coded into the interface. After a rebind, the command palette and every context menu show the new key immediately

## Pressed and held keys

A pressed key fires only if its modifiers match exactly.
`Ctrl+Shift+P` will not also fire as `Ctrl+P`, and a bare `T` will not fire while `Ctrl` is held

A held key fires if its modifiers are among the ones held down. It refines a gesture that is already under way

> [!info] Worth knowing
> That is why two held keys can share one button on purpose. Multi-select and timeline panning are both on `Ctrl` and do not get in each other's way

Next: [[1_order-of-work|The order of work]], [[2_reuse|Reuse: prefabs, copying, generators]]
