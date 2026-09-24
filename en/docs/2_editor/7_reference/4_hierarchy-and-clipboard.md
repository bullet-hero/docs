---
title: Hierarchy and clipboard
date: 2026-09-24
tags: [level_author]
---

# Hierarchy and clipboard

The hierarchy panel, the clipboard and the command palette

## Hierarchy

Every object alive on the **current frame**, nested by parent

An object appears here only while the playhead is inside its span, so the list changes as you scrub - an empty hierarchy usually means the playhead is past the end of your content

> [!info] Worth knowing
> **Parenting** composes transforms, and layers add up along the chain: a child's draw order is its own layer plus every ancestor's. Reparenting therefore moves an object in draw order too - and rerolls any random values under it, because randomness is addressed by the effective layer

> [!tip] Tip
> Right-click a row for its actions. Hold a row on touch for the same menu

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Clipboard

One buffer per timeline, with a status line each

**Serialize Copy** writes every buffer into the system clipboard as text, so a selection can travel to another level or another machine. **Deserialize Paste** reads it back into the buffers - and **stops there**

> [!info] Worth knowing
> That stop is deliberate: deserialising and pasting are two decisions, and where a section lands depends on the playhead and the active scope. **Pasting into the timeline you actually chose** is what places anything

Deserialising text that is not ours reports rather than throws - the system clipboard holds whatever you last copied anywhere

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Command palette

Everything the editor can do, by name

It lists commands rather than content: the same actions the toolbar and the context menus run

> [!tip] Tip
> The content search is its sibling and searches objects, keyframes and resources instead

More: [[3_speed-and-shortcuts|Speed and shortcuts]]
