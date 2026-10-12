---
title: 動画のエクスポート
date: 2026-10-03
tags: [level_author]
---

# 動画のエクスポート

エディターは、コンピューターにインストールされたffmpegを使って、開いているレベルを動画ファイルにレンダリングします。レンダリングはオフラインで1フレームずつ行われるので、マシンがどれだけ遅くても動画は正確です

エクスポートはWindows、macOS、Linuxで動作します。スマートフォンでは使えません

## 開き方

- レベル設定のサイド列にある`{{ui:editor_video-export_open}}`
- コマンドパレットのコマンド`{{ui:cmd_editor_export-video}}`

ウィンドウはエディターの上に開きます。レベル設定から開いた場合は、閉じるとレベル設定に戻ります。動画のレンダリング中はウィンドウを閉じられません：`{{ui:editor_video-export_stop}}`でレンダリングを終了します

## ffmpegのインストール

ffmpegはゲームに含まれていません。一度インストールすれば、ウィンドウが自動で見つけます。バージョン`{{v:ffmpeg.min-version}}`以降が必要です。それより古いものは拒否され、見つかったバージョンがウィンドウに表示されます

| システム | インストールコマンド |
|---|---|
| Windows | `winget install ffmpeg` |
| macOS | `brew install ffmpeg` |
| Linux | ディストリビューションのパッケージ。たとえば`sudo apt install ffmpeg` |

> [!warning] 警告
> 一部のLinuxディストリビューションは、`{{v:ffmpeg.min-version}}`より古いffmpegを同梱しています（Ubuntu 24.04は6.1）。その場合は、ffmpegのサイトから新しいビルドをインストールし、ウィンドウでそのファイルを指定してください

ウィンドウは次の順でffmpegを探します：
1. `{{ui:editor_video-export_ffmpeg_choose}}`で選んだファイル。この場合、ほかの場所は探しません
2. 環境変数`BH_FFMPEG`のパス
3. ゲームのデータフォルダー内の`tools/ffmpeg`
4. `PATH`にあるすべてのフォルダー
5. 一般的なインストーラーが書き込むフォルダー

`{{ui:editor_video-export_ffmpeg_auto}}`は選んだファイルを忘れて、もう一度探します。`{{ui:editor_video-export_ffmpeg_check}}`はチェックをやり直します。たとえばインストール直後に使います

ffmpegにはハードウェアエンコーダー（NVIDIA、AMD、Intel、Apple）が含まれている場合があります。ウィンドウは0.1秒の黒い映像でそれぞれを試し、このコンピューターで実際に動作するものだけを使います

## ウィンドウのオプション

| オプション | 機能 |
|---|---|
| `{{ui:editor_video-export_container}}`、`{{ui:editor_video-export_codec}}` | ファイルの種類と圧縮方法。下の形式を参照してください |
| `{{ui:editor_video-export_resolution}}` | 動画のサイズ。幅と高さは`{{v:video-export.min-size}}`から`{{v:video-export.max-size}}`までの偶数です |
| `{{ui:editor_video-export_fps}}` | 動画の1秒あたりのフレーム数で、最大`{{v:video-export.max-fps}}`。レベル自体のフレームレートには依存しません。`{{v:video-export.min-simulation-rate}}`未満では各フレームが複数のステップでシミュレートされるので、ボットはゲーム内と同じようにプレイします |
| `{{ui:editor_video-export_range}}` | レベル全体、タイムラインのループ範囲、または自分で決めた開始フレームと終了フレーム |
| `{{ui:editor_video-export_quality}}` | 動画が占める容量。もともとロスレスの形式では非表示です |
| `{{ui:editor_video-export_full-chroma}}` | 1ピクセルおきではなく、すべてのピクセルに色を持たせます。細い色付きの線がくっきりしますが、ファイルは大きくなります |
| `{{ui:editor_video-export_seed}}` | レベルのランダム性のシード。`0`ならエディターが使っているシードのままです |
| `{{ui:editor_video-export_preroll}}` | 開始前の何秒間を、記録せずに再生するか。これでエフェクトはすでに履歴を持った状態になります。デフォルトは`{{v:video-export.default-preroll}}`、最大`{{v:video-export.max-preroll}}` |
| `{{ui:editor_video-export_bot}}` | デフォルトは`{{ui:enum_bot-kind_reflex}}`で、ほかに`{{ui:enum_bot-kind_warm}}`、またはアバターなしの動画用の`{{ui:enum_bot-kind_none}}`があります。エクスポート中は被弾しても何も起きません |
| `{{ui:editor_video-export_post-processing}}`、`{{ui:editor_video-export_effects}}` | エディターと同じスイッチで、動画だけに適用されます |
| `{{ui:editor_video-export_audio}}` | 動画に入れるレベルのオーディオトラック |

ウィンドウでは、各オプションに専用の`?`があります

