---
title: Getting started
date: 2026-09-24
tags: [level_author]
---

# Getting started

What a level is, how to build the first one and how the editor thinks about time

This section is the minimum you need before the first level: what a level is on disk, the route to the first playtest, and the handful of ideas the rest of the editor is built on. It describes the model and the order of work, not individual fields - those are explained by the hint next to each panel

## A level is a folder

A Bullet Hero level is an ordinary folder on disk with two main files: `level.json` holds the content and `metadata.json` holds the cover (name, description, authors, tags, duration). Next to them lies everything the level uses: the track, images, fonts. The developers ship no textures, so everything you see in a level is either a built-in shape or a file from that folder

What follows from that:
- a level travels by copying the folder, with no import step
- a backup is a copy of the folder
- a level in `Json` stays readable and repairable by hand, a level in `Blob` loads faster but cannot be read by eye

The data model is open and lives in a separate MIT repository, [bullet-hero-sdk](https://github.com/vertoker/bullet-hero-sdk). Details are in [[1_what-is-a-level]]

## Six ideas

Everything in the editor is built from six ideas, and [[3_how-the-editor-thinks]] explains each one:

| Idea | In one line |
|---|---|
| Object | a shape (what you see) and a collider (what hits you), two separate fields |
| Frame | a cell of time, not a moment |
| Span | an object's lifetime: a start and a duration, the end excluded |
| Layer | draw order, summed with the layers of all parents |
| Parent | passes transform, active state and lifetime down to its children |
| Key | a field's value on one frame, the game interpolates between keys |

## Time is counted in level frames

A level frame is not a screen frame. The number of level frames per second is stored in the level itself (`60` by default, the range is 1 to 1000), so a level plays identically at 60 Hz, at 144 Hz and on a phone that dropped to 30. The level's length and the track's length are separate numbers and do not have to match. [[4_frames-and-time]] covers the consequences, including what happens to content past the end

> [!tip] Recommendation
> Read the section in order, then follow [[2_first-level]] with a short track of 1 to 2 minutes. A 4-minute first level is four times the work and ten times the reasons to stop before it is finished

After the first playtest, go on to level design in [[2_editor/4_craft/index]] and to [[1_order-of-work]] for a level larger than a sketch
