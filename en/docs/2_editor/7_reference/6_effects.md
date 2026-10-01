---
title: Effects
date: 2026-10-01
tags: [level_author]
---

# Effects

An effect is VFX Graph particles whose parameters are split into modules: how many particles, where they fly out from, how they move, what colour and size they are. You edit them in the inspector or in the effect editor

## Effect inspector

Shows the parameters of a `VFX Graph` effect in groups: config, core, forces, shape, angle, scale and colour. Every group is visible at once

> [!info] Worth knowing
> Effects are **seeded the same way as everything else**: from the numbers you edit, not from generator state. So the level plays back identically on any device

> [!tip] Tip
> Colours can reference the level theme instead of a fixed value. Gradient types open the shared gradient editor

More: [[1_level-budget|The level's budget]]

## Core - how many particles and for how long

Sets how many particles exist, how long they live and what they are drawn with. That is everything true before the first force. The other half is [[6_effects#Forces - what moves a particle|Forces]]

`Particle Count` is the main cost knob. It is exactly the number the level capacity hint counts

An emitter costs roughly its count times its lifetime. Doubling `Lifetime Bounds` costs as much as doubling the count

`Shape` is each particle's silhouette, from the same set ordinary objects use. `Texture` is the image on top of it. Both fields may be empty. A particle without a texture is the cheap ordinary case

> [!warning] Warning
> The count is capped at 1024. That is the capacity of the graph itself. A VFX graph processes its whole CAPACITY every frame, not only the live particles. So a system costs as much as it asked for, even if it needs less

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default in one undo step

More: [[1_level-budget|What a level can afford]]

## Config - when the emitter goes quiet

Sets when the emitter stops spawning. When off, it spawns for as long as the object lives. That is the ordinary case: the burst ends together with the object

`Stop Frame` counts from the start of the OBJECT's own span, not from the level timeline. So an effect at the end of a level may go quiet three hundred of its own frames later

Particles already alive live out their life. The emission is cut off, and the picture fades out smoothly

> [!info] Worth knowing
> The **reset** next to this button returns both fields to their defaults in one undo step

More: [[1_level-budget|What a level can afford]]

## Angle - particle rotation

Sets how a particle is rotated over its life. There are five variants:
- `Value` - a fixed angle
- the two `Curves` variants read a curve
- the two `Random` variants draw a value between A and B for each particle

Which rows exist depends on the choice. The two curve variants differ in WHAT the curve is read by:
- `Over Life` - by the particle's lifetime
- `By Speed` - by the particle's speed, through the speed window below

> [!info] Worth knowing
> The **reset** next to this button returns the whole group to its defaults, `Type` included. The curve or random pair you set up is lost

More: [[1_readability-and-fairness|Readability]]

## Color - particle colour

Sets how a particle is coloured over its life. Six variants: the same five as [[6_effects#Angle - particle rotation|Angle]] and [[6_effects#Scale - particle size|Scale]], only with gradients instead of curves, plus one more gradient `Random`:
- `Over Life` reads the gradient by the particle's lifetime
- `By Speed` reads it by the particle's speed
- `Random` takes one colour from the gradient per particle instead of moving along it
- the two `Random` variants at the bottom draw a colour between two colours

> [!tip] Tip
> A colour here can be a theme reference, as anywhere else in the level. That way the effect follows a level that changes its palette along the way

> [!info] Worth knowing
> The **reset** next to this button returns the whole group to its defaults, `Type` included. The gradient or colour pair you set up is lost

More: [[5_color-and-postprocessing|Colour and themes]]

## Scale - particle size

Sets a particle's size over its life. The same five variants as [[6_effects#Angle - particle rotation|Angle]]: a fixed size, a curve or a range per particle

There are two curves here, because size has two axes. `Curve X` and `Curve Y` are read independently. A particle can stretch and shrink at the same time

> [!warning] Warning
> The row under the curves is REUSED. Under `Value` and the two `Random` variants it is the size itself. Under `By Speed` it is the speed window. The caption next to it and its hint tell what the row is right now

> [!info] Worth knowing
> The **reset** next to this button returns the whole group to its defaults, `Type` included. Both curves and the random pair are lost

More: [[1_readability-and-fairness|Readability]]

## Shape - where particles fly out from

Sets the spawn volume: a point, a ring, a rectangle, a segment, a cone or a torus. It decides only where a particle STARTS. What happens to it next is [[6_effects#Forces - what moves a particle|Forces]]

Changing `Type` changes the set of fields below. The rows are reused: the first one is a circle's radius, a cone's top radius or a torus' minor radius, depending on what is selected

`Arc` is how much of the rim is used, in radians, counter-clockwise from the +X axis. Less than a full turn gives a fan

> [!tip] Tip
> `Spread` turns a static ring into a moving one. It decides where on the rim the next particle lands: randomly, round in one direction, back and forth or along a sine. `Loop` is the classic rotating emitter

> [!info] Worth knowing
> The **reset** next to this button returns the whole group to its defaults, `Type` included. The shape you set up, with its radii and spread, is lost

More: [[4_composition-and-camera|Composition]]

## Forces - what moves a particle

Sets everything that moves a particle after it spawns. [[6_effects#Shape - where particles fly out from|Shape]] decides where it starts, and this group decides where it flies

The fields come in two kinds. Mixing them up is the usual mistake:
- the `Start` pairs are drawn ONCE when a particle is born, between their minimum and maximum. Spread a pair apart and an even burst becomes a fan
- everything else acts CONTINUOUSLY for the particle's whole life

Fields of the second kind:
- `Linear Velocity` is wind, not a push
- `Linear Force` is an acceleration, so it accumulates
- `Orbital Velocity` turns particles around the centre, not around themselves

> [!tip] Tip
> `Velocity Speed` multiplies the whole result. That way a finished effect can be slowed down or sped up without touching the other fields

> [!info] Worth knowing
> The **reset** next to this button returns all eleven fields to their defaults in one undo step

More: [[4_composition-and-camera|Composition]]

## Effect editor

Builds a particle effect and shows it on the canvas

> [!info] Worth knowing
> The parameter groups are the same as in the effect inspector. Here they are edited as a **draft**: nothing reaches the level until you save

> [!tip] Tip
> Save the effect to the device's shared library to use it in other levels

More: [[1_level-budget|The level's budget]]
