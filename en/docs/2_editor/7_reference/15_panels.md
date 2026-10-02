---
title: Panels
date: 2026-10-02
tags: [level_author]
---

# Panels

The hierarchy, inspectors and timelines are docked around the viewport. A click on the handle at a panel's edge opens or closes it, a drag changes its width

## Three panels

The viewport sits in the middle, and three panels are docked around it:
- the left panel holds the hierarchy
- the right panel holds the inspectors
- the bottom panel holds the timelines

A right-panel tab with nothing to show is hidden. More - [[5_object-properties]]

## Panel handle

Each panel has one handle on its edge:
- a click opens or closes the panel
- a drag changes its size. One movement can pull a closed panel out to any width

The arrow on the handle shows the panel's state. On a closed panel it points one way, on an open panel it is turned half a turn at any width. An arrow turned only part of the way means a drag is in progress

A click opens the panel with an animation, and so do the shortcuts: `Ctrl+Left`, `Ctrl+Right` and `Ctrl+Down`. More - [[3_speed-and-shortcuts]]

## Width

A panel is either closed or somewhere between its narrowest and its widest width. The narrowest width is also the ordinary one: it is how much room the panel's content needs

| Panel | Narrowest | Widest |
|---|---|---|
| left | 25% of the screen | 25% of the screen |
| right | 40% of the screen | 50% of the screen |
| bottom | 35% of the screen height | 70% of the screen height |

The left panel only opens and closes. The rest of the editor is laid out against its width

If you release a drag narrower than the narrowest width, the panel goes to whichever is closer: the closed position or the narrowest width. Exactly halfway, it opens. So one movement still closes a panel

A click opens the panel at the width you last left it open at

> [!info] Worth knowing
> A dragged width is not saved. It lives only in the current session, so a widened panel will not stay wide next time

## Minimize and open on its own

`{{ui:cmd_editor_toggle-minimize-panels}}` closes every open panel and leaves the viewport alone. Pressing it again opens the panels that were open. If none were open, all three open

`{{ui:settings_game-editor_interface-auto-open-panel}}` (settings, `{{ui:settings_game-editor_title}}` tab, `{{ui:settings_interface_label}}`) opens the right panel by itself when you select something. Off by default
