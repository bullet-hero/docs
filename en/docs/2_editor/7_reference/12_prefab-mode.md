---
title: Prefab Mode
date: 2026-09-24
tags: [level_author]
---

# Prefab Mode

Editing a prefab in place and flattening nested prefabs

## Prefab Mode

> [!caution] Caution
> You are editing a prefab **template**, not one placement of it. Saving propagates the change to every placement that references this template

A placement is **materialised**, not resolved at load time: the moment you point a placement at a template, real, permanently-numbered copies of its objects are written into the level. By the time a level loads, a prefab child is an entirely ordinary object

A placement can then diverge through **per-instance overrides**, recorded whenever you edit a materialised child *outside* this mode. Editing the template in here records none - that is a template change, not an override

> [!tip] Tip
> Templates open on top of each other - a placement inside this one opens its own template, and "Save & Close" brings you back here. The same template cannot be open twice at once, and 8 levels of nesting is the limit

More: [[2_reuse|Reuse: prefabs, copying, generators]]

## Flatten nested prefabs too

Off - only the placement you pointed at stops following its template. A prefab placed inside it stays a placement and keeps its own link, so editing that inner template still reaches this level. This is the default, because it is what "unpack this prefab" asks for

On - everything nested unpacks as well, and after that nothing in the level is linked to those inner templates any more. One press, and the link count goes to zero at every depth

The templates themselves are kept in the level either way, and a flatten is one undo step
