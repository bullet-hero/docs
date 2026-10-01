---
title: Preparing the track
date: 2026-10-01
tags: [level_author]
---

# Preparing the track

Convert the track to ogg: it weighs 8-10 times less than wav and, unlike mp3, adds no silence to the start of the file. Apart from ogg, only mp3 and wav load

## Formats

`oga`, `mp2`, `aiff`, `flac` and the tracker modules `mod`, `xm`, `it`, `s3m` are not accepted

> [!caution] Caution
> `flac` does not load at all: the engine does not decode it. Convert it first

> [!warning] Warning
> An `mp3` encoder adds a few milliseconds of silence to the start, and different encoders add different amounts. If the track is re-encoded by another encoder, the whole beat map shifts

## Offset

Even in `ogg` a track almost never starts exactly on the first beat. That is what the beat segment's offset is for.
It is set in fractional frames, so it is finer than one frame

The order is: tempo first, then the offset, and only then content

## Loudness

Normalise the track before you put it into the level. Peak normalisation to -1 dB is a sensible default

A level noticeably quieter than the next one looks like the game is broken, not the track

## Length

The level's length and the track's length are different numbers, they do not have to match.
A level can end before the track does. That is how you can make an ending with a fade-out

## Several tracks

There can be several tracks. Each has its own position on the timeline, its own speed, volume and chain of effects

Effects: chorus, compressor, distortion, echo, flange, filters, normalisation, equaliser, pitch shifter, reverb

An effect on a track is heard everywhere that track plays, not only where you meant it

Next: [[3_where-to-get-resources]], [[2_rhythm-and-structure]]
