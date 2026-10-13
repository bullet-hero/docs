---
title: 동영상 내보내기
date: 2026-10-03
tags: [level_author]
---

# 동영상 내보내기

에디터는 컴퓨터에 설치된 ffmpeg 프로그램을 통해 열려 있는 레벨을 동영상 파일로 렌더링합니다. 렌더링은 오프라인으로 한 프레임씩 진행되므로, 컴퓨터가 아무리 느려도 동영상은 정확합니다

내보내기는 Windows, macOS, Linux에서 동작합니다. 휴대폰에서는 사용할 수 없습니다

## 찾는 곳

- 레벨 설정 옆 열의 `{{ui:editor_video-export_open}}`
- 명령 팔레트의 `{{ui:cmd_editor_export-video}}` 명령

창은 에디터 위에 열립니다. 레벨 설정에서 열었다면 닫을 때 레벨 설정으로 돌아갑니다. 동영상을 렌더링하는 동안에는 창을 닫을 수 없습니다: `{{ui:editor_video-export_stop}}`(으)로 렌더링을 끝냅니다

## ffmpeg 설치

ffmpeg 프로그램은 게임에 포함되어 있지 않습니다. 한 번 설치하면 창이 스스로 찾아냅니다. `{{v:ffmpeg.min-version}}` 이상의 버전이 필요합니다. 더 오래된 버전은 거부되며, 창에 찾아낸 버전이 표시됩니다

| 시스템 | 설치 명령 |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | 배포판의 패키지, 예: `sudo apt install ffmpeg` |

> [!warning] 경고
> 일부 Linux 배포판은 `{{v:ffmpeg.min-version}}`보다 오래된 ffmpeg 버전을 제공합니다(Ubuntu 24.04에서는 6.1 버전). 이 경우 ffmpeg 사이트에서 더 새로운 빌드를 설치하고 창에서 그 파일을 지정하십시오

창은 다음 순서로 ffmpeg 실행 파일을 찾습니다:
1. `{{ui:editor_video-export_ffmpeg_choose}}`(으)로 고른 파일. 이 경우 다른 곳은 찾지 않습니다
2. 환경 변수 `BH_FFMPEG`의 경로
3. 게임 데이터 폴더 안의 `tools/ffmpeg`
4. `PATH`의 모든 폴더
5. 일반적인 설치 프로그램이 쓰는 폴더

`{{ui:editor_video-export_ffmpeg_auto}}`은(는) 고른 파일을 잊고 다시 찾습니다. `{{ui:editor_video-export_ffmpeg_check}}`은(는) 검사를 다시 합니다. 예를 들어 설치 직후에 씁니다

설치한 ffmpeg에 하드웨어 인코더(NVIDIA, AMD, Intel, Apple)가 들어 있을 수 있습니다. 창은 각 인코더로 0.1초 분량의 검은 화면을 시험하고, 이 컴퓨터에서 실제로 동작하는 인코더만 사용합니다

## 창의 옵션

