---
title: Audio
date: 2026-09-24
tags: [level_author]
---

# Audio

The audio track inspector and all 11 audio effects

## Audio track inspector

The selected audio track's clip, speed, fader volume and its chain of audio effects - lowpass, highpass, echo, reverb, chorus, pitch shifter, distortion, flange, compressor, normalize and parametric EQ

Speed and volume are sliders rather than plain number fields so their legal range is visible

> [!caution] Caution
> **Volume here is the fader.** Keyframed volume is a separate track on the Local timeline, and the two multiply at playback

More: [[2_preparing-the-track|Preparing the track]]

## Normalize

Continuously brings the signal toward a target loudness. It is what makes clips from different sources sit at a comparable level without hand-tuning each one, so reach for it when a level's tracks were not mastered together

It targets overall level, where [[7_audio#Compressor|Compressor]] shapes dynamics inside a track. `Lowest Volume` is what keeps it from amplifying silence and noise floors into hiss, and `Maximum Amp` caps how far it may go

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Compressor

Pulls the loud parts down so the quiet ones can sit higher. A compressed track stays audible under everything else the level is playing without ever clipping, which is what makes it the usual fix for a song that keeps disappearing behind its own effects

`Threshold` is where it starts acting, `Attack` and `Release` are how fast it clamps and lets go - too fast on either kills transients or pumps audibly - and `Make Up Gain` gives back the level it removed

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Lowpass

Passes the low end and cuts everything above `Cutoff Freq` - the underwater, behind-a-wall sound. Bring the cutoff down and the track loses its air first, then its clarity, then everything but the bass. At the top of the range the filter is effectively transparent, so a track that never touches it sounds exactly as the file does

> [!tip] Tip
> The effect chain belongs to the **track** and is not keyframed, so it cannot sweep over time - cut the track where you want the change and set the two halves apart

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Highpass

The mirror image of Lowpass: passes the highs and cuts everything below `Cutoff Freq`. Raise the cutoff and the track thins out into a tiny speaker or a phone call, which is why it is the usual way to make a section sound small before it opens up

> [!tip] Tip
> The effect chain belongs to the **track** and is not keyframed, so it cannot sweep over time - cut the track where you want the change and set the two halves apart

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Param EQ

One parametric band: boost or cut a chosen region of the spectrum. Unlike the [[7_audio#Lowpass|Lowpass]] and [[7_audio#Highpass|Highpass]] pair it can add level as well as remove it, which is what makes it the tool for carving room rather than for an effect

`Center Freq` is where the band sits, `Octave Range` how wide it is - narrow for a surgical fix, wide for tone shaping - and `Frequency Gain` below 1 cuts while above 1 boosts

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Distortion

Clips the waveform, which fills the sound with harmonics it did not have - gritty, overdriven, aggressive. The simplest effect here: one dial, `Level`, for how hard the clipping bites

It also flattens dynamics as a side effect, so a heavily distorted track stops having quiet moments. That is useful when a section is meant to feel relentless and destructive when it is not

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Echo

Repeats the signal at a fixed interval, each repeat quieter than the last. Rhythmic and countable, which is what separates it from [[7_audio#Reverb|Reverb]]'s diffuse tail - you hear individual copies, not a room

`Delay` is the distance between copies in milliseconds and `Decay` is how much of each one feeds the next. Set the delay from the song's tempo and the echoes land on the beat instead of blurring it

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Reverb

Puts the track in a space: a burst of early reflections off the nearby walls, then a tail that decays away. It is the largest effect here because its fields describe a room rather than a repeat, which is what [[7_audio#Echo|Echo]] does

Three fields carry most of the sound. `Decay Time` is how big the room is, `Room` is how much of it you hear, and `Room HF` cut low reads as soft, absorbent walls. The rest are shaping dials you reach for once those three are right

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Chorus

Lays three slightly delayed, pitch-wobbled copies over the signal so one source sounds like several. The result is width and thickness rather than a repeat - the delays are too short to be heard as separate events

Three taps is what separates it from [[7_audio#Flange|Flange]], which sweeps a single copy. `Rate` is the speed of the wobble and `Depth` its size. Push `Feedback` up and the sound walks into flanger territory

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Flange

Mixes the signal with a very short, sweeping delay of itself. The two cancel each other at frequencies that move as the delay sweeps, and that moving notch is the jet-engine whoosh you hear - the effect is the cancellation, not the copy

Same family as [[7_audio#Chorus|Chorus]], but one modulated copy at a shorter delay, which is why it reads as a sweep rather than as width. `Dry Mix` and `Wet Mix` near each other make the notch deepest

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]

## Pitch Shifter

Transposes the track without changing its speed. That is the whole point of it here: a level's timing is locked to the song, so the track cannot simply be resampled the way the track's own `Speed` field does it

`Pitch` is a multiplier - 1 leaves it alone, 2 is an octave up. `FFT Size` and `Overlap` trade quality against cost, and a large shift will sound processed whatever you set them to

> [!tip] Tip
> The effect chain belongs to the **track** and is not keyframed, so it cannot glide over time - cut the track where you want the change and set the two halves apart

> [!info] Worth knowing
> The **reset** beside this button puts every field back to what the developers ship, **Mix Level** included - and its default is the -80 dB floor, so a reset also switches the effect off

More: [[2_preparing-the-track|Preparing the track]]
