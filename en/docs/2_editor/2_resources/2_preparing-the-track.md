---
title: Preparing the track
date: 2026-09-24
tags: [level_author]
---

# Preparing the track

Which formats load, what to convert to, and why an mp3 may one day shift your whole beat map

## Formats

**Convert the track to `ogg`.** It weighs 8 to 10 times less than `wav`. And unlike `mp3`, it adds no silence to the start of the file

What else loads: `oga`, `mp3`, `mp2`, `wav`, `aiff` and the tracker modules `mod`, `xm`, `it`, `s3m`

> [!caution] Caution
> `flac` does not load at all: the engine does not decode it. Convert it first

> [!warning] Warning
> An `mp3` encoder pads the start with a few milliseconds of silence, and different encoders pad differently. If the track is re-encoded by another encoder, the whole beat map shifts

## Offset

Even in `ogg` a track almost never starts exactly on the first beat. That is what the beat segment's offset is for.
It is set in fractional frames, so it is finer than one frame

The order is: bpm first, then the offset, and only then content

## Loudness

Normalise the track before it goes into the level. Peak normalisation to -1 dB is a reasonable default

A level noticeably quieter than the next one reads as the game being broken rather than the track

## Length

The level's length and the track's length are different numbers and do not have to match.
A level can end before the track does. That is one way to build a fade-out ending

## Several tracks

There can be more than one track. Each has its own position on the timeline, its own speed, volume and chain of effects

Effects: chorus, compressor, distortion, echo, flange, filters, normalisation, EQ, pitch shifter, reverb

An effect on a track is heard everywhere that track plays, not only where you meant it

Next: [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
