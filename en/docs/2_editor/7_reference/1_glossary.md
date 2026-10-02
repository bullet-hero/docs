---
title: Glossary
date: 2026-10-02
tags: [level_author]
---

# Glossary

The project's main list of terms. The game's interface, these docs and every other text about Bullet Hero use these words, and a new term is added here first

## Level content

| Term | Meaning |
|---|---|
| **Level** | Everything one playthrough is made of: objects, audio, events and its own resources |
| **Object** | One authored thing on the timeline, with its own lifetime, transform and parent |
| **Rect** | An object that draws nothing: a transform, a lifetime and children. Every other type adds its own on top of it |
| **Shape** | Real geometry an object draws, not a picture. The game generates around 500 of them itself |
| **Collider** | What an object hits with. It may not match what the object draws |
| **Prefab** | A reusable template of objects, placed into a level as many times as needed |
| **Prefab Mode** | Editing a template's own content instead of the level around it |
| **Effect** | A spawner: every frame it creates its own objects from a few parameters |
| **Inframe Object** | An object an effect spawned. The engine owns it: it cannot be selected or edited |
| **Theme** | A palette a level refers to by index: recolouring is one edit, not a hundred |

## Time and animation

| Term | Meaning |
|---|---|
| **Frame** | The unit of level time. A frame is a cell, and time is the boundary between two cells |
| **Keyframe** | One authored value at one frame. Between two keyframes the value is interpolated |
| **Track** | A row of keyframes of one animatable property: position, rotation, volume |
| **Timeline** | The frame axis the level is authored on: one tab for each kind of content |
| **Span** | When an object exists: a start frame and a length, but not an end frame |
| **Playhead** | The frame being shown right now |
| **Ease** | How a value moves from the previous keyframe to this one |
| **Marker** | A named point on the level's ruler, for getting back to the right place |
| **Checkpoint** | Where a death sends the player back to |

## Placement and drawing

| Term | Meaning |
|---|---|
| **Anchor** | An edge that follows the parent's edge: shrink the parent and the child moves with it |
| **Layer** | Draw order, and it is relative: a child's layer is added to its parent's layer |
| **Pivot** | The point an object rotates and scales about, in its own box |
| **Gizmo** | The drag handles drawn on the selected object in the viewport |
| **Snapping** | Pulling a drag onto something: onto content under the magnet, onto the music under the beat toggle |

## Music

| Term | Meaning |
|---|---|
| **Beat** | The music's own grid: the author sets it, and nothing reads it during play |
| **Beat Segment** | One stretch of constant tempo with its own tempo, phase and bar length |
| **BPM** | Beats per minute - how fast a beat segment runs |
| **Tap** | One press while you tap out the tempo. Enough of them describe a beat segment |

## Automation and data

| Term | Meaning |
|---|---|
| **Generator** | Authoring automation: it makes level content from a few parameters |
| **Modifier** | A generator that edits or removes what already exists instead of adding |
| **Seed** | The number every random value in a level is derived from: a run replays exactly the same |
| **Raw Data** | The whole saved model as one editable tree. Nothing is checked here, and that is on purpose |

## Resources and sharing

| Term | Meaning |
|---|---|
| **Library** | Resources on the device for reuse across levels: your library, your collections and the ones you subscribed to |
| **Collection** | A folder of reusable resources of up to seven kinds. Importing copies out of it, so the level does not depend on it |
