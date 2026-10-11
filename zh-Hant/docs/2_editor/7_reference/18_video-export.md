---
title: 影片匯出
date: 2026-10-03
tags: [level_author]
---

# 影片匯出

編輯器通過你電腦上安裝的ffmpeg，將開啟的關卡渲染為影片檔案。渲染為離線逐幀進行，因此無論電腦多慢，影片都是精確的

匯出支援Windows、macOS和Linux。手機上不可用

## 在哪裡

- 關卡設定側欄中的`{{ui:editor_video-export_open}}`
- 命令面板中的命令`{{ui:cmd_editor_export-video}}`

視窗在編輯器上方開啟。從關卡設定開啟時，關閉後會回到關卡設定。影片渲染期間無法關閉視窗：用`{{ui:editor_video-export_stop}}`中止渲染

## 安裝ffmpeg

ffmpeg不屬於遊戲。安裝一次後，視窗會自動找到它。需要`{{v:ffmpeg.min-version}}`或更新的版本。更舊的版本會被拒絕，視窗會顯示找到的版本

| 系統 | 安裝命令 |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | 發行版自帶的軟體包，例如`sudo apt install ffmpeg` |

> [!warning] 警告
> 部分Linux發行版自帶的ffmpeg早於`{{v:ffmpeg.min-version}}`（Ubuntu 24.04為6.1）。此時請從ffmpeg官網安裝較新的版本，並在視窗中手動指定

視窗按以下順序查詢ffmpeg：
1. 通過`{{ui:editor_video-export_ffmpeg_choose}}`選擇的檔案。此時不再查詢其他位置
2. 環境變數`BH_FFMPEG`中的路徑
3. 遊戲資料資料夾中的`tools/ffmpeg`
4. `PATH`中的每個資料夾
5. 常見安裝程式寫入的資料夾

`{{ui:editor_video-export_ffmpeg_auto}}`會忘記所選檔案並重新查詢。`{{ui:editor_video-export_ffmpeg_check}}`會重新檢查，例如在剛安裝之後

你的ffmpeg可能包含硬體編碼器（NVIDIA、AMD、Intel、Apple）。視窗會用十分之一秒的黑色畫面逐一試用，只使用在此電腦上真正可用的編碼器

## 視窗選項

