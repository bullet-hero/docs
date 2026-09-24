---
title: "Colour, themes and post-processing"
date: 2026-09-24
tags: [level_author]
---

# Colour, themes and post-processing

Theme references instead of literal colours, and where style stops and unreadable begins

## Theme references and literal colours

A colour can be set two ways, and they are not equivalent. A literal colour is a value typed into the object. A theme reference says "take slot N of the active theme", and which theme is active is itself a keyframe track

The difference shows on the second pass, not the first. On references, changing the palette is one edit to the theme. On literals, it is an edit to every object

So put content colour through a theme reference, and use a literal only where the colour is genuinely unique and must follow nothing. The background is themeable too. How slots and theme keys work is on the page [[6_themes]]

> [!caution] Caution
> Check contrast on every theme, not on the one you worked in. A level that switches theme on the drop has to stay readable in both. Dark projectiles that read perfectly on a light theme vanish on a dark one

## Post-processing

The standard URP set plus two glitch effects, all keyframed, so every parameter can be animated

> [!caution] Caution
> This is the fastest road to a level nobody can play. Bloom at the top of its range turns any bright object into a smear and a projectile stops having an edge. Chromatic aberration pulls edges apart. A glitch held longer than a bar is interference rather than style

Three rules keep it on the side of style:
- turn an effect on at a peak and off again rather than leaving it as a backdrop
- never turn on an effect that changes projectile readability where those projectiles have to be dodged
- if you had to squint after turning an effect on, turn it off. The player will not squint, they will quit

## Anti-aliasing

The default is `MSAA`, which resolves geometric edges exactly - every shape is real geometry. The alternative is `FXAA`, whose cost is one full-screen pass no matter how much the level overdraws. `TAA` and `STP` are not offered, because they leave a trail behind fast-moving objects, and a trail behind a projectile is a readability problem

This is the player's setting rather than yours. A level that only looks right under one mode does not look right for everyone

Next: [[1_readability-and-fairness|Readability and fairness]], [[1_level-budget|The level's budget]]
