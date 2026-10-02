---
title: Hierarchy and clipboard
date: 2026-10-02
tags: [level_author]
---

# Hierarchy and clipboard

The hierarchy is a tree of the current frame's objects by parent. Every timeline has its own clipboard buffer, and the command palette finds any editor action by name

## Hierarchy

Shows every object alive on the **current frame**, nested by parent

An object is visible here only while the playhead is inside its span. So the list changes as you scrub.
An empty hierarchy usually means the playhead is past the end of the content

> [!info] Worth knowing
> **A parent** passes its transform down to its children. Layers add up along the chain: a child's draw order is its own layer plus the layers of all its ancestors. So changing the parent moves the object in draw order. It also changes its random values: randomness is tied to the resulting layer

> [!tip] Tip
> Right-click a row to open its actions. On a touchscreen, holding opens the same menu

Holding a row opens the menu with a mouse too. Clips on the timelines have no hold menu

Drag a row onto another to make the object its child. Dropped on the empty space below the rows, it loses its parent. A drop is refused:
- onto the object itself or onto the parent it already has
- onto one of its own children
- if the chain would become deeper than 15 levels

The `{{ui:editor_search-option_camera}}` row is pinned at the bottom of the list. A row dropped onto it makes the object a child of the level's camera. Inside a prefab template the camera takes no children, but the template's root does

More: [[3_how-the-editor-thinks|How the editor works]]

## Selecting several objects

A click with `Ctrl` adds an object to the selection or removes it. It works the same in the hierarchy, on the timelines and in the viewport. `Ctrl` is the only such key: a click with `Shift` in the hierarchy does nothing, there is no range selection. The key can be rebound

A click with `Ctrl`, or a box that catches more than one item, turns on **multi-select mode**. While it is on, what a plain click does depends on `{{ui:settings_game-editor-multi-select-requires_hold}}` - see [[14_editor-settings]]

The selection item on the toolbar shows `{{ui:editor_multi-select_status}}` or `Selected (N)`. It works while something is selected:
- a press clears the whole selection
- a double click or a click with `Shift` turns on multi-select mode instead. Turned on this way, the mode ignores `{{ui:settings_game-editor-multi-select-requires_hold}}`, and every plain click adds. That is how a finger, which has no `Ctrl`, builds a selection

The same item appears in context menus while something is selected. There a press clears the selection

The mode turns off by itself when nothing is selected, and with `Escape` if no text field is being typed in

## Clipboard

Moves a selection between levels and between devices. Every timeline has its own buffer and its own status line

`{{ui:editor_clipboard-serialize_copy}}` writes all buffers into the system clipboard as text.
`{{ui:editor_clipboard-deserialize_paste}}` reads the text back into the buffers - and **stops there**

> [!info] Worth knowing
> The stop is deliberate. Reading the text and pasting are two different decisions. Where content is pasted depends on the playhead and the active scope. Content appears only when you **paste it into the timeline you chose**

If the system clipboard holds someone else's text, the editor reports an error and does not crash. It holds whatever you last copied anywhere

There is no "paste every buffer at once" action. After `{{ui:editor_clipboard-deserialize_paste}}`, paste into each timeline yourself

Pasted keyframes land at the playhead. For each owner, its earliest pasted keyframe is put on the playhead, counted inside that owner's span. Event keyframes shift by the same amount, so a camera move and the effect that went with it stay the same distance apart

A keyframe is skipped if it would land outside its owner's timeline or on a frame already taken on its track. Skipped keyframes are counted and reported in one message

A successful copy or paste writes nothing to the console. Only problems are reported

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Command palette

Finds any editor action by name

It lists commands, not content. These are the same actions the toolbar and the context menus run

> [!tip] Tip
> The content search (`Ctrl+F`) is its twin. It searches every object of the current scope and every audio track. Resources are not in it: each one is picked through the field that needs it

More: [[3_speed-and-shortcuts|Speed and shortcuts]]
