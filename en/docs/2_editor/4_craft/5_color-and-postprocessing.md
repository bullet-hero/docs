---
title: "Colour, themes and post-processing"
date: 2026-09-24
tags: [level_author]
---

# Colour, themes and post-processing

Theme references instead of literal colours, and where style stops and unreadable begins

## Theme references and literal colours

Put content colour through a theme reference.
Use a literal only where the colour is genuinely unique and must follow nothing

A colour can be set two ways:
- **a literal colour** - a value typed straight into the object
- **a theme reference** - "take slot N of the active theme". Which theme is active is set by a keyframe track

The difference shows on the second pass. On references, changing the palette is one edit to the theme. On literals, it is an edit to every object

The background takes its colour from the theme too. How slots and theme keys work - [[6_themes]]

> [!caution] Caution
> Check contrast on every theme, not only on the one you worked in. A level that switches theme on the drop has to stay readable in both. Dark projectiles that read perfectly on a light theme vanish on a dark one

## Post-processing

The standard URP set plus two glitch effects. All keyframed, so every parameter can be animated

> [!caution] Caution
> This is the fastest road to a level nobody can play. Bloom at the top of its range turns any bright object into a smear, and a projectile loses its edge. Chromatic aberration pulls edges apart. A glitch longer than a bar is interference rather than style

Three rules keep post-processing on the side of style:
- turn an effect on at a peak and off again, do not leave it as a backdrop
- never turn on an effect that hurts projectile readability where those projectiles have to be dodged
- had to squint after turning an effect on? Turn it off. The player will not squint, they will quit

## Anti-aliasing

Anti-aliasing is the player's setting, not yours.
A level that only looks right under one mode does not look right for everyone

| Mode | What it does |
|---|---|
| `MSAA` | the default. Resolves geometric edges exactly, and every shape is real geometry |
| `FXAA` | costs one full-screen pass, no matter how much the level overdraws |
| `TAA`, `STP` | not offered: they leave a trail behind fast-moving objects, and a trail behind a projectile hurts readability |

Next: [[1_readability-and-fairness|Readability and fairness]], [[1_level-budget|The level's budget]]
