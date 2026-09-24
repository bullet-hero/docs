---
title: Level settings
date: 2026-09-24
tags: [level_author]
---

# Level settings

The level's own tabs: play, core settings, rules, metadata, history and raw data

## Play

> [!info] Worth knowing
> Launch options for **this run only** - nothing here is saved into the level

> [!tip] Tip
> Lives, speed, checkpoints and auto-level let you rehearse a section without editing it. The **seed** here outranks the level's own: it is the top of the three tiers, and it is the one to use when you want to replay the exact run you just saw

More: [[3_difficulty-curve|Difficulty and the curve]]

## Core

Frame length, framerate and the level's two seeds

> [!info] Worth knowing
> **A frame is a cell, and time is a boundary.** Frame *f* covers the interval from *f*/fps up to but not including (*f*+1)/fps. A level of N frames holds 0 to N-1, and N itself is the end boundary, not a frame

**Seed** is the level's own, and it is undoable content. 0 means "reroll every run" and is the default, so an ordinary level plays differently each time

> [!tip] Tip
> **Runtime Seed** is read-only and shows what this editor session actually resolved. *Regenerate* rolls a new one for the session only - no operation, no undo, nothing written - and reloading the level resolves it from scratch again

More: [[4_frames-and-time|Frames, time and the length of a level]]

## Level Orientation

Which way round this level is meant to be held

**Horizontal** and **Vertical** ask the player device to turn to it while the level plays, and outrank whatever the player set. A monitor cannot be turned, so on desktop a vertical level simply plays inside side bars - which is fine, and is what it should look like

**Not Specified** hands the choice back to the player, and it is a **claim about your level** rather than a default: it says the composition reads correctly in **both** shapes. Nothing is reframed, letterboxed or scaled to make that true, so content placed beyond the horizontal edges is off screen in one orientation and visible in the other. Pick it only after looking at the level both ways

## Dangerous Zone

Actions that destroy or rewrite files rather than content

> [!caution] Caution
> The **file format** dropdowns rewrite the level and its metadata on disk. Rewriting in another format **deletes the file the old one left behind**. Nothing else happens: no reload, no resimulation, no reset of your selection or undo stack, because the model in memory is already exactly what gets written

> [!caution] Caution
> **Delete** removes the level's folder from disk. There is no undo for that one

More: [[4_not-losing-work|Not losing your work]]

## Rules

What validation found in this level: broken references, duplicate ids, parent cycles, prefabs nested too deep, overlapping beat segments

> [!info] Worth knowing
> **No finding carries a repair, and that is deliberate.** Every one of them is a content decision only you can make - an automatic fix would quietly pick one of several valid answers

> [!tip] Tip
> An overhanging child span is **not** reported: that is legal authored data behaving as designed. If you do want lifetimes fitted, run the `span-fit` modifier from Generators, which either clamps children in or expands parents out

More: [[4_not-losing-work|Not losing your work]]

## Metadata

Everything about the level that is not the level: name, description, logo, licence, age rating and authors

> [!info] Worth knowing
> Name and description are **localized strings** - you author the text per language inline, with no keys involved, because a level is content rather than part of the game's interface. A player whose language you did not author falls back to the first entry you did

Licence and authors travel with the level wherever it is shared, which is what makes credit survive a re-upload

More: [[2_metadata-and-sharing|Metadata and sharing a level]]

## Level Tags

Tags are your own words, shown exactly as you write them and never translated - they are what a player filters by in the level browser, so a tag only helps if other levels use the same one

Comma-separated. Keep them short and general: a genre, a mood, a mechanic. A tag nobody else will ever type is a tag that filters nothing

## History

Every edit you make this session is a node here, newest at the top, like a git log. The leftmost column is the main line. A column of its own is a branch - a line you left behind when you undid something and went another way

Clicking any row walks the level back to that exact state. The walk applies one operation per frame, so you watch the level change instead of waiting on a frozen screen

> [!warning] Warning
> The editor is read-only while a walk runs. The viewport still pans and the playhead still scrubs, but nothing can be edited until it lands. Cancel stops it where it is, which is always a real state

The ring marks where you stand. The green circle marks the last save

> [!tip] Tip
> This history lives in the session only. It is never written to disk, reopening the level starts it over, and it is bounded - the oldest abandoned branches go first, then the oldest edits

More: [[10_level-settings#Raw Data|Raw]]

## Raw Data

The whole persisted level model as one tree of fields - the file itself, before any of the editor's opinions about it

> [!caution] Caution
> **Nothing here validates anything.** This is the escape hatch for what no purpose-built screen covers yet, and it will happily write a value the rest of the editor considers impossible

> [!info] Worth knowing
> A filled dot beside a field means you rewrote it this session, a hollow one means something under it changed - without which a change three levels down a collapsed branch would be invisible

**Apply** is absent rather than disabled when there is nothing to commit: an empty commit is a level swap pushed onto the undo stack for no reason

More: [[4_not-losing-work|Not losing your work]]