エディターのUI、グリッド、ギズモ、選択、カメラの境界は、動画には入りません。画面はレベルのカメラで構成され、そのアスペクト比で覆えない部分は黒い帯で埋まります

## レンダリング速度

動画はコンピューターの速さに左右されません。レンダリングするフレーム1つごとに、レベルの時間とボットはどちらも動画のちょうど1フレーム分だけ進みます。そのため、遅いマシンでも同じ動画がレンダリングされ、時間が余分にかかるだけです

`{{ui:enum_bot-kind_warm}}`は最初のフレームの前にルート全体を計算し、ウィンドウにその進み具合が表示されます。ルートが見つからない場合、エクスポートは停止し、別のボットを選ぶよう求めます

## 形式

形式は2つの選択で決まります：`{{ui:editor_video-export_container}}`と`{{ui:editor_video-export_codec}}`です。リストには、ffmpegで作れる組み合わせだけが並びます。その下の行に、組み合わせに付くサウンドと、できるファイルが表示されます

| `{{ui:editor_video-export_container}}` | `{{ui:editor_video-export_codec}}` | サウンド | 用途 |
|---|---|---|---|
| `{{ui:editor_video-export_container_mp4}}` | H.264、HEVC、AV1 | `{{ui:editor_video-export_audio-codec_aac}}` | どこへでも送信・アップロードできる |
| `{{ui:editor_video-export_container_mkv}}` | H.264、HEVC、AV1、VP9、FFV1 | `{{ui:editor_video-export_audio-codec_flac}}` | アーカイブ。FFV1なら一切の劣化なし |
| `{{ui:editor_video-export_container_mov}}` | H.264、HEVC、ProRes | `{{ui:editor_video-export_audio-codec_pcm}}` | Premiere、DaVinci Resolve、Final Cutでの編集 |
| `{{ui:editor_video-export_container_webm}}` | VP9、AV1 | `{{ui:editor_video-export_audio-codec_opus}}` | Web |
| `{{ui:editor_video-export_container_gif}}`、`{{ui:editor_video-export_container_webp}}`、`{{ui:editor_video-export_container_apng}}` | なし | サウンドなし | チャットやページ向けの短いループクリップ |
| `{{ui:editor_video-export_container_sequence}}` | PNG、JPEG、WebP、TIFF | フレームの横に`audio.wav` | どの編集ソフトでもインポートできる |
| `{{ui:editor_video-export_container_audio}}` | WAV、FLAC、MP3、Opus | 形式そのもの | レベルのサウンドだけ。何もレンダリングされない |

GIFはクリップ全体で256色のパレットを1つ使います。短く小さく保ってください：レベル全体のGIFは、同じレベルのMP4よりはるかに重くなります

## 動画の保存先

デフォルトでは、動画はゲームのデータフォルダーの`recordings/<level id>/`に、レベル名とエクスポート時刻を含む名前で保存されます。`{{ui:editor_video-export_output_folder}}`でそのフォルダーを開きます。`{{ui:editor_video-export_output_choose}}`を使うと、次の動画をほかの任意の場所に保存します

録画はレベルを削除しても残ります。`{{ui:settings_profile-transfer_category-recordings}}`にチェックを入れない限り、プロファイル転送には含まれません

## サウンド

動画のサウンドはスピーカーから録音されるわけではなく、エクスポート中は何も聞こえません

`{{ui:editor_video-export_engine-audio}}`がオン（デフォルト）で、オーディオトラックにエフェクトがある場合、フレームのレンダリング中にレベルのサウンドがリアルタイムで再生され、エフェクトを含むゲーム自身のサウンドが録音されます。エクスポートには少なくとも範囲の長さだけ時間がかかります：速いコンピューターはサウンドが終わるまで待ちます。オフの場合、オーディオトラックは別々にミックスされ、音量とパンのキーフレームは反映されますが、エフェクトは反映されません。`{{ui:editor_video-export_container_audio}}`は常に別々にミックスします

プレビューの下に、ウィンドウは2本の進行バー`{{ui:editor_video-export_track_frames}}`と`{{ui:editor_video-export_track_sound}}`を表示します：これらは独立して進みます。重いレベルでは、並行して録音するサウンドが途切れることがあります。その場合は`{{ui:editor_video-export_sound-after-frames}}`をオンにします：サウンドは最後のフレームの後に録音され、エクスポートは範囲の長さの分だけ長くかかります

> [!warning] 警告
> 動画のレンダリング中はゲームを閉じないでください。ウィンドウには、実行中ずっとその注意が表示されます

## 動画に入らないもの

- オーディオトラックのエフェクト。ただし、`{{ui:editor_video-export_engine-audio}}`がオフの場合か、`{{ui:editor_video-export_container_audio}}`の場合だけです。レベルにエフェクトがあると、ウィンドウが警告します
- 透明な背景
- 自分がプレイした様子の記録：動画内でプレイできるのはボットだけです

次へ：[[13_export-and-protection]]、[[7_audio]]
