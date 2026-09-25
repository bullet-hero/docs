---
title: Hierarchy and clipboard
date: 2026-09-24
tags: [level_author]
---

# Hierarchy and clipboard

The hierarchy panel, the clipboard and the command palette

## Hierarchy

Shows every object alive on the **current frame**, nested by parent

An object appears here only while the playhead is inside its span. So the list changes as you scrub.
An empty hierarchy usually means the playhead is past the end of your content

> [!info] Worth knowing
> **A parent** passes its transform down to its children. Layers add up along the chain: a child's draw order is its own layer plus every ancestor's. So reparenting moves an object in draw order. It also rerolls its random values: randomness is tied to the effective layer

> [!tip] Tip
> Right-click a row for its actions. On touch, hold a row for the same menu

Holding a row opens its menu with a mouse too. Timeline clips have no hold menu

Drag a row onto another row to make it that object's child. Drop it on the empty space below the rows to take its parent away. A drop is refused:
- onto the object itself or onto the parent it already has
- onto one of its own children
- when the chain would nest deeper than 15 levels

The `Camera` row is pinned at the bottom of the list. Dropping a row onto it parents the object to the level's camera. Inside a prefab template the camera takes no children, and the template's root does

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Selecting several objects

`Ctrl`-click adds an object to the selection or takes it out. It means the same in the hierarchy, on the timelines and in the viewport. `Ctrl` is the only such key: `Shift`-click in the hierarchy does nothing, it is not a range select. The key can be rebound

A `Ctrl`-click, or a box selection that catches more than one item, turns on **multi-select mode**. While it is on, what a plain click does depends on `Multi Select Requires Hold` - see [[14_editor-settings]]

The selection control on the toolbar reads `No Selection` or `Selected (N)`. It works while something is selected:
- a press drops the whole selection
- a double click, or a `Shift`-click, turns multi-select mode on instead. Turned on this way, the mode ignores `Multi Select Requires Hold` and every plain click adds. That is how a finger with no `Ctrl` key builds a selection

The same control appears in the context menus while something is selected. There a press drops the selection

The mode ends by itself when nothing is selected any more, and with `Escape` when no text field is being edited

## Clipboard

Moves a selection between levels and between machines. Every timeline has its own buffer and its own status line

`Serialize Copy` writes every buffer into the system clipboard as text.
`Deserialize Paste` reads the text back into the buffers - and **stops there**

> [!info] Worth knowing
> That stop is deliberate. Reading the text and pasting are two decisions. Where content lands depends on the playhead and the active scope. Content appears only when you **paste it into the timeline you chose**

If the system clipboard holds foreign text, the editor reports an error instead of crashing. The clipboard holds whatever you last copied anywhere

There is no action that pastes every buffer at once. After `Deserialize Paste`, paste into each timeline yourself

Pasted keyframes land at the playhead. For each owner, its earliest pasted keyframe goes onto the playhead, counted inside that owner's own span. Event keyframes share one offset, so a camera move and the effect that went with it stay the same distance apart

A keyframe is skipped when it would land outside its owner's timeline, or on a frame its track already uses. The skipped keyframes are counted and reported in one message

A copy or a paste that works writes nothing to the console. Only problems are reported

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Command palette

Finds any editor action by name

It lists commands rather than content. These are the same actions the toolbar and the context menus run

> [!tip] Tip
> The content search (`Ctrl+F`) is its sibling. It searches every object of the current scope and every audio track. Resources are not there: each is picked through the field that needs it

More: [[3_speed-and-shortcuts|Speed and shortcuts]]
