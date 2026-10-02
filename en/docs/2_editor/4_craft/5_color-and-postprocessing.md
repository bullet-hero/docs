---
title: "Colour, themes and post-processing"
date: 2026-10-02
tags: [level_author]
---

# Colour, themes and post-processing

Route content colour through a theme reference, keep literal colours for what is truly unique. Turn post-processing on at a peak and off again, or projectiles lose their edges

## Theme references and literal colours

A colour can be set two ways:
- **a literal colour** - a value typed straight into the object
- **a theme reference** - "take such-and-such slot of the active theme". Which theme is active is set by a keyframe track

The difference shows on the second pass. With references, changing the palette is one edit to the theme. With literals, it is an edit to every object

The background takes its colour from the theme too. How slots and theme keys work - [[6_themes]]

> [!caution] Caution
> Check contrast on every theme, not only on the one you worked in. A level that switches theme on the drop has to stay readable in both. Dark projectiles that read perfectly on a light theme vanish on a dark one

## Post-processing

The standard URP set plus two glitch effects. Everything is on keys, so every parameter can be animated

> [!caution] Caution
> This is the fastest road to a level nobody can play. Bloom at its limit turns any bright object into a blot, and a projectile loses its edge. Chromatic aberration pulls edges apart. A glitch longer than a bar is interference, not style

Three rules keep post-processing on the side of style:
- turn an effect on at a peak and off again, do not leave it as a backdrop
- do not turn on an effect that hurts projectile readability where those projectiles have to be dodged
- had to squint after turning an effect on? Turn it off. The player will not squint, they will quit

## Anti-aliasing

Anti-aliasing is the player's setting, not yours.
A level that looks right in only one mode does not look right for everyone

| Mode | What it does |
|---|---|
| `{{ui:enum_anti-aliasing-type_msaa}}` | the default. Smooths exactly the edges of geometry, and every shape is real geometry |
| `{{ui:enum_anti-aliasing-type_fxaa}}` | costs one pass over the screen, however much the level draws over itself |
| `TAA`, `STP` | not offered: they leave a trail behind fast objects, and a trail behind a projectile makes the level harder to read |

Next: [[1_readability-and-fairness|Readability and fairness]], [[1_level-budget|Level budget]]
