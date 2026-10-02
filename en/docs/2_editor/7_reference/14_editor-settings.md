---
title: Editor settings
date: 2026-10-02
tags: [level_author]
---

# Editor settings

Autosave, the grid, selection, gizmos and new-level presets are set here. Autosave is on by default and fires {{v:editor.autosave-delay}} seconds after an edit

## Game Editor

Autosave, the camera, selection and file formats are set here

| Setting | What it does | Default |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | turns autosave on | on |
| `{{ui:settings_game-editor_autosave-rate}}` | how many seconds pass from an unsaved edit to the autosave | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | how many copies are kept. When the limit is reached, the oldest is deleted | {{v:editor.autosave-copies}} |

The timer runs only while there are unsaved edits

One autosave does two things:
1. Writes a copy of the level to `<game folder>/backups/<level id>/`
2. Saves the level itself, as `Ctrl+S` does

A copy holds only the level file. There are two ways to restore it:
- in the level settings: `{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- by hand: copy it into the level folder under the name `level.json` (or `level.blob`)

More - [[4_not-losing-work#Autosave]]

`{{ui:settings_game-editor_camera-min-size}}` and `{{ui:settings_game-editor_camera-max-size}}` limit how far the editor viewport can zoom in and out

`{{ui:settings_game-editor-multi-select-requires_hold}}` and `{{ui:settings_game-editor-pick-invisible_aabb}}` change what a click in the viewport means.
Check them if selection suddenly behaves differently from what you are used to

`{{ui:settings_game-editor-level-serialize_mode}}` and `{{ui:settings_game-editor-resources-serialize_mode}}` set the default format for writing to disk

`{{ui:settings_game-editor_publish-language}}` picks the language a Workshop item's title and description are published in first: `{{ui:enum_publish-language_english}}` (the default) or `{{ui:enum_publish-language_system}}`, the device's language

More - [[3_speed-and-shortcuts]]

## Grid

The viewport grid is drawn behind the level and helps you place objects

| Setting | What it does | Default |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | whether the grid is on when the editor opens. This is only the starting state | off |
| `{{ui:settings_game-editor-grid_size}}` | the side of one cell, in world units | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | how visible the lines are, from 0 to 1 | 0.25 |

The grid button on the toolbar turns it on and off. That state is not saved between sessions

How the grid looks:
- It has no edge. The cell changes in steps of 10 as you zoom, and the finer grid fades in gradually
- If a grid level would need too many lines, that level is switched off rather than thinned out
- The line colour is always the inverse of the camera background on the current frame, so the grid stays visible when the background changes. You set only the opacity

With snapping on, dragging a position sticks to half a cell: to the crossings and to the cell centres. It uses the grid you can see. With the grid off, the position sticks to a fixed step

## Selection

| Setting | What it does | Default |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | on: in multi-select mode a click adds only while `Ctrl` is held, and a plain click replaces the selection. Off: while the mode is on, every click adds | on |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | draws the hitbox of every selected object as a translucent fill | off |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | a click picks an object by its whole rectangle, not by what it draws | off |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | how long a hold lasts before a menu opens, in seconds | 0.5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | how far the cursor may move during the hold before it becomes a drag | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | how solid the hitbox of a selected object is drawn | 0.5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | the same for the view of all hitboxes, fainter because hundreds of them overlap there | 0.25 |

Releasing `Ctrl` in multi-select mode clears nothing and does not leave the mode. Only the next plain click replaces the selection. More on the mode - [[4_hierarchy-and-clipboard]]

The collider button on the toolbar shows the hitboxes of everything in the frame, the player's circle included. That state is not saved between sessions. If there are too many hitboxes on screen, the view switches itself off with a message rather than drawing only some of them

An object with no collider draws no hitbox in either view, and neither does an inactive object

The fill colour of both views is `Settings > Graphics > Colliders Only Mode > Fill Color`, shared with the game's "Colliders Only" mode ([[4_settings]]). The two opacities above stay the editor's own settings

## Gizmos

| Setting | What it does | Default |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | how large the drag handles in the viewport are, from 0.1 to 10. A handle sized for a mouse is hard to hit with a finger | 1 |

The handles keep the same size on screen at any zoom

## Create a level

`{{ui:settings_editor-settings_level-presets}}` set what a new level starts with: empty or with a small scaffold.
Without a preset you would have to build that scaffold by hand every time

> [!caution] Caution
> `{{ui:settings_editor-settings_parameters}}` set the things that are awkward to change later: the length in frames and the framerate

> [!tip] Tip
> The `{{ui:settings_editor-settings_quot-level-quot-file-format}}` and `{{ui:settings_editor-settings_quot-metadata-quot-file-format}}` lists pick the format the level and its metadata are written to disk in. Both can be changed later in the level's `{{ui:settings_level-settings_dangerous-zone}}`

More - [[2_first-level]]

## Library

`{{ui:settings_editor-settings_library}}` is the last tab, after `{{ui:settings_editor-settings_community}}`. It holds the resources you reuse across levels: the device library, your own collections and, in the Steam build, the collections you subscribed to in Steam Workshop

The column on the left picks the kind: `{{ui:settings_level-settings_collections}}`, then prefabs, themes, shapes and effects, then textures, fonts and audio.
Here you create and edit collections, copy entries between them, import and export them, and in the Steam build publish your own

More - [[16_library-and-collections]]

## Using someone else's work

Every external resource in a level (music, images, fonts, texts) has to fit one of two options:
- a licence at least as free as `CC BY-NC`
- the rights holder's own permission for public non-commercial distribution

> [!caution] Caution
> A private "sure, no problem" is not enough. A level under `CC BY-NC` is distributed publicly. The permission has to cover exactly that, not only your personal use

A level that stays on your device is not checked.
The rules apply at one moment: when the level is handed to a service

The full rules, the list of accepted licences, the request template and where to look for resources:
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
