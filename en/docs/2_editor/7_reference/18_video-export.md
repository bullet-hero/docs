---
title: Video export
date: 2026-10-03
tags: [level_author]
---

# Video export

The editor renders the open level into a video file through ffmpeg installed on your computer. Rendering is offline, one frame at a time, so the video is exact however slow the machine is

Export works on Windows, macOS and Linux. It is not available on phones

## Where to find it

- `{{ui:editor_video-export_open}}` in the side column of the level settings
- the command `{{ui:cmd_editor_export-video}}` in the command palette

The window opens over the editor. While a video renders, the window cannot be closed: `{{ui:editor_video-export_stop}}` ends the render

## Installing ffmpeg

ffmpeg is not part of the game. Install it once, and the window finds it by itself. Version `{{v:ffmpeg.min-version}}` or newer is needed. An older one is refused, and the window names the version it found

| System | Install command |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | your distribution's package, for example `sudo apt install ffmpeg` |

> [!warning] Warning
> Some Linux distributions ship an ffmpeg older than `{{v:ffmpeg.min-version}}` (Ubuntu 24.04 ships 6.1). Then install a newer build from the ffmpeg site and point the window at it

The window looks for ffmpeg in this order:
1. the file you chose with `{{ui:editor_video-export_ffmpeg_choose}}`. Then nothing else is searched
2. the path in the environment variable `BH_FFMPEG`
3. `tools/ffmpeg` inside the game's data folder
4. every folder in `PATH`
5. the folders the usual installers write to

`{{ui:editor_video-export_ffmpeg_auto}}` forgets the chosen file and searches again. `{{ui:editor_video-export_ffmpeg_check}}` repeats the check, for example right after installing

Your ffmpeg may contain hardware encoders (NVIDIA, AMD, Intel, Apple). The window tries each one on a tenth of a second of black and uses only the ones that actually work on this computer

## Window options

| Option | What it does |
|---|---|
| `{{ui:editor_video-export_container}}`, `{{ui:editor_video-export_codec}}` | the kind of file and how it is compressed, see the formats below |
| `{{ui:editor_video-export_resolution}}` | the size of the video. Width and height are even numbers from `{{v:video-export.min-size}}` to `{{v:video-export.max-size}}` |
| `{{ui:editor_video-export_fps}}` | frames per second of the video, up to `{{v:video-export.max-fps}}`. It does not depend on the level's own frame rate. Below `{{v:video-export.min-simulation-rate}}` every frame is simulated in several steps, so the bot plays as it does in the game |
| `{{ui:editor_video-export_range}}` | the whole level, the loop range of the timeline, or your own start and end frame |
| `{{ui:editor_video-export_quality}}` | how much space the video takes. Hidden for formats that are lossless anyway |
| `{{ui:editor_video-export_full-chroma}}` | colour for every pixel instead of every second one. Sharper thin coloured lines, a bigger file |
| `{{ui:editor_video-export_seed}}` | the seed of the level's randomness. `0` keeps the seed the editor is using |
| `{{ui:editor_video-export_preroll}}` | how many seconds before the start are played but not recorded, so effects already have their history. `{{v:video-export.default-preroll}}` by default, up to `{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | `{{ui:enum_bot-kind_reflex}}` by default, `{{ui:enum_bot-kind_warm}}`, or `{{ui:enum_bot-kind_none}}` for a video without an avatar. Hits do nothing during an export |
| `{{ui:editor_video-export_post-processing}}`, `{{ui:editor_video-export_effects}}` | the same switches as in the editor, for the video only |
| `{{ui:editor_video-export_audio}}` | the level's tracks in the video |

Every option has its own `?` in the window.

The editor UI, the grid, gizmos, the selection and the camera bounds never get into the video. The camera of the level frames the picture, and black bars fill whatever its aspect does not cover

## Rendering speed

The video does not depend on how fast your computer is. Level time and the bot both advance by exactly one frame of the video per rendered frame, so a slow machine renders the same video, only later

`{{ui:enum_bot-kind_warm}}` works its whole route out before the first frame, and the window shows how far it has got. If it finds no route, the export stops and asks for another bot

## Formats

A format is two choices: `{{ui:editor_video-export_container}}` and `{{ui:editor_video-export_codec}}`. Only the pairs your ffmpeg can make are listed. The line under them says which sound goes with the pair and what file you get

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | Sound | Good for |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264, HEVC, AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | sending and uploading anywhere |
| `{{ui:editor_video-export_container_mkv}}` | H.264, HEVC, AV1, VP9, FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | archiving, FFV1 without any loss |
| `{{ui:editor_video-export_container_mov}}` | H.264, HEVC, ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | editing in Premiere, DaVinci Resolve, Final Cut |
| `{{ui:editor_video-export_container_webm}}` | VP9, AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | the web |
| `{{ui:editor_video-export_container_gif}}`, `{{ui:editor_video-export_container_webp}}`, `{{ui:editor_video-export_container_apng}}` | - | no sound | short looping clips for chats and pages |
| `{{ui:editor_video-export_container_sequence}}` | PNG, JPEG, WebP, TIFF | `audio.wav` beside the frames | any editor imports it |
| `{{ui:editor_video-export_container_audio}}` | WAV, FLAC, MP3, Opus | the format itself | the level's sound alone, nothing is rendered |

GIF takes one palette of 256 colours for the whole clip. Keep it short and small: a GIF of a whole level weighs far more than an MP4 of it

## Where the video goes

By default the video goes to `recordings/<level id>/` in the game's data folder, named after the level and the time of the export. `{{ui:editor_video-export_output_folder}}` opens that folder. `{{ui:editor_video-export_output_choose}}` saves the next video anywhere else

Recordings stay when you delete the level. They are not part of a profile transfer unless you tick `{{ui:settings_profile-transfer_category-recordings}}`

## Sound

The video's sound is not recorded from the speakers, and you hear nothing during an export.

With `{{ui:editor_video-export_engine-audio}}` on (the default) and effects on the tracks, the level's sound plays in real time while the frames render, and the game's own sound is recorded, effects included. The export lasts at least the length of the range: a fast computer waits for the sound to finish. Off, the tracks are mixed separately, with their volume and pan keyframes but without their effects. `{{ui:editor_video-export_container_audio}}` always mixes separately

Under the preview the window shows two timelines, `{{ui:editor_video-export_track_frames}}` and `{{ui:editor_video-export_track_sound}}`: they move independently. On a heavy level the parallel sound can stutter. Then turn on `{{ui:editor_video-export_sound-after-frames}}`: the sound is recorded after the last frame, and the export takes longer by the length of the range

> [!warning] Warning
> Do not close the game while a video renders. The window says so for the whole run

## What is not in the video

- the effects on audio tracks, but only with `{{ui:editor_video-export_engine-audio}}` off or in `{{ui:editor_video-export_container_audio}}`. The window warns when the level has them
- a transparent background
- a recording of how you played: only the bot can play in the video

Read next: [[13_export-and-protection]], [[7_audio]]
