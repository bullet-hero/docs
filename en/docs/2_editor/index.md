---
title: Level editor
date: 2026-09-24
tags: [level_author]
---

# Level editor

A guide to making levels in the editor built into Bullet Hero: in what order to read it and where the reference of every panel is

The editor is part of the game, not a separate program: you open it from the same client you play in, and a level you build there is a folder of files that anyone with the game can open. This guide is written for level authors, from the first empty folder to a level ready to be published

## What you build

A level is objects that live on a stretch of time and move along keyframes. Time is counted in frames, and every object has a span (a start and a length), a layer, a parent and its own keys per field. What an object draws and what hits the player are separate: a shape and a collider. These six ideas are explained in [[3_how-the-editor-thinks]], and everything else in the editor is built on them

Everything a level uses travels inside its folder: the track, the images and the fonts. The game itself ships no textures, so a level carries its own, and sending a level to someone means sending that folder

## Guide and reference

The docs are split into two kinds of text that are read differently:
- **the guide** explains how to work and why: what a level is made of, where its resources come from and what you may use, how to make it readable and fair, how to work without losing anything, and what devices can take. Its sections build on each other, so on the first pass read them in the order the sidebar shows
- **the reference** says what each panel, field and button does, one section per panel. It is not read through: you open it from a search or from a link in a guide article when you need the exact meaning of something

The two point at each other. A reference section ends with a link to the guide article behind the idea, and guide articles link to the panels they talk about. When a word in either is unfamiliar, the [[1_glossary]] has every term, in tables by topic

## Three places to stop first

- **Before the first level,** read the section [[2_editor/1_basics/index]]. It gives the ideas everything else is built on
- **Before publishing anything,** read the section [[2_editor/3_rights/index]]. A level with music you have no right to share cannot be published, and that is decided by the resources you pick at the very start
- **Before targeting phones,** read the section [[2_editor/6_performance/index]]. A phone holds about 1000 shapes comfortably where an average PC holds 50000

## Related

- [[ugc-licensing-policy]] - the full rules a level has to meet to be published on the official server
- [[3_sdk/index]] - the level format itself, for those who want to read or generate levels outside the editor