| 選項 | 作用 |
|---|---|
| `{{ui:editor_video-export_container}}`、`{{ui:editor_video-export_codec}}` | 檔案型別和壓縮方式，見下方格式 |
| `{{ui:editor_video-export_resolution}}` | 影片尺寸。寬和高為`{{v:video-export.min-size}}`至`{{v:video-export.max-size}}`之間的偶數 |
| `{{ui:editor_video-export_fps}}` | 影片每秒幀數，最高`{{v:video-export.max-fps}}`。與關卡自身的幀率無關。低於`{{v:video-export.min-simulation-rate}}`時每幀分多步模擬，讓機器人的表現與遊戲中一致 |
| `{{ui:editor_video-export_range}}` | 整個關卡、時間軸的迴圈範圍，或自定義的起始幀和結束幀 |
| `{{ui:editor_video-export_quality}}` | 影片佔用多少空間。對本身無損的格式隱藏 |
| `{{ui:editor_video-export_full-chroma}}` | 每個畫素都有顏色，而不是每兩個畫素一個。細的彩色線條更清晰，檔案更大 |
| `{{ui:editor_video-export_seed}}` | 關卡隨機性的種子。`0`保持編輯器當前使用的種子 |
| `{{ui:editor_video-export_preroll}}` | 開始前播放但不錄製的秒數，讓特效已有歷史。預設`{{v:video-export.default-preroll}}`，最多`{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | 預設`{{ui:enum_bot-kind_reflex}}`，也可選`{{ui:enum_bot-kind_warm}}`，或`{{ui:enum_bot-kind_none}}`生成沒有化身的影片。匯出期間受擊不產生任何效果 |
| `{{ui:editor_video-export_post-processing}}`、`{{ui:editor_video-export_effects}}` | 與編輯器中相同的開關，僅作用於影片 |
| `{{ui:editor_video-export_audio}}` | 影片中包含關卡的軌道 |

視窗中每個選項都有自己的`?`。

編輯器介面、網格、操作柄、選中框和攝像機邊界永遠不會進入影片。畫面由關卡攝像機決定，其寬高比未覆蓋的部分由黑邊填充

## 渲染速度

影片與電腦速度無關。每渲染一幀，關卡時間和機器人都恰好前進影片的一幀，因此慢的電腦渲染出相同的影片，只是耗時更長

`{{ui:enum_bot-kind_warm}}`會在第一幀之前算好整條路線，視窗會顯示進度。如果找不到路線，匯出會停止並要求選擇其他機器人

## 格式

格式由兩個選項組成：`{{ui:editor_video-export_container}}`和`{{ui:editor_video-export_codec}}`。列表中只有你的ffmpeg能生成的組合。下方一行說明這個組合配套的聲音和最終檔案

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | 聲音 | 適用於 |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264、HEVC、AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | 傳送和上傳到任何地方 |
| `{{ui:editor_video-export_container_mkv}}` | H.264、HEVC、AV1、VP9、FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | 存檔，FFV1完全無損 |
| `{{ui:editor_video-export_container_mov}}` | H.264、HEVC、ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | 在Premiere、DaVinci Resolve、Final Cut中剪輯 |
| `{{ui:editor_video-export_container_webm}}` | VP9、AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | 網頁 |
| `{{ui:editor_video-export_container_gif}}`、`{{ui:editor_video-export_container_webp}}`、`{{ui:editor_video-export_container_apng}}` | 無 | 無聲音 | 用於聊天和網頁的迴圈短片 |
| `{{ui:editor_video-export_container_sequence}}` | PNG、JPEG、WebP、TIFF | 幀旁邊的`audio.wav` | 任何剪輯軟體都能匯入 |
| `{{ui:editor_video-export_container_audio}}` | WAV、FLAC、MP3、Opus | 格式本身 | 僅關卡的聲音，不渲染任何畫面 |

GIF整個片段只使用一個256色的調色盤。請保持簡短、尺寸小：整個關卡的GIF比同一關卡的MP4大得多

## 影片儲存在哪裡

預設情況下，影片儲存到遊戲資料資料夾中的`recordings/<關卡id>/`，以關卡名稱和匯出時間命名。`{{ui:editor_video-export_output_folder}}`開啟該資料夾。`{{ui:editor_video-export_output_choose}}`將下一個影片儲存到其他位置

刪除關卡時錄製檔案會保留。只有勾選`{{ui:settings_profile-transfer_category-recordings}}`時，它們才會包含在存檔轉移中

## 聲音

影片的聲音不是從揚聲器錄製的，匯出期間你聽不到任何聲音。

開啟`{{ui:editor_video-export_engine-audio}}`（預設）且軌道有效果時，關卡的聲音會在渲染幀的同時即時播放，錄製遊戲自身的聲音並包含效果。匯出時間至少為範圍的長度：在較快的電腦上會等待聲音播放完畢。關閉時，軌道單獨混音，保留音量和聲像關鍵幀，但不含效果。`{{ui:editor_video-export_container_audio}}`始終單獨混音

預覽下方顯示兩條進度，`{{ui:editor_video-export_track_frames}}`和`{{ui:editor_video-export_track_sound}}`，它們各自獨立推進。關卡較重時，同時錄製的聲音可能卡頓。此時請開啟`{{ui:editor_video-export_sound-after-frames}}`：聲音會在最後一幀之後錄製，匯出時間會增加一個範圍的長度

> [!warning] 警告
> 影片渲染期間請不要關閉遊戲。整個錄製過程中視窗都會提醒這一點

## 影片中沒有的內容

- 軌道上的效果，僅在關閉`{{ui:editor_video-export_engine-audio}}`或使用`{{ui:editor_video-export_container_audio}}`時。關卡中有這些效果時，視窗會提示
- 透明背景
- 你自己遊玩的錄影：影片中只能由機器人遊玩

繼續閱讀：[[13_export-and-protection]]、[[7_audio]]
