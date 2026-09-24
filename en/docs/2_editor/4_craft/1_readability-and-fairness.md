---
title: Readability and fairness
date: 2026-09-24
tags: [level_author]
---

# Readability and fairness

The player has to understand what killed them. Telegraphs, reaction time, contrast, and a hitbox that need not match the art

There is one test of fairness: **dying, does the player blame themselves or the level.** Everything else here pushes the answer towards the first

**Telegraphing.** A danger has to be visible before it becomes dangerous. A shape and a collider are two separate fields of one object, so a beam that glows but never touches you is an ordinary object with a shape and no collider. Half a second later a second one appears beside it, this time with a collider

The reverse is equally legal: an invisible wall is an object with no shape and a real collider

> [!caution] Caution
> An invisible danger is fair in exactly one case - when the player already knows it is there, because the level showed it earlier

**Reaction time.** A person sees and reacts in roughly 0.2 to 0.25 seconds at best. At 60 level frames per second that is 12 to 15 frames. A danger appearing 10 frames before contact cannot be passed first time, it can only be learned

> [!warning] Warning
> A memorisation level is a legitimate genre, but it has to be a decision rather than an accident

**Contrast.** What is dangerous must differ from the background more than what is decorative. The most common failure is a dark projectile on a dark background at the exact moment the background is also changing

> [!tip] Recommendation
> Take both the background and the projectile colours from the theme. Then one theme edit keeps the contrast everywhere, while hand-typed colours keep it until the first change

**Structure beats density.** A screen full of motion reads as noise rather than as difficulty. A player does not distinguish 40 projectiles, they distinguish a wall with a hole, a wave, a spiral, a corridor. Eight objects with structure are harder and fairer than forty without

> [!info] Worth knowing
> There are no conditions, counters or triggers reacting to what the player does. Everything is authored on the timeline and plays the same way every time, and randomness is addressed rather than drawn - the same spot produces the same numbers on any device. So a level cannot be made reactive, and it also cannot become unfair by accident

> [!caution] Caution
> The number of lives, the playback speed and whether checkpoints are on are chosen by the PLAYER on the launch screen. The defaults are 3 lives, speed 1.0, checkpoints on. Design against the default, but build nothing on "they will die here"

Next: [[3_difficulty-curve|Difficulty and the curve]], [[5_color-and-postprocessing|Colour, themes and post-processing]]
