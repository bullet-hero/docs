---
title: Preparing the track
date: 2026-09-24
tags: [level_author]
---

# Preparing the track

Which formats load, what to convert to, and why an mp3 will quietly shift your whole beat map

## Formats

**What loads:** `ogg` and `oga`, `mp3` and `mp2`, `wav`, `aiff`, plus the tracker modules `mod`, `xm`, `it` and `s3m`

> [!caution] Caution
> `flac` does not load at all - the engine does not decode it. Convert it first

**Convert to `ogg`.** It is compressed, so it weighs 8 to 10 times less than `wav`, and unlike `mp3` it adds no silence to the front of the file

> [!warning] Warning
> An `mp3` encoder pads the start with a few milliseconds of nothing, and different encoders pad differently. The beat map you place against what you hear will be correct until the day the same track is re-encoded by something else, at which point the whole map is off

## Offset

Even with `ogg` a track almost never starts exactly on the first beat. That is what the beat segment's offset is for, and it is measured in fractional frames, so it is finer than one frame

Find the bpm first, then the offset, and only then place content

## Loudness and length

**Loudness.** Normalise the track before it goes into the level. A level noticeably quieter than the next one reads as the game being broken rather than the track. Peak normalisation to -1 dB is a reasonable default

**Length.** The level's length and the track's length are different numbers and are not required to match. A level can end before the track does, which is one way to build a fade-out ending

## Several tracks

There can be more than one track, each with its own position on the timeline, its own speed, its own volume and its own chain of effects - chorus, compressor, distortion, echo, flange, filters, normalisation, EQ, pitch shifter, reverb

An effect on a track is heard everywhere that track plays, not only where you meant it

Next: [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
