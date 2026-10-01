---
title: Rhythm and structure
date: 2026-10-01
tags: [level_author]
---

# Rhythm and structure

Map the beat grid first: the tempo, then the offset, then the beats per bar. Put the level's peak on the track's peak, and give the player a breather in the breaks

A rhythm game rests on one sensation: the player is not moving to the music, they are playing it

## The beat grid

The beat grid is for you, not for the game. Playback does not read it.
You use it to place content on the music, and generators work on the same beats

The grid is made of segments. **A segment is a stretch of constant tempo**, and there can be several.
Between segments there can be holes: an intro with no drums, a break, the tail after the last note

Map only the stretches that will carry content. An intro usually needs nothing

## Finding the tempo

1. Find the tempo
2. Then the offset
3. Then the beats per bar

Don't know the tempo? Tap it along with the track in the `Beat Grid` window (`Shift+T`).
Round it to a whole number and fine-tune with the offset

A track is almost always written in a whole-number tempo. A fractional value usually means the offset is wrong, not the tempo

## Sound in motion

**Spread the instruments across different kinds of content:**
- the kick - under whatever requires action from the player
- secondary hits - under motion that requires no action
- long pads and atmosphere - under the background and the camera

Then the level sounds deep instead of hitting one beat with everything at once

**The size of a movement carries the strength of a sound.** A small movement is a weak hit, a large one a strong hit.
A big effect on a weak note reads as a sync error, even when the frames are exact

**The shape of a movement carries the accent.** A sharp turn stresses a strong note, a smooth arc a weak one

**In 4/4 the beats rank by weight as 1, 3, 2, 4.** An action on the first beat is the most intuitive.
Syncopation gives groove. But frequent or inconsistent syncopation leaves the player not knowing where they are

**An unusual time signature is split into groups the player can count.** In 7/4, groups of 4+4+2+2+2 are easier to follow than 4+4+4+2

## Structure

Sections are what a player remembers.
A level without them is four minutes of the same thing, even if something new happens every five seconds

**Repetition teaches.** A pattern that comes back is recognised and learned faster. But too much of it bores, and breaking an established pattern for no reason reads as carelessness, not as variety

> [!tip] Recommendation
> Put markers on the track's structure before you place the first object: intro, verse, chorus, break, drop, outro. They show on every timeline and cost nothing

> [!caution] Caution
> The level's peak has to land on the track's peak, and pauses are mandatory. A break is where the player breathes. A level with no pauses wears people out before it gets difficult

The ending needs thought too: either a final peak or a calm fade-out. A level should not just cut off

## Why segments, not keys

The beat grid is a list of stretches, not a track of keys.
A key track cannot express absence: its last key would stretch to the end of the level. And segments need holes between them

Next: [[4_frames-and-time|Frames, time and the length of a level]], [[3_difficulty-curve|Difficulty and the curve]]
