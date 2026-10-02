---
title: "Your first level: the route"
date: 2026-10-02
tags: [level_author]
---

# Your first level: the route

Six steps to the first playtest: create a level, add a track, map the rhythm, place objects, run a playtest, save

## Six steps

This is the order of work only. What each field does is explained by the hint next to its panel

**1. Create the level.** `{{ui:settings_editor-settings_editor-settings}}` → `{{ui:settings_editor-settings_create-level}}`. Pick a preset, set a name and a duration. The duration can be changed later

**2. Add the track.** Copy the audio file into the level folder and hook it up. `ogg` works best, and `flac` does not load. More - [[2_preparing-the-track]]

**3. Map the rhythm.** The `{{ui:editor_inspector-beat_tab}}` tab: BPM, offset, beats per bar. The grid is not for the game, it is for you: content snaps to it

Don't know the tempo? Tap it along with the track in the `{{ui:editor_beat-window_title}}` window (`Shift+T`). Tapping itself has no default key

**4. Place the first objects.** Create an object, give it a shape and put two keys on its position. The game moves the value between keys by itself

**5. Check it.** Run a playtest straight from the editor. Most likely everything will move either far too fast or far too slow. That is normal: speed is only ever tuned by ear

**6. Save.** `Ctrl+S`

Autosave is on by default. {{v:editor.autosave-delay}} seconds after an unsaved edit it saves the level and puts a copy of it in `backups/<level id>/`. More - [[4_not-losing-work#Autosave]]

## Keep the first level small

> [!tip] Recommendation
> Take a short track, 1-2 minutes. A 4-minute level is four times the work and ten times the reasons to abandon it unfinished

Start with the simplest pattern that works, not with the hardest one you thought of.
Play the level end to end yourself before showing it to anyone

Leave generators, prefabs and modifiers for later. They save time on a large level and get in the way on a first one

## The track and rights

A track for yourself needs no one's permission. Rights are checked only when you publish.
More - [[1_licensing-basics]]

The full rules for publishing on the official server - [[ugc-licensing-policy]]

## What next

How the editor works - [[3_how-the-editor-thinks]]

After the first playtest - level design: [[2_editor/4_craft/index]]

When the level grows beyond a sketch - [[1_order-of-work]]
