---
title: Audio
date: 2026-10-02
tags: [level_author]
---

# Audio

An audio track's sound goes through a chain of effects: there are 11 of them, from normalize and compressor to echo and reverb. The chain, speed and volume are set in the audio track inspector

## Audio track inspector

Shows the selected audio track's clip, its speed, the fader volume and the chain of effects.
The effects: lowpass, highpass, echo, reverb, chorus, pitch shifter, distortion, flange, compressor, normalize and a parametric equalizer

`{{ui:field_common_speed}}` and `{{ui:editor_inspector-audio_volume}}` are sliders, not input fields. That way the allowed range is visible

> [!caution] Caution
> **The volume here is a fader.** Keyframed volume is a separate track on the local timeline. During playback the two are multiplied

More: [[2_preparing-the-track|Preparing the track]]

## Normalize

Constantly pulls the signal toward a target loudness. That way clips from different sources sound equally loud without manual adjustment.
Use it if the level's tracks were not mixed together

It works on the overall loudness level. The dynamics inside a track are changed by [[7_audio#Compressor|Compressor]]

- `Lowest Volume` keeps it from pulling silence and noise up into hiss
- `Maximum Amp` limits how much it can boost

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Compressor

Pushes the loud parts down so the quiet ones can sound higher. A compressed track is heard under everything else in the level and does not clip.
It is usually used to fix a song that gets lost behind its own effects

- `Threshold` - where it starts working
- `Attack` and `Release` - how fast it clamps down and lets go. Too fast and you cut the attacks or get audible pumping
- `Make Up Gain` gives back the volume it took away

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Lowpass

Lets the lows through and cuts everything above `Cutoff Freq`. Sounds like it is coming from under water or through a wall

Lower the cutoff frequency: the track loses its air first, then its clarity, and in the end everything but the bass.
At the top of the range the filter is almost transparent. The track sounds the same as the file

> [!tip] Tip
> The effect chain belongs to the **track** and is not animated with keyframes. It cannot change smoothly over time. Cut the track where the change is needed and set up the halves differently

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Highpass

The mirror of Lowpass: lets the highs through and cuts everything below `Cutoff Freq`

Raise the cutoff frequency: the track thins out to a tiny speaker or a phone call.
It is usually used to make things sound small before everything opens up

> [!tip] Tip
> The effect chain belongs to the **track** and is not animated with keyframes. It cannot change smoothly over time. Cut the track where the change is needed and set up the halves differently

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Param EQ

One parametric band: boosts or cuts a chosen part of the spectrum.
Unlike [[7_audio#Lowpass|Lowpass]] and [[7_audio#Highpass|Highpass]] it can also add. That is why it is used to clear room in the mix rather than to make an effect

- `Center Freq` - where the band sits
- `Octave Range` - the width of the band. Narrow for a precise fix, wide for overall colouring
- `Frequency Gain` below 1 cuts, above 1 boosts

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Distortion

Clips the waveform. The sound fills with harmonics it did not have: dirty, overdriven, angry.
The simplest effect here: one knob, `Level` - how hard the clipping bites

As a side effect it flattens the dynamics. A heavily distorted track loses its quiet parts.
Where a section should sound relentless, that is useful. Where it should not, it is destructive

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Echo

Repeats the signal at equal intervals. Each repeat is quieter than the previous one.
An echo is rhythmic, and the repeats can be counted. That is what sets it apart from the blurred tail of [[7_audio#Reverb|Reverb]]: you hear separate copies, not a room

- `Delay` - the distance between copies in milliseconds
- `Decay` - what share of each copy goes into the next one

Take the delay from the song's tempo, and the echo will land on the beat instead of smearing it

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Reverb

Puts the track into a space. First come the early reflections from the nearby walls, then a fading tail.
This is the biggest effect here: its fields describe a room, not a repeat. Repeats are the job of [[7_audio#Echo|Echo]]

The main sound is set by three fields:
- `Decay Time` - how big the room is
- `Room` - how much of it is heard
- `Room HF` - cut it and the walls sound soft and absorbent

The rest is fine-tuning. Move on to it once these three fields are right

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Chorus

Layers three slightly delayed copies with a wavering pitch over the signal. One source sounds like several.
The result is width and thickness, not a repeat. The delays are too short to be heard separately

The three copies set it apart from [[7_audio#Flange|Flange]], where one copy sweeps

- `Rate` - the speed of the wavering
- `Depth` - the range of the wavering
- `Feedback` - raise it and the sound moves toward a flanger

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Flange

Mixes a very short, wavering delay of the signal into the signal itself. The two cancel each other out at frequencies that move along with the delay.
That creeping notch is the jet engine whoosh. The effect comes from cancellation, not from a copy

It is the same family as [[7_audio#Chorus|Chorus]]. But there is one copy and the delay is shorter, so you hear a sweep, not width

The notch is deepest when `Dry Mix` and `Wet Mix` are set close to each other

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Pitch Shifter

Changes the track's pitch without changing its speed.
That is the whole point: the level's timing is tied to the song. So the track cannot simply be resampled, the way the track's own `{{ui:field_common_speed}}` field does it

- `Pitch` - a multiplier. 1 changes nothing, 2 raises it by an octave
- `FFT Size` and `Overlap` trade quality for cost

With a large shift the sound will still be heard as processed

> [!tip] Tip
> The effect chain belongs to the **track** and is not animated with keyframes. It cannot change smoothly over time. Cut the track where the change is needed and set up the halves differently

> [!info] Worth knowing
> The **reset** next to this button returns every field to its default, `{{ui:field_common_mix-level}}` included. Its default is the -80 dB floor, so the reset also turns the effect off

More: [[2_preparing-the-track|Preparing the track]]
