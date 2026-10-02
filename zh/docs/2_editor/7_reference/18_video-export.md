---
title: 视频导出
date: 2026-10-03
tags: [level_author]
---

# 视频导出

编辑器通过你电脑上安装的ffmpeg，将打开的关卡渲染为视频文件。渲染为离线逐帧进行，因此无论电脑多慢，视频都是精确的

导出支持Windows、macOS和Linux。手机上不可用

## 在哪里

- 关卡设置侧栏中的`{{ui:editor_video-export_open}}`
- 命令面板中的命令`{{ui:cmd_editor_export-video}}`

窗口在编辑器上方打开。视频渲染期间无法关闭窗口：用`{{ui:editor_video-export_stop}}`中止渲染

## 安装ffmpeg

ffmpeg不属于游戏。安装一次后，窗口会自动找到它。需要`{{v:ffmpeg.min-version}}`或更新的版本。更旧的版本会被拒绝，窗口会显示找到的版本

| 系统 | 安装命令 |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | 发行版自带的软件包，例如`sudo apt install ffmpeg` |

> [!warning] 警告
> 部分Linux发行版自带的ffmpeg早于`{{v:ffmpeg.min-version}}`（Ubuntu 24.04为6.1）。此时请从ffmpeg官网安装较新的版本，并在窗口中手动指定

窗口按以下顺序查找ffmpeg：
1. 通过`{{ui:editor_video-export_ffmpeg_choose}}`选择的文件。此时不再查找其他位置
2. 环境变量`BH_FFMPEG`中的路径
3. 游戏数据文件夹中的`tools/ffmpeg`
4. `PATH`中的每个文件夹
5. 常见安装程序写入的文件夹

`{{ui:editor_video-export_ffmpeg_auto}}`会忘记所选文件并重新查找。`{{ui:editor_video-export_ffmpeg_check}}`会重新检查，例如在刚安装之后

你的ffmpeg可能包含硬件编码器（NVIDIA、AMD、Intel、Apple）。窗口会用十分之一秒的黑色画面逐一试用，只使用在此电脑上真正可用的编码器

## 窗口选项

| 选项 | 作用 |
|---|---|
| `{{ui:editor_video-export_container}}`、`{{ui:editor_video-export_codec}}` | 文件类型和压缩方式，见下方格式 |
| `{{ui:editor_video-export_resolution}}` | 视频尺寸。宽和高为`{{v:video-export.min-size}}`至`{{v:video-export.max-size}}`之间的偶数 |
| `{{ui:editor_video-export_fps}}` | 视频每秒帧数，最高`{{v:video-export.max-fps}}`。与关卡自身的帧率无关。低于`{{v:video-export.min-simulation-rate}}`时每帧分多步模拟，让机器人的表现与游戏中一致 |
| `{{ui:editor_video-export_range}}` | 整个关卡、时间轴的循环范围，或自定义的起始帧和结束帧 |
| `{{ui:editor_video-export_quality}}` | 视频占用多少空间。对本身无损的格式隐藏 |
| `{{ui:editor_video-export_full-chroma}}` | 每个像素都有颜色，而不是每两个像素一个。细的彩色线条更清晰，文件更大 |
| `{{ui:editor_video-export_seed}}` | 关卡随机性的种子。`0`保持编辑器当前使用的种子 |
| `{{ui:editor_video-export_preroll}}` | 开始前播放但不录制的秒数，让特效已有历史。默认`{{v:video-export.default-preroll}}`，最多`{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | 默认`{{ui:enum_bot-kind_reflex}}`，也可选`{{ui:enum_bot-kind_warm}}`，或`{{ui:enum_bot-kind_none}}`生成没有化身的视频。导出期间受击不产生任何效果 |
| `{{ui:editor_video-export_post-processing}}`、`{{ui:editor_video-export_effects}}` | 与编辑器中相同的开关，仅作用于视频 |
| `{{ui:editor_video-export_audio}}` | 视频中包含关卡的轨道 |

窗口中每个选项都有自己的`?`。

编辑器界面、网格、操作柄、选中框和摄像机边界永远不会进入视频。画面由关卡摄像机决定，其宽高比未覆盖的部分由黑边填充

## 渲染速度

视频与电脑速度无关。每渲染一帧，关卡时间和机器人都恰好前进视频的一帧，因此慢的电脑渲染出相同的视频，只是耗时更长

`{{ui:enum_bot-kind_warm}}`会在第一帧之前算好整条路线，窗口会显示进度。如果找不到路线，导出会停止并要求选择其他机器人

## 格式

格式由两个选项组成：`{{ui:editor_video-export_container}}`和`{{ui:editor_video-export_codec}}`。列表中只有你的ffmpeg能生成的组合。下方一行说明这个组合配套的声音和最终文件

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | 声音 | 适用于 |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264、HEVC、AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | 发送和上传到任何地方 |
| `{{ui:editor_video-export_container_mkv}}` | H.264、HEVC、AV1、VP9、FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | 存档，FFV1完全无损 |
| `{{ui:editor_video-export_container_mov}}` | H.264、HEVC、ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | 在Premiere、DaVinci Resolve、Final Cut中剪辑 |
| `{{ui:editor_video-export_container_webm}}` | VP9、AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | 网页 |
| `{{ui:editor_video-export_container_gif}}`、`{{ui:editor_video-export_container_webp}}`、`{{ui:editor_video-export_container_apng}}` | 无 | 无声音 | 用于聊天和网页的循环短片 |
| `{{ui:editor_video-export_container_sequence}}` | PNG、JPEG、WebP、TIFF | 帧旁边的`audio.wav` | 任何剪辑软件都能导入 |
| `{{ui:editor_video-export_container_audio}}` | WAV、FLAC、MP3、Opus | 格式本身 | 仅关卡的声音，不渲染任何画面 |

GIF整个片段只使用一个256色的调色板。请保持简短、尺寸小：整个关卡的GIF比同一关卡的MP4大得多

## 视频保存在哪里

默认情况下，视频保存到游戏数据文件夹中的`recordings/<关卡id>/`，以关卡名称和导出时间命名。`{{ui:editor_video-export_output_folder}}`打开该文件夹。`{{ui:editor_video-export_output_choose}}`将下一个视频保存到其他位置

删除关卡时录制文件会保留。只有勾选`{{ui:settings_profile-transfer_category-recordings}}`时，它们才会包含在存档转移中

## 声音

视频的声音不是从扬声器录制的，导出期间你听不到任何声音。

开启`{{ui:editor_video-export_engine-audio}}`（默认）且轨道有效果时，渲染完帧后关卡会再实时播放一次，录制游戏自身的声音并包含效果。导出时间会增加一个范围的长度。关闭时，轨道单独混音，保留音量和声像关键帧，但不含效果。`{{ui:editor_video-export_container_audio}}`始终单独混音

> [!warning] 警告
> 视频渲染期间请不要关闭游戏。整个录制过程中窗口都会提醒这一点

## 视频中没有的内容

- 轨道上的效果，仅在关闭`{{ui:editor_video-export_engine-audio}}`或使用`{{ui:editor_video-export_container_audio}}`时。关卡中有这些效果时，窗口会提示
- 透明背景
- 你自己游玩的录像：视频中只能由机器人游玩

继续阅读：[[13_export-and-protection]]、[[7_audio]]
