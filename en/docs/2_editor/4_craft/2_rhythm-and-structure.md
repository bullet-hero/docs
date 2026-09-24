---
title: Rhythm and structure
date: 2026-09-24
tags: [level_author]
---

# Rhythm and structure

How to map the music, why beat segments have holes in them, and why the level has to peak where the track does

A rhythm game rests on one sensation: the player is not moving to the music, they are playing it

## The beat grid

**The beat grid is metadata, not a mechanic.** Playback never reads it. It exists so you can place content on the music, and so generators act on the same beats you see

**A segment is a stretch of constant tempo**, and there can be several. Between them there can be holes - an intro with no percussion, a break, the tail after the last note. That is why this is a list of stretches rather than a track of keys: a key track cannot express absence, and its last point would reach to the end of the level

Map only the stretches that will carry content. An intro usually needs nothing

## Finding the tempo

Find the bpm first, then the offset, then the beats per bar. If the bpm is unknown, tap it in along with the track in the Beat Grid window (`Shift+T`), round to a whole number and fix the rest with the offset

A track is almost always written on a whole bpm. A fractional value usually means the offset is wrong rather than the tempo

## Mapping the sound

**Split the instruments across different kinds of content.** The kick under whatever requires action from the player, secondary hits under motion that requires nothing, long pads and atmosphere under the background and the camera. Then the level sounds like it has depth instead of hitting one beat with everything

**The size of a movement carries the strength of a sound.** Small movement, weak hit. Large movement, strong hit. A big effect on a weak note reads as a sync error even when the frames are exact

**In 4/4 the beats rank 1, 3, 2, 4.** An action on the first beat is the most intuitive there is. Syncopation gives groove, but used often or inconsistently it stops the player knowing where they are

## Structure

Sections are what a player remembers. A level without them is four minutes of the same thing even when something new happens every five seconds

> [!tip] Recommendation
> Put markers on the track's structure - intro, verse, chorus, break, drop, outro - before placing the first object. They show on every timeline and cost nothing

> [!caution] Caution
> The level's peak has to land on the track's peak, and rests are mandatory. A break is where the player breathes, and a level with none exhausts people before it gets difficult

Next: [[4_frames-and-time|Frames, time and the length of a level]], [[3_difficulty-curve|Difficulty and the curve]]
