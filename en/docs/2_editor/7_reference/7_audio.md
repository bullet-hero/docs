---
title: Audio
date: 2026-09-24
tags: [level_author]
---

# Audio

The audio track inspector and all 11 audio effects

## Audio track inspector

Shows the selected audio track's clip, speed, fader volume and its chain of audio effects.
The effects: lowpass, highpass, echo, reverb, chorus, pitch shifter, distortion, flange, compressor, normalize and parametric EQ

`Speed` and `Volume` are sliders, not number fields. That way their legal range is visible

> [!caution] Caution
> **Volume here is the fader.** Keyframed volume is a separate track on the Local timeline. The two multiply at playback

More: [[2_preparing-the-track|Preparing the track]]

## Normalize

Continuously brings the signal toward a target loudness. That makes clips from different sources equally loud without hand-tuning.
Reach for it when a level's tracks were not mastered together

It works on overall level. Dynamics inside a track are the job of [[7_audio#Compressor|Compressor]]

- `Lowest Volume` keeps it from amplifying silence and noise into hiss
- `Maximum Amp` caps how far it may boost

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Compressor

Pulls the loud parts down so the quiet ones can sit higher. A compressed track stays audible under everything else in the level and never clips.
It is the usual fix for a song that keeps disappearing behind its own effects

- `Threshold` - where it starts acting
- `Attack` and `Release` - how fast it clamps and lets go. Too fast and it kills transients or pumps audibly
- `Make Up Gain` gives back the level it removed

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Lowpass

Passes the low end and cuts everything above `Cutoff Freq`. It sounds underwater or behind a wall

Bring the cutoff down: the track loses its air first, then its clarity, then everything but the bass.
At the top of the range the filter is nearly transparent. The track sounds the same as the file

> [!tip] Tip
> The effect chain belongs to the **track** and is not keyframed. It cannot change smoothly over time. Cut the track where you want the change and set the two halves apart

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Highpass

The mirror of Lowpass: passes the highs and cuts everything below `Cutoff Freq`

Raise the cutoff: the track thins out into a tiny speaker or a phone call.
It is the usual way to make a section sound small before it opens up

> [!tip] Tip
> The effect chain belongs to the **track** and is not keyframed. It cannot change smoothly over time. Cut the track where you want the change and set the two halves apart

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Param EQ

One parametric band: boosts or cuts a chosen region of the spectrum.
Unlike [[7_audio#Lowpass|Lowpass]] and [[7_audio#Highpass|Highpass]] it can add level as well. So it is the tool for carving room in the mix, not for an effect

- `Center Freq` - where the band sits
- `Octave Range` - how wide the band is. Narrow for a surgical fix, wide for tone shaping
- `Frequency Gain` below 1 cuts, above 1 boosts

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Distortion

Clips the waveform. The sound fills with harmonics it did not have: gritty, overdriven, aggressive.
The simplest effect here: one dial, `Level`, for how hard the clipping bites

As a side effect it flattens dynamics. A heavily distorted track loses its quiet moments.
That is useful when a section should feel relentless. It is destructive when it should not

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Echo

Repeats the signal at a fixed interval. Each repeat is quieter than the last.
The echo is rhythmic and countable. That separates it from [[7_audio#Reverb|Reverb]]'s diffuse tail: you hear separate copies, not a room

- `Delay` - the distance between copies in milliseconds
- `Decay` - how much of each copy feeds the next

Set the delay from the song's tempo and the echoes land on the beat instead of blurring it

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Reverb

Puts the track in a space. First come early reflections off the nearby walls, then a tail that decays away.
It is the largest effect here: its fields describe a room, not a repeat. Repeats are the job of [[7_audio#Echo|Echo]]

Three fields carry most of the sound:
- `Decay Time` - how big the room is
- `Room` - how much of it you hear
- `Room HF` - cut it low and the walls sound soft and absorbent

The rest are shaping dials. Reach for them once those three are right

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Chorus

Lays three slightly delayed copies with a wobbling pitch over the signal. One source sounds like several.
The result is width and thickness, not a repeat. The delays are too short to be heard separately

Three copies separate it from [[7_audio#Flange|Flange]], which sweeps a single one

- `Rate` - the speed of the wobble
- `Depth` - the size of the wobble
- `Feedback` - push it up and the sound walks into flanger territory

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Flange

Mixes the signal with a very short, sweeping delay of itself. The two cancel each other at frequencies that move with the delay.
That moving notch is the jet-engine whoosh you hear. The effect comes from the cancellation, not from the copy

Same family as [[7_audio#Chorus|Chorus]]. But there is one copy and a shorter delay, so you hear a sweep, not width

The notch is deepest when `Dry Mix` and `Wet Mix` are close to each other

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Pitch Shifter

Changes the track's pitch without changing its speed.
That is the whole point: a level's timing is locked to the song. So the track cannot simply be resampled, the way the track's own `Speed` field does it

- `Pitch` - a multiplier. 1 leaves it alone, 2 is an octave up
- `FFT Size` and `Overlap` trade quality against cost

A large shift will sound processed whatever you set

> [!tip] Tip
> The effect chain belongs to the **track** and is not keyframed. It cannot change smoothly over time. Cut the track where you want the change and set the two halves apart

> [!info] Worth knowing
> The **reset** beside this button puts every field back to the developers' defaults, `Mix Level` included. Its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]
