---
title: Level settings
date: 2026-09-24
tags: [level_author]
---

# Level settings

The level's own tabs: play, core settings, rules, metadata, history and raw data

## Play

Launch options apply to **this run only**. Nothing here is saved into the level

`Lifes`, `Speed`, `Checkpoints` and auto-level let you rehearse a section without editing it

> [!tip] Tip
> The `Seed` here outranks the level's own seed. It is the top of the three tiers. Use it to replay the exact run you just saw. `0` means use the level's own seed, or a new one each run

More - [[3_difficulty-curve]]

## Core

Frame length, framerate and the level's two seeds

`Level Seed` is the level's own seed. It is part of the content, and changing it can be undone.
`0` means "a new seed every run". It is the default, so an ordinary level plays differently each time

> [!tip] Tip
> `Runtime Seed` only shows which seed this editor session resolved. `Regenerate` rolls a new one for the session only: nothing is written and nothing goes into undo. Reloading the level resolves the seed again

> [!info] Worth knowing
> **A frame is a cell, and time is a boundary.** Frames count from 1. Frame *f* covers the time from (*f*-1)/fps up to but not including *f*/fps. A level of N frames holds frames 1 to N. N+1 is the end boundary, not a frame

More - [[4_frames-and-time]]

## Level Orientation

Which way round the device is held during this level

`Horizontal` and `Vertical` turn the player's device for the duration of the level. This choice outranks the player's setting.
A monitor cannot be turned. So on desktop a vertical level plays inside side bars, and that is how it should look

`Not Specified` leaves the choice to the player. It is not a default but a claim about your level: it reads correctly in **both** orientations.
The game adjusts nothing for it: nothing is reframed, letterboxed or scaled. Content beyond the horizontal edges is off screen in one orientation and visible in the other.
Pick it only after checking the level both ways

## Dangerous Zone

Actions that delete or rewrite files rather than content

> [!caution] Caution
> The `"level" File Format` and `"metadata" File Format` dropdowns rewrite the level and its metadata on disk. Switching format **deletes the file in the old format**. Nothing else happens: no reload, no resimulation, your selection and undo history stay. What is written is exactly what is already in memory

> [!caution] Caution
> `Delete level` removes the level's folder from disk. This cannot be undone

More - [[4_not-losing-work]]

## Rules

Problems that validation found in this level:
- broken references
- duplicate ids
- parent cycles
- prefabs nested too deep
- overlapping beat segments

> [!info] Worth knowing
> **No finding comes with an automatic fix, and that is deliberate.** Every finding is a content decision only you can make. An automatic fix would quietly pick one of several valid answers

> [!tip] Tip
> A child that overhangs its parent's span is **not** reported. That is legal data behaving as designed. If you do want lifetimes fitted, run the `Fit Spans` modifier from the generators. It clamps the children in or expands the parents out

More - [[4_not-losing-work]]

## Metadata

Everything about the level that is not the level itself: name, description, logo, licence, age rating and authors

Name and description are written per language, right here.
A player whose language you did not fill in gets the first one you did

> [!info] Worth knowing
> No translation keys are needed here. A level is content, not part of the game's interface

Licence and authors travel with the level wherever it is shared. That is how credit survives a re-upload

More - [[2_metadata-and-sharing]]

## Level Tags

Tags are your own words. They are shown exactly as written and never translated.
A player filters levels by them in the level browser

Write tags comma-separated. Keep them short and general: a genre, a mood, a mechanic.
A tag helps only if other levels use it too. A tag nobody else will type filters nothing

## History

Every edit this session is a row here. Newest at the top, like a `git log`

The leftmost column is the main line.
A column of its own is a branch. It is a line you left behind when you undid an edit and went another way

The ring marks where you are. The green circle marks the last save

Clicking a row walks the level back to that exact state.
The walk applies one operation per frame. So you watch the level change instead of waiting on a frozen screen

> [!warning] Warning
> The editor is read-only while a walk runs. You can still move the camera and scrub, but not edit. Cancel stops the walk where it is, and that is always a real state of the level

> [!tip] Tip
> History lives in the current session only. It is never written to disk, and reopening the level starts it over. Its size is limited: the oldest abandoned branches go first, then the oldest edits

## Raw Data

The whole saved level model as one tree of fields. It is the file itself, before the editor processes it

> [!caution] Caution
> **Nothing here is validated.** This is the escape hatch for what no other screen covers yet. It will write a value the rest of the editor considers impossible

A filled dot beside a field means you changed it this session.
A hollow dot means something inside it changed. Without it, a change three levels down a collapsed branch would be invisible

The `Apply` button is hidden, not disabled, when there is nothing to apply.
An empty apply would push a level swap onto the undo stack for no reason

More - [[4_not-losing-work]]
