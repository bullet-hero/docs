---
title: Letting a bot play your level
date: 2026-09-24
tags: [level_author]
---

# Letting a bot play your level

What a bot does, what it never promises, what it costs, and how to use one to test the level you are building

**A bot plays the level for you, with your own controls.** It watches what is coming, works out where there is room, and moves the same character you would - it walks, it dashes, it takes damage and it dies. You pick one before a run, next to lives and speed

**It is not a guarantee that the level gets cleared.** A bot is a player that never gets tired, not a player that never loses. On a section built around a pattern you have to enter correctly a second early, it will be hit - and nothing is broken when that happens

**It costs performance while it runs.** Working out where the room is takes real work on every frame, so on a weak device expect a lower framerate, and on a heavy level expect the first seconds to be the worst

> [!info] Worth knowing
> A bot cannot cheat, and that is how it is built rather than a promise. It has exactly the controls a player has and nothing more - the same speed, the same dash, the same hitbox, the same damage. There is no path through the game that lets it pass through something a player could not

**In the editor a bot steers the preview player.** Settings, `Game Editor`, `Player`: tick `Bot Steers The Player`, then switch the preview player on in the toolbar. There is no choice of bot there, and that is deliberate - only `Reflex Bot v1` needs nothing prepared in advance and keeps working while you edit, at any playback speed, backwards included. Right after a scrub it plays worse for a moment while it rebuilds what it knows about what is coming

> [!tip] Tip
> A bot is a readability check, not a difficulty check. Where it walks calmly through a section you find hard, the section is readable and you are unpractised. Where it is hit again and again in one place, look at that place - it is usually a hazard that arrives with no room to leave, and a human reads that no better

**The overlays say what it sees.** Under the same settings, `Show What The Bot Sees` draws how much room it believes each part of the screen has, the point it is heading for, and how far it thinks it can get. Red is where it expects to be hit. Turn it on while playback is paused, which is where the picture holds still

**Bots get better on levels the developers have never seen.** A level that beats one is worth sending in: open an issue on [the SDK repository](https://github.com/vertoker/bullet-hero-sdk), say which bot lost and where, and attach the level folder. That is the whole way a bot improves - the levels it already clears teach it nothing

Next: [[1_readability-and-fairness|Readability and fairness]], [[3_difficulty-curve|Difficulty]]
