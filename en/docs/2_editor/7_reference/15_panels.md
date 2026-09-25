---
title: Panels
date: 2026-09-25
tags: [level_author]
---

# Panels

The editor's three docked panels: opening, closing and resizing them

## Three panels

The viewport sits in the middle, and three panels dock around it:
- the left panel holds the hierarchy
- the right panel holds the inspectors
- the bottom panel holds the timelines

A right-panel tab with nothing to show is hidden. More - [[5_object-properties]]

## Panel handle

Each panel has one handle on its edge:
- a click opens or closes the panel
- a drag resizes it. One drag can take a closed panel to any width

The arrow on the handle reads the panel's state. It points one way when the panel is closed and is turned half a turn when it is open, at any width. An arrow turned only part of the way means a drag is in progress

A click animates the panel, and so do the shortcuts: `Ctrl+Left`, `Ctrl+Right` and `Ctrl+Down`. More - [[3_speed-and-shortcuts]]

## Widths

A panel rests either closed or somewhere between its narrowest and its widest width. The narrowest width is also the ordinary one: it is how much room the panel's content needs

| Panel | Narrowest | Widest |
|---|---|---|
| left | 25% of the screen | 25% of the screen |
| right | 40% of the screen | 50% of the screen |
| bottom | 35% of the screen height | 70% of the screen height |

The left panel only opens and closes. The rest of the editor is laid out against its width

Let go of a drag below the narrowest width and the panel goes to whichever is nearer: closed, or the narrowest width. Exactly halfway opens it. So one swipe still closes a panel

A click reopens a panel at the width you last left it open at

> [!info] Worth knowing
> A dragged width is never saved. It lives only for the current session, so a panel you widened does not stay wide next time

## Minimize and auto-open

`Toggle Minimize Panels` closes every open panel and leaves the viewport alone. Pressed again, it opens the panels that were open. If none were, it opens all three

`Auto-Open Right Panel` (settings, `Game Editor` tab, `Interface`) opens the right panel by itself when you select something. It is off by default