| 옵션 | 하는 일 |
|---|---|
| `{{ui:editor_video-export_container}}`, `{{ui:editor_video-export_codec}}` | 파일의 종류와 압축 방식. 아래 형식을 참조하십시오 |
| `{{ui:editor_video-export_resolution}}` | 동영상의 크기. 너비와 높이는 `{{v:video-export.min-size}}`부터 `{{v:video-export.max-size}}`까지의 짝수입니다 |
| `{{ui:editor_video-export_fps}}` | 동영상의 초당 프레임 수, 최대 `{{v:video-export.max-fps}}`. 레벨 자체의 프레임 레이트와는 관계없습니다. `{{v:video-export.min-simulation-rate}}` 미만이면 각 프레임을 여러 단계로 시뮬레이션하므로 봇이 게임에서와 똑같이 플레이합니다 |
| `{{ui:editor_video-export_range}}` | 레벨 전체, 타임라인의 반복 범위, 또는 직접 정한 시작 프레임과 끝 프레임 |
| `{{ui:editor_video-export_quality}}` | 동영상이 차지하는 용량. 어차피 무손실인 형식에서는 숨겨집니다 |
| `{{ui:editor_video-export_full-chroma}}` | 두 픽셀마다가 아니라 모든 픽셀마다 색상을 기록합니다. 가는 색 선이 더 선명해지고 파일이 커집니다 |
| `{{ui:editor_video-export_seed}}` | 레벨 무작위성의 시드. 값이 `0`일 때는 에디터가 쓰고 있는 시드를 유지합니다 |
| `{{ui:editor_video-export_preroll}}` | 시작 전에 재생하되 녹화하지 않는 초 수. 이펙트가 이미 이력을 갖고 시작하도록 합니다. 기본값은 `{{v:video-export.default-preroll}}`, 최대 `{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | 기본값 `{{ui:enum_bot-kind_reflex}}`, `{{ui:enum_bot-kind_warm}}`, 또는 아바타 없는 동영상을 위한 `{{ui:enum_bot-kind_none}}`. 내보내는 동안 피격은 아무 영향도 주지 않습니다 |
| `{{ui:editor_video-export_post-processing}}`, `{{ui:editor_video-export_effects}}` | 에디터와 같은 스위치이며, 동영상에만 적용됩니다 |
| `{{ui:editor_video-export_audio}}` | 동영상에 들어가는 레벨의 트랙 |

창에서 모든 옵션에 각각 `?`이(가) 있습니다

에디터 UI, 그리드, 기즈모, 선택, 카메라 경계는 동영상에 절대 들어가지 않습니다. 화면 구도는 레벨의 카메라가 정하며, 카메라의 화면비가 덮지 못하는 부분은 검은 띠로 채워집니다

## 렌더링 속도

동영상은 컴퓨터의 속도와 관계가 없습니다. 레벨 시간과 봇은 렌더링한 프레임마다 정확히 동영상 한 프레임씩 진행하므로, 느린 컴퓨터도 같은 동영상을 렌더링하고 다만 더 늦게 끝낼 뿐입니다

`{{ui:enum_bot-kind_warm}}`은(는) 첫 프레임 전에 전체 경로를 계산하며, 창에 진행 정도가 표시됩니다. 경로를 찾지 못하면 내보내기가 멈추고 다른 봇을 고르라고 요청합니다

## 형식

형식은 두 가지 선택입니다: `{{ui:editor_video-export_container}}`와(과) `{{ui:editor_video-export_codec}}`. 설치한 ffmpeg 프로그램이 만들 수 있는 조합만 목록에 나옵니다. 그 아래 줄에 해당 조합에 어떤 사운드가 붙는지와 어떤 파일이 나오는지 표시됩니다

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | 사운드 | 적합한 용도 |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264, HEVC, AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | 어디로든 보내고 올리기 |
| `{{ui:editor_video-export_container_mkv}}` | H.264, HEVC, AV1, VP9, FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | 보관, FFV1 코덱은 손실이 전혀 없음 |
| `{{ui:editor_video-export_container_mov}}` | H.264, HEVC, ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | Premiere, DaVinci Resolve, Final Cut에서 편집 |
| `{{ui:editor_video-export_container_webm}}` | VP9, AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | 웹 |
| `{{ui:editor_video-export_container_gif}}`, `{{ui:editor_video-export_container_webp}}`, `{{ui:editor_video-export_container_apng}}` | - | 사운드 없음 | 채팅과 웹 페이지용 짧은 반복 클립 |
| `{{ui:editor_video-export_container_sequence}}` | PNG, JPEG, WebP, TIFF | 프레임 옆의 `audio.wav` | 어떤 편집 프로그램이든 가져올 수 있음 |
| `{{ui:editor_video-export_container_audio}}` | WAV, FLAC, MP3, Opus | 형식 자체 | 레벨의 사운드만, 아무것도 렌더링하지 않음 |

GIF 형식은 클립 전체에 256색 팔레트 하나를 씁니다. 짧고 작게 유지하십시오: 레벨 전체를 담은 GIF 파일은 같은 내용의 MP4 파일보다 훨씬 무겁습니다

## 동영상이 저장되는 곳

기본적으로 동영상은 게임 데이터 폴더의 `recordings/<level id>/`에 레벨 이름과 내보낸 시각을 딴 이름으로 저장됩니다. `{{ui:editor_video-export_output_folder}}`은(는) 그 폴더를 엽니다. `{{ui:editor_video-export_output_choose}}`(으)로 다음 동영상을 다른 곳에 저장할 수 있습니다

레벨을 삭제해도 녹화본은 남습니다. `{{ui:settings_profile-transfer_category-recordings}}`에 체크하지 않으면 녹화본은 프로필 이전에 포함되지 않습니다

## 사운드

동영상의 사운드는 스피커에서 녹음하는 것이 아니며, 내보내는 동안에는 아무 소리도 들리지 않습니다

`{{ui:editor_video-export_engine-audio}}`이(가) 켜져 있고(기본값) 트랙에 효과가 걸려 있으면, 프레임을 렌더링하는 동안 레벨의 사운드가 실시간으로 재생되고 게임 자체의 사운드가 효과까지 포함해 녹음됩니다. 내보내기는 최소한 범위의 길이만큼 걸립니다: 빠른 컴퓨터는 사운드가 끝나기를 기다립니다. 꺼져 있으면 트랙을 따로 믹싱하며, 음량과 팬 키프레임은 반영되지만 효과는 빠집니다. `{{ui:editor_video-export_container_audio}}`은(는) 항상 따로 믹싱합니다

미리 보기 아래에 창은 두 타임라인 `{{ui:editor_video-export_track_frames}}`와(과) `{{ui:editor_video-export_track_sound}}`을(를) 보여 줍니다: 둘은 독립적으로 움직입니다. 무거운 레벨에서는 병렬로 녹음하는 사운드가 끊길 수 있습니다. 그럴 때는 `{{ui:editor_video-export_sound-after-frames}}`을(를) 켜십시오: 사운드는 마지막 프레임 뒤에 녹음되며, 내보내기가 범위의 길이만큼 더 오래 걸립니다

> [!warning] 경고
> 동영상을 렌더링하는 동안 게임을 닫지 마십시오. 창이 실행 내내 이 사실을 알립니다

## 동영상에 들어가지 않는 것

- 오디오 트랙의 효과. 단, `{{ui:editor_video-export_engine-audio}}`이(가) 꺼져 있거나 `{{ui:editor_video-export_container_audio}}`에서만 해당합니다. 레벨에 효과가 있으면 창이 경고합니다
- 투명한 배경
- 직접 플레이한 기록: 동영상에서는 봇만 플레이할 수 있습니다

다음 읽을거리: [[13_export-and-protection]], [[7_audio]]
