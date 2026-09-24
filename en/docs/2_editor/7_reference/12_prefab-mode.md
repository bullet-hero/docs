---
title: Prefab Mode
date: 2026-09-24
tags: [level_author]
---

# Prefab Mode

Editing a prefab in place and flattening nested prefabs

## Prefab Mode

In this mode you edit a prefab **template**

> [!caution] Caution
> You are editing the template, not one placement of it. Saving carries the change to every placement that references this template

How a placement works:
- The moment you point a placement at a template, real copies of its objects with permanent ids are written into the level
- Nothing is rebuilt when the level loads. A prefab child is an entirely ordinary object
- A placement can differ from the template through **per-instance overrides**. They are recorded when you edit such an object *outside* Prefab Mode
- Edits made in Prefab Mode record no overrides. They change the template itself

> [!tip] Tip
> Templates open on top of each other. A placement inside a template opens its own template, and `Save & Close` brings you back. The same template cannot be open twice at once. The nesting limit is 8 levels

More - [[2_reuse]]

## Flatten nested prefabs too

Decides what happens to the prefabs inside the one you flatten

**Off** - only the placement you pointed at stops following its template.
A prefab placed inside it stays a placement and keeps its link. Editing that inner template still reaches the level.
This is the default: it is what "unpack this prefab" usually asks for

**On** - everything nested is flattened as well.
After one press, nothing in the level is linked to those inner templates, at any depth

Either way the templates themselves stay in the level. The whole flatten is one undo step
