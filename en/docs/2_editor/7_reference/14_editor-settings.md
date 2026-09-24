---
title: Editor settings
date: 2026-09-24
tags: [level_author]
---

# Editor settings

The editor's settings tab, creating a level and using someone else's work

## Game Editor

**Autosave** is configured here - how often a copy is taken and how many are kept.  the policy is stored but not acted on yet, so nothing is written on a timer. Until it is, saving is entirely yours

**Camera bounds** cap how far the editor viewport may zoom

**Multi-select requires hold** and **pick invisible** change what a click in the viewport means, which is worth knowing when selection suddenly behaves differently than you remember

The **serialize modes** decide how levels are written to disk by default

More: [[3_speed-and-shortcuts|Speed and shortcuts]]

## Create a level

A **preset** decides what the new level starts with - an empty one, or a small amount of scaffolding you would otherwise build by hand every time

> [!caution] Caution
> **Parameters** set the things that are awkward to change later: frame length and framerate

> [!tip] Tip
> The two file-format dropdowns pick how the level and its metadata are written to disk. Both can be changed afterwards from the level's Dangerous Zone

More: [[2_first-level|Your first level: the route]]

## Using someone else's work

Every external resource in a level - music, images, fonts, texts - has to satisfy one of two options: a licence at least as free as `CC BY-NC`, or the rights holder's own permission covering public non-commercial redistribution

> [!caution] Caution
> A private "sure, go ahead" is not enough on its own. A level marked `CC BY-NC` is redistributed publicly, so the permission has to cover that rather than your personal use

Nothing is checked on a level that stays on your own device. All of it applies at exactly one moment - when a level is offered to a service

The full rules, the accepted licence list, the request template and where to look for resources are in the guide:
- [[2_legal-resource-paths|Two ways a resource qualifies]]
- [[6_asking-permission|Asking an author for permission]]
- [[3_where-to-get-resources|Where to get resources]]
