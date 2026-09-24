---
title: Object properties
date: 2026-09-24
tags: [level_author]
---

# Object properties

The object and keyframe inspectors and every property they show

## Object inspector

The selected object's own fields. Every type shows the shared rect fields. Shape, Effect, Text and Prefab objects add their own below them

**Active** gates rendering *and* collision, and is inherited by children - an object hidden here cannot kill the player, which the old visibility flag got wrong

> [!caution] Caution
> **Layer** is relative to the parent, never absolute. The read-only global layer beside it is what the renderer actually uses: your layer plus every ancestor's

> [!tip] Tip
> A field edited on an object that came from a prefab records a **per-instance override** - the checkbox beside it shows and reverts one

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Keyframe inspector

**Every track the selection touches is shown at once**, not just the last one you clicked - a selection can hold position and rotation keys, keys of several objects, and object, audio and event keys together

> [!tip] Tip
> The **Ease** picker works across tracks and commits as a **single undo step**: a selection spanning position and rotation becomes one operation, not two

> [!info] Worth knowing
> The **Frame** field is disabled while several keys are selected. A frame is unique per track, so typing one number for many keys would collapse them onto each other and silently drop all but one - moving several at once is the timeline drag's job

A value shown blank means the selected keys **disagree** on it

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Span

When this object exists, as a half-open range: it covers its start frame up to but not including its end, so an object ending at 20 and one starting at 20 never both draw on that frame

> [!info] Worth knowing
> **A child's span must lie inside its parent's - but that is resolved on read, never stored.** Shrinking a parent clips what its children play without touching what you authored here, so growing it back restores them. A root object running past the end of the level is legal - it simply never plays

> [!info] Worth knowing
> **Anchors** mean "this edge follows the parent's". They are authoring intent only and change nothing at playback

More: [[4_frames-and-time|Frames, time and the length of a level]]

## Easing

How the value moves between this keyframe and the next

> [!info] Worth knowing
> It belongs to the **outgoing** side of a keyframe, so the last keyframe of a track has nothing to ease into and its choice does not show

> [!tip] Tip
> Picking an ease with several keyframes selected applies to all of them as a **single undo step**, even when they span different tracks and different objects. A blank choice means the selected keyframes disagree

## Layer

Draw order, and it is **relative to the parent** rather than absolute

> [!caution] Caution
> What the renderer uses is this number plus every ancestor's, shown read-only in the Global field below. So the same layer means different things under different parents, and reparenting changes where an object draws

> [!info] Worth knowing
> It also feeds randomness: a random value is addressed by the effective layer, so moving an object in the hierarchy rerolls what it drew. Two objects sharing an effective layer AND a start frame therefore draw the same numbers

More: [[3_how-the-editor-thinks|How the editor thinks]]

## Shape

What this object **draws**

> [!info] Worth knowing
> A shape is real geometry, not a picture: it is fitted to its bounding box, so it measures exactly 1 across its longer axis and the object's rect really is what appears on screen

> [!info] Worth knowing
> The game generates around 500 of them from four axes - a form, a sector, a thickness and an invert flag - and a level can add its own on top. Setting this to nothing is valid: an object that draws nothing but still has a hitbox is an invisible wall

More: [[1_readability-and-fairness|Readability and fairness]]

## Collider

What this object **hits** - and it is a separate choice from what it draws

> [!info] Worth knowing
> Neither derives from the other, and that is deliberate: a telegraph beam that is drawn but harmless, a hitbox simpler than the art it guards, and an invisible wall are all ordinary content rather than tricks

> [!tip] Tip
> Both fields pick from the same two collections, so a shape a level authored can serve as either or both

More: [[1_readability-and-fairness|Readability and fairness]]

## Shader Type

Which render path this object takes

> [!caution] Caution
> **Auto** decides once when the level loads, under a hard rule: it must never change how the level looks, so anything it cannot prove is opaque resolves to transparent. Geometry is not an input - it reasons about alpha only

> [!tip] Tip
> The label beside this field shows what Auto actually resolved to. It is read straight from what the renderer consumes rather than worked out again, because a label that disagrees with the pixels is the exact bug it exists to prevent

More: [[1_level-budget|The level's budget]]

## Resolved values

What the selected objects **are** on the current frame, rather than what was authored onto them. Every number is read out of the running simulation, so it can never disagree with what you see in the viewport

The square at the end of a row is that field's keyframe state. Blue - a keyframe sits on this frame, and clicking the square selects it. Amber - the frame lies between two keys and the value is being interpolated. Grey - the track has keys but this frame is outside them, so the value is held. Hollow - the track is empty and the field takes the engine default

The arrows move the playhead to the previous or the next keyframe of that track. A UV row reads as two pairs - tiling first, then offset

Below the rule sit the composed answers - the summed layer, the inherited Active flag and the parent-composed transform. Nothing keyframes those, so they carry no indicator

> [!info] Worth knowing
> An empty keyframe track is valid data rather than missing data - it means the object uses the default for that field

> [!caution] Caution
> Inside Prefab Mode a template plays no frames of its own, so the values read as dashes. The keyframe indicators keep working there, since they read the level file rather than the simulation
