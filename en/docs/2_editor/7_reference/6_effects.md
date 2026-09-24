---
title: Effects
date: 2026-09-24
tags: [level_author]
---

# Effects

The effect inspector, each of its modules and the effect editor

## Effect inspector

A `VFX Graph` effect's parameters, grouped: config, core, forces, shape, angle, scale and colour. Every group is visible at once rather than one at a time

> [!info] Worth knowing
> Effects are **seeded the same way everything else is** - from numbers you edit rather than from generator state - so the same level plays back identically on any device

> [!tip] Tip
> Colours can reference the level theme instead of holding a literal, and gradient types open the shared gradient editor

More: [[1_level-budget|The level's budget]]

## Core

How many particles exist, how long they live and what they are drawn with - everything that is true before a single force is applied. [[6_effects#Forces|Forces]] is the other half

`Particle Count` is the main cost knob and the number a level's capacity hint ultimately counts. Emitter cost is roughly count times lifetime, so doubling `Lifetime Bounds` costs what doubling the count does. `Shape` is the silhouette each particle is drawn with, out of the same pool objects draw from, and `Texture` is the image painted on it - both may be empty, and an untextured particle is the cheap ordinary case

> [!warning] Warning
> The count is capped at 1024, and that ceiling is the graph's own capacity rather than a matter of taste - a VFX graph dispatches over its CAPACITY every frame, not over the particles actually alive, so a system asking for more than it needs costs what it asked for

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, as one undo step

More: [[1_level-budget|What a level can afford]]

## Config

When the emitter stops spawning. Off, it keeps spawning for as long as the object lives, which is the ordinary case - a burst that ends is the object ending

`Stop Frame` is counted from the OBJECT's own span start, not from the level timeline, so an effect placed near the end of a level may legitimately stop three hundred of its own frames later. Particles already alive still finish their lifetime, so the emission stops and the picture fades rather than cutting

> [!info] Worth knowing
> The **reset** beside this button puts both fields back to what the developers ship, as one undo step

More: [[1_level-budget|What a level can afford]]

## Angle

How a particle is rotated over its life, as one of five variants. `Value` is a fixed angle, the two `Curves` variants read a curve, and the two `Random` ones draw between A and B per particle

Which rows exist follows that choice, and the difference between the two curve variants is what the curve is read AGAINST: `Over Life` maps it onto the particle's own lifetime, while `By Speed` maps it onto how fast the particle is going, through the speed window below it

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to what the developers ship, the **Type** included - which discards the curve or the random pair it was holding

More: [[1_readability-and-fairness|Readability]]

## Color

How a particle is tinted over its life. The same five-way split [[6_effects#Angle|Angle]] and [[6_effects#Scale|Scale]] use, with gradients where those two have curves

`Over Life` reads the gradient along the particle's own lifetime and `By Speed` along how fast it is going, while `Random` picks one colour out of the gradient per particle rather than walking it. The two `Random` variants at the bottom draw between two colours instead

> [!tip] Tip
> A colour here can be a theme reference rather than a literal, exactly as anywhere else in a level - which is what lets one effect follow a level that changes its palette partway through

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to what the developers ship, the **Type** included - which discards the gradient or the colour pair it was holding

More: [[5_color-and-postprocessing|Colour and themes]]

## Scale

How big a particle is over its life, in the same five-variant family [[6_effects#Angle|Angle]] uses - a fixed size, a curve, or a range drawn per particle

It is the one place in the group with two curves, because a particle's size has two axes: `Curve X` and `Curve Y` are read independently, so a particle can stretch as it shrinks

> [!warning] Warning
> The row under the curves is REUSED - it is the scale itself under Value and the two Random variants, and the speed window under By Speed. The caption beside it says which one it currently is, and so does its own hint

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to what the developers ship, the **Type** included - which discards both curves and the random pair

More: [[1_readability-and-fairness|Readability]]

## Shape

The spawn volume: a point, a ring, a box, a segment, a cone or a torus. It decides only where a particle STARTS - what happens to it afterwards is [[6_effects#Forces|Forces]]

Changing `Type` changes which fields below exist, and the rows are shared: the first one is a circle's radius, a cone's top radius or a torus' minor radius depending on what is selected. `Arc` is how much of the rim is used, in radians, measured counter-clockwise from the +X axis - less than a full turn makes a fan

> [!tip] Tip
> **Spread** is what turns a static ring into a moving one. It decides where along the rim the next particle lands - randomly, looping in one direction, ping-ponging, or on a sine - and Loop is the classic rotating emitter

> [!info] Worth knowing
> The **reset** beside this button puts the whole group back to what the developers ship, the **Type** included - which discards the shape it was holding, its radii and its spread along with it

More: [[4_composition-and-camera|Composition]]

## Forces

Everything that moves a particle after it spawns. [[6_effects#Shape|Shape]] decides only where it starts, this decides where it goes

The fields split in two kinds, and reading them as one is the usual mistake. The `Start` pairs are drawn ONCE at birth, per particle, between their min and max - spreading a pair is what turns a clean burst into a spray. Everything else acts CONTINUOUSLY for the particle's whole life: `Linear Velocity` is wind rather than an impulse, `Linear Force` is an acceleration and so compounds, and `Orbital Velocity` turns particles around a centre rather than around themselves

> [!tip] Tip
> `Velocity Speed` multiplies the whole result, so a finished effect can be slowed down or sped up without re-tuning a single field above it

> [!info] Worth knowing
> The **reset** beside this button puts all eleven fields back to what the developers ship, as one undo step

More: [[4_composition-and-camera|Composition]]

## Effect editor

Author a particle effect and preview it on the canvas

> [!info] Worth knowing
> The parameter groups are the same ones the Effect inspector shows, edited here as a **draft**: nothing reaches the level until you save

> [!tip] Tip
> Save to the device-wide library to reuse the effect across levels

More: [[1_level-budget|The level's budget]]
