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
- The moment you point a placement at a template, the placement gets real copies of its objects with permanent ids. In the editor a prefab child is an entirely ordinary object
- The level file keeps only the placement: the template, the ids of the copies and the overrides. The copies are rebuilt from the template every time the level loads
- A placement can differ from the template through **per-instance overrides**. They are recorded when you edit such an object *outside* Prefab Mode
- Edits made in Prefab Mode record no overrides. They change the template itself

> [!tip] Tip
> Templates open on top of each other. A placement inside a template opens its own template, and `Save & Close` brings you back. The same template cannot be open twice at once. The nesting limit is 8 levels

More - [[2_reuse]]

## Entering and leaving

There are two ways in:
- `Edit Prefab` in a placement's inspector
- `Edit` on a template's row in the level settings, `Prefabs` tab. It needs no placement, so it also opens a template that is not placed anywhere, or placed only inside another template

`Open in Prefab` in a context menu and in the command palette does the same for a selected placement, or for an object a placement brought. The matching object inside the template is selected straight away

There are two ways out:
- `Save & Close` on the Prefab timeline leaves one level, back to the template that opened this one
- the status on the main toolbar (`Editing '...'`) and `Ctrl+Shift+E` leave every open template at once, back to the level

The selection is cleared every time you enter or leave. Going back one level restores what was selected in that template

Inside a template, selecting works as in the level: click, `Ctrl`-click, a box, deleting, copying and folding. A click in the viewport picks nothing there: the viewport keeps showing the level, and a template has no live preview in it

## Inside a template

Every object of a template hangs off its **root**. The root:
- spans the whole template. Its length is `Frame Length`, the same number on the root's inspector and on the `Prefab` tab
- cannot be deleted or given a parent
- has read-only `Active` and `Layer`. Those belong to each placement

A new object goes under the selected object when exactly one is selected, the root included. Otherwise it goes to the template's top level, under the root.
It spans its parent, anchored at both ends. At the top level that is the whole template

Generators that need the whole level are not available here. Creating a prefab from a selection and flattening a placement are refused inside a template too

## Create a prefab from a selection

Turns the selected objects into a new template and puts one placement of it where they were. The level looks and plays the same afterwards

Where to find it:
- `Create Prefab From This` in a hierarchy row's menu
- the viewport's context menu
- `Create Prefab From Selection` in the command palette, `Ctrl+G`
- `From Selection` in the level settings, `Prefabs` tab

It asks no confirmation and is one undo step. The new placement ends up selected.
One object gives the template its own name. Several objects give a template called `Prefab`. Rename it in the level settings, `Prefabs` tab

What is refused:
- a placement, or an object a placement brought. The menus offer `Open in Prefab` for those instead
- a selection that would nest deeper than 15 levels. Nothing is written, and the message says so

## Flatten a placement

Unlinks a placement from its template: its objects become ordinary level objects and stay exactly where they are

Where to find it: `Flatten Prefab` in the placement's inspector, in a hierarchy row's menu and in the command palette

It always asks first. The level looks the same afterwards, so a flatten done by mistake would otherwise be found much later, when a template edit stops reaching it. Several selected placements give one confirmation and one undo step

An object that a placement brought cannot be flattened on its own. Flatten the placement it belongs to

## Flatten nested prefabs too

Decides what happens to the prefabs inside the one you flatten

**Off** - only the placement you pointed at stops following its template.
A prefab placed inside it stays a placement and keeps its link. Editing that inner template still reaches the level.
This is the default: it is what "unpack this prefab" usually asks for. The switch is off every time the confirmation opens

**On** - everything nested is flattened as well.
After one press, nothing in the level is linked to those inner templates, at any depth

Either way the templates themselves stay in the level. The whole flatten is one undo step
