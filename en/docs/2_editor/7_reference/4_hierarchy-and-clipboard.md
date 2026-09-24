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

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Clipboard

Moves a selection between levels and between machines. Every timeline has its own buffer and its own status line

`Serialize Copy` writes every buffer into the system clipboard as text.
`Deserialize Paste` reads the text back into the buffers - and **stops there**

> [!info] Worth knowing
> That stop is deliberate. Reading the text and pasting are two decisions. Where content lands depends on the playhead and the active scope. Content appears only when you **paste it into the timeline you chose**

If the system clipboard holds foreign text, the editor reports an error instead of crashing. The clipboard holds whatever you last copied anywhere

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Command palette

Finds any editor action by name

It lists commands rather than content. These are the same actions the toolbar and the context menus run

> [!tip] Tip
> The content search is its sibling. It searches objects, keyframes and resources

More: [[3_speed-and-shortcuts|Speed and shortcuts]]
