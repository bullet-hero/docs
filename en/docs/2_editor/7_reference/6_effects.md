---
title: Effects
date: 2026-09-24
tags: [level_author]
---

# Effects

The effect inspector, each of its modules and the effect editor

## Effect inspector

Shows a `VFX Graph` effect's parameters in groups: config, core, forces, shape, angle, scale and colour. Every group is visible at once

> [!info] Worth knowing
> Effects are **seeded the same way everything else is**: from numbers you edit, not from generator state. So the level plays back identically on any device

> [!tip] Tip
> Colours can reference the level theme instead of holding a fixed value. Gradient types open the shared gradient editor

More: [[1_level-budget|The level's budget]]

## Core

Sets how many particles exist, how long they live and what they are drawn with. That is everything true before the first force. The other half is [[6_effects#Forces|Forces]]

`Particle Count` is the main cost knob. It is the number the level's capacity hint counts

Emitter cost is roughly count times lifetime. Doubling `Lifetime Bounds` costs as much as doubling the count

`Shape` is each particle's silhouette, from the same pool objects use. `Texture` is the image painted on it. Both may be empty. An untextured particle is the cheap ordinary case

> [!warning] Warning
> The count is capped at 1024. That is the graph's own capacity. A VFX graph processes its whole CAPACITY every frame, not only the particles alive. So a system costs what it asked for, even if it needs less

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, as one undo step

More: [[1_level-budget|What a level can afford]]

## Config

Sets when the emitter stops spawning. When off, it spawns for as long as the object lives. That is the ordinary case: a burst ends when the object ends

`Stop Frame` counts from the OBJECT's own span start, not from the level timeline. So an effect near the end of a level may stop three hundred of its own frames later

Particles already alive live out their lifetime. The emission stops, and the picture fades out rather than cutting

> [!info] Worth knowing
> The **reset** beside this button puts both fields back to the developers' defaults, as one undo step

More: [[1_level-budget|What a level can afford]]

## Angle

Sets how a particle is rotated over its life. There are five variants:
- `Value` - a fixed angle
- the two `Curves` variants read a curve
- the two `Random` variants draw a value between A and B per particle

Which rows exist follows that choice. The two curve variants differ in what the curve is read AGAINST:
- `Over Life` - the particle's own lifetime
- `By Speed` - how fast the particle goes, through the speed window below

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to the developers' defaults, `Type` included. The curve or the random pair it held is lost

More: [[1_readability-and-fairness|Readability]]

## Color

Sets how a particle is tinted over its life. The same five variants as [[6_effects#Angle|Angle]] and [[6_effects#Scale|Scale]], with gradients instead of curves:
- `Over Life` reads the gradient along the particle's lifetime
- `By Speed` reads it by the particle's speed
- `Random` picks one colour from the gradient per particle rather than walking it
- the two `Random` variants at the bottom draw between two colours

> [!tip] Tip
> A colour here can be a theme reference, as anywhere else in a level. That lets an effect follow a level that changes its palette partway through

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to the developers' defaults, `Type` included. The gradient or the colour pair it held is lost

More: [[5_color-and-postprocessing|Colour and themes]]

## Scale

Sets how big a particle is over its life. The same five variants as [[6_effects#Angle|Angle]]: a fixed size, a curve, or a range drawn per particle

There are two curves here, because size has two axes. `Curve X` and `Curve Y` are read independently. A particle can stretch while it shrinks

> [!warning] Warning
> The row under the curves is REUSED. Under `Value` and the two `Random` variants it is the size itself. Under `By Speed` it is the speed window. The caption beside it and its hint say which one it is right now

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to the developers' defaults, `Type` included. Both curves and the random pair are lost

More: [[1_readability-and-fairness|Readability]]

## Shape

Sets the spawn volume: a point, a ring, a box, a segment, a cone or a torus. It decides only where a particle STARTS. What happens next is [[6_effects#Forces|Forces]]

Changing `Type` changes which fields below exist. The rows are shared: the first one is a circle's radius, a cone's top radius or a torus' minor radius, depending on the choice

`Arc` is how much of the rim is used, in radians, counter-clockwise from the +X axis. Less than a full turn makes a fan

> [!tip] Tip
> `Spread` turns a static ring into a moving one. It decides where on the rim the next particle lands: randomly, looping in one direction, ping-ponging, or on a sine. `Loop` is the classic rotating emitter

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to the developers' defaults, `Type` included. The shape it held, with its radii and spread, is lost

More: [[4_composition-and-camera|Composition]]

## Forces

Sets everything that moves a particle after it spawns. [[6_effects#Shape|Shape]] decides where it starts, this group decides where it goes

The fields come in two kinds. Mixing them up is the usual mistake:
- the `Start` pairs are drawn ONCE at birth, per particle, between their min and max. Spread a pair and a clean burst becomes a spray
- everything else acts CONTINUOUSLY for the particle's whole life

The second kind:
- `Linear Velocity` is wind, not an impulse
- `Linear Force` is an acceleration, so it compounds
- `Orbital Velocity` turns particles around a centre, not around themselves

> [!tip] Tip
> `Velocity Speed` multiplies the whole result. So a finished effect can be slowed down or sped up without touching the other fields

> [!info] Worth knowing
> The **reset** beside this button puts all eleven fields back to the developers' defaults, as one undo step

More: [[4_composition-and-camera|Composition]]

## Effect editor

Builds a particle effect and previews it on the canvas

> [!info] Worth knowing
> The parameter groups are the same as in the Effect inspector. Here they are edited as a **draft**: nothing reaches the level until you save

> [!tip] Tip
> Save the effect to the device-wide library to use it in other levels

More: [[1_level-budget|The level's budget]]
