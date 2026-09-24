---
title: "Your first level: the route"
date: 2026-09-24
tags: [level_author]
---

# Your first level: the route

Six steps from an empty folder to the first playtest

## Six steps

This is the order of work only. What each field does is explained by the hint next to its panel

**1. Create the level.** `Editor Settings` → `Create Level`. Pick a preset, set a name and a duration. You can change the duration later

**2. Add the track.** Copy the audio file into the level folder and hook it up. `ogg` works best, and `flac` does not load. More - [[2_preparing-the-track]]

**3. Map the rhythm.** The `Beat` tab: bpm, offset, beats per bar. The grid is not for the game, it is for you: content snaps to it

Don't know the bpm? Tap it along with the track in the `Beat Grid` window (`Shift+T`). Tapping itself has no default key

**4. Place the first objects.** Create an object, give it a shape and put two keyframes on its position. The game moves the value between keyframes by itself

**5. Play it.** Run a playtest straight from the editor. Most likely everything will move either far too fast or far too slow. That is normal: speed is only ever tuned by ear

**6. Save.** `Ctrl+S`

Autosave is on by default. 60 seconds after an unsaved edit it saves the level and puts a copy of it in `backups/<level id>/`. More - [[4_not-losing-work#Autosave]]

## Keep the first level small

> [!tip] Recommendation
> Take a short track, 1 to 2 minutes. A 4-minute level is four times the work and ten times the reasons to stop before it is finished

Start with the simplest pattern that works, not with the hardest one you thought of.
Play the level end to end yourself before showing it to anyone

Leave generators, prefabs and modifiers for later. They save time on a large level and get in the way on a first one

## The track and rights

A track for yourself needs no permission from anyone. Rights are checked only when you publish.
More - [[1_licensing-basics]]

The full rules for publishing on the official server - [[ugc-licensing-policy]]

## What next

How the editor works - [[3_how-the-editor-thinks]]

After the first playtest - level design: [[2_editor/4_craft/index]]

When the level grows beyond a sketch - [[1_order-of-work]]
