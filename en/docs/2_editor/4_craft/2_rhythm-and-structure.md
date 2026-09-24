---
title: Rhythm and structure
date: 2026-09-24
tags: [level_author]
---

# Rhythm and structure

How to map the music, why beat segments have holes in them, and why the level has to peak where the track does

A rhythm game rests on one sensation: the player is not moving to the music, they are playing it

## The beat grid

The beat grid is for you, not for the game. Playback never reads it.
You use it to place content on the music, and generators act on the same beats

The grid is made of segments. **A segment is a stretch of constant tempo**, and there can be several.
Between segments there can be holes: an intro with no percussion, a break, the tail after the last note

Map only the stretches that will carry content. An intro usually needs nothing

## Finding the tempo

1. Find the bpm
2. Then the offset
3. Then the beats per bar

The bpm is unknown? Tap it in along with the track in the `Beat Grid` window (`Shift+T`).
Round it to a whole number and fix the rest with the offset

A track is almost always written on a whole bpm. A fractional value usually means the offset is wrong rather than the tempo

## Mapping the sound

**Split the instruments across different kinds of content:**
- the kick - under whatever requires action from the player
- secondary hits - under motion that requires nothing
- long pads and atmosphere - under the background and the camera

Then the level sounds like it has depth instead of hitting one beat with everything

**The size of a movement carries the strength of a sound.** Small movement, weak hit. Large movement, strong hit.
A big effect on a weak note reads as a sync error even when the frames are exact

**In 4/4 the beats rank 1, 3, 2, 4.** An action on the first beat is the most intuitive there is.
Syncopation gives groove. But syncopation used often or inconsistently stops the player knowing where they are

## Structure

Sections are what a player remembers.
A level without them is four minutes of the same thing, even when something new happens every five seconds

> [!tip] Recommendation
> Put markers on the track's structure before placing the first object: intro, verse, chorus, break, drop, outro. They show on every timeline and cost nothing

> [!caution] Caution
> The level's peak has to land on the track's peak, and rests are mandatory. A break is where the player breathes. A level with none exhausts people before it gets difficult

## Why segments rather than keys

The beat grid is a list of stretches, not a track of keys.
A key track cannot express absence: its last key would reach to the end of the level. And segments need holes between them

Next: [[4_frames-and-time|Frames, time and the length of a level]], [[3_difficulty-curve|Difficulty and the curve]]
