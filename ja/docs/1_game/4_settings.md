---
title: 設定
date: 2026-10-02
tags: [player]
---

# 設定

最も重要な設定は初回起動時に決まります。ゲームが自動でクイック設定を開き、言語、音量、パフォーマンス、エフェクトを尋ねます。リセットで変わるのは設定だけで、レベルは残ります

## タブ

| タブ | 内容 |
|---|---|
| `{{ui:settings_general_title}}` | 言語：どの言語もその言語自身で表記されます（`Русский (ru)`）。`システム (ja)`はデバイスに従い、実際にどの言語になったかを表示します。ほかに、同時に読み込むレベルファイルの数、Webアドレスにあるファイルのタイムアウト、`{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | 音量：`{{ui:settings_audio_volume}}`、`{{ui:settings_audio_game}}`、`{{ui:settings_audio_ui}}`、`{{ui:settings_audio_editor-ui}}`、`{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | デバイスと操作方法、[[3_controls]] |
| `{{ui:settings_keybindings_label}}` | ホットキー（主にエディターのもの）、[[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | 画面、フレームレート、アンチエイリアス、`{{ui:settings_graphics-colliders-mode_title}}`、テクスチャ、エフェクト、ポストプロセス |
| `{{ui:settings_interface_label}}` | ゲーム内インターフェース、`{{ui:settings_interface_open-menu-on-lose}}`、`{{ui:settings_interface_menu-background}}`、`{{ui:settings_interface_levels-layout}}`、画面の向き、統計オーバーレイ |
| `{{ui:settings_game-editor_title}}` | エディター独自の設定。エディター用の`{{ui:settings_interface_levels-layout}}`もここにあります |
| `{{ui:settings_profile_tab}}` | 自分の統計、[[10_statistics]] |
| `{{ui:settings_other_title}}` | ストレージの消去、プロファイル転送（[[14_profile-transfer]]）、Androidでのフォルダーへのアクセス、匿名モード、`{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}`は、メインメニューのボタンの後ろに何を表示するかを選びます。ボットが攻撃を回避するライブのアリーナ、回転するシェイプのフィールド、または何も表示しない、のいずれかです

`{{ui:settings_interface_levels-layout}}`は、レベル選択をどの形で開くかを選びます。カバーを並べた`{{ui:enum_level-browser-layout_grid}}`か、説明付きの行を並べた`{{ui:enum_level-browser-layout_list}}`です。この設定は2つあります。`{{ui:settings_interface_label}}`タブのものはメニュー用（デフォルトは`{{ui:enum_level-browser-layout_grid}}`）、`{{ui:settings_game-editor_title}}`タブのものはエディター用（デフォルトは`{{ui:enum_level-browser-layout_list}}`）です。検索欄の横のボタンでも、その画面を離れるまでは表示を切り替えられます

## クイック設定

`{{ui:settings_quick-setup_title}}`は`{{ui:settings_general_title}}`タブの`{{ui:settings_general-open_folder}}`の上にあるボタンで、最も重要な質問をいくつか、1ページに1カテゴリーずつ尋ねます。初回起動時には、チュートリアルの案内より前に自動で開きます。どの回答にも、その回答で何が変わるかを説明する1行があります。ページはどの順番でも開けます。`{{ui:settings_quick-setup_next}}`は次のページを提案するだけです

| ページ | 質問 | 回答 | 変わるもの |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}`とゲームのすべての言語（それぞれその言語自身で表記） | `{{ui:settings_general_title}}`タブと同じ |
| | `{{ui:settings_audio_volume}}` | スライダー | `{{ui:field_common_audio}}`タブと同じ |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`、`{{ui:settings_quick-setup_performance-economy}}`、`{{ui:settings_quick-setup_performance-recommended}}`、`{{ui:settings_quick-setup_performance-max}}` | レンダースケール（PC）、アンチエイリアス、テクスチャサイズ、エフェクトのフレームレート。フレームレートの上限は変わらず、どの回答でも画面のリフレッシュレートで動作します。`{{ui:settings_quick-setup_performance-minimum}}`はさらにパーティクルエフェクトとポストプロセスをオフにし、画像を512に制限します |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`、`{{ui:settings_quick-setup_comfort-soft}}`、`{{ui:settings_quick-setup_comfort-minimal}}` | すべてのポストプロセス効果とアバターの砕け散る演出。`{{ui:settings_quick-setup_comfort-soft}}`はグリッチ、グレイン、ブラー、レンズ歪み、色にじみをオフにします |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | ここでは何も変わりません。チュートリアルではすべての操作方法を試して自分に合うものを選べます。チュートリアルはメインメニューかサンドボックスから開きます |

`{{ui:settings_quick-setup_default-badge}}`の付いた回答は、そのデバイスでゲームが最初に使う設定です。選んだ内容はすぐに適用され、通常の設定画面にも反映されます。設定がどの回答とも一致しない場合は、どれも強調表示されず、その旨が1行で表示されます。これは自分で調整した設定で、回答を押すと置き換えられます

## 折りたたまれたセクション

長いタブはセクションに分かれています。よく変更する項目は開いていて、細かい調整は折りたたまれています。セクションは見出しを押すと開きます。タブのリセットの横にあるボタンで、すべてのセクションをまとめて折りたたんだり展開したりできます

`{{ui:settings_controls_title}}`タブでは、手にしているデバイスのセクションだけが開いています

## リセット

タブごとに専用のリセットがあります。`{{ui:settings_other_title}}`の`{{ui:settings_other_reset}}`は、すべてのタブをまとめてリセットします

リセットで変わるのは設定だけです。レベルは残ります

## バージョン行

設定画面にはバージョン行があります。クリックするとコピーされます

形式は`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`です。バグ報告にはこの行を書いてください、[[11_help]]

## グラフィック

**アンチエイリアス**。PCのデフォルトは`{{ui:enum_anti-aliasing-type_msaa}}`です。スマートフォンはアンチエイリアスなしで始まります。ゲーム内のシェイプはすべて実際のジオメトリで、`{{ui:enum_anti-aliasing-type_msaa}}`はどのプラットフォームでも、ぼかさずにきれいな輪郭を描きます

`{{ui:enum_anti-aliasing-type_fxaa}}`は性能の低いスマートフォン向けです。画面全体に1回処理をかけるだけなので、負荷は一定です。`{{ui:enum_anti-aliasing-type_msaa}}`の負荷は、半透明のシェイプが何枚も重なって描かれるほど大きくなります

TAAは意図的に用意していません。速い弾の後ろに残像が残り、そのジッターがグリッチ効果を邪魔するためです

**フレームレート**。目標フレームレートは垂直同期ではなく手動で設定します。そのため、60Hzの画面でも144Hzの画面でもレベルのタイミングは同じです。`{{ui:settings_graphics_vsync}}`がオンの間（PCのみ）、フレームレートの上限は効きません

> [!tip] 推奨
> 性能の低いデバイスでは、まず**レンダースケール**を1より下げることをおすすめします。失うのはシャープさだけで、インターフェースは元のサイズのままです。PCのみ

詳細：[[2_mobile-devices]]

## コライダーのみモード

練習用のモードで、`{{ui:settings_graphics_title}}`タブの折りたたまれたセクションにあります。`{{ui:settings_graphics-colliders-mode_active}}`をオンにすると、プレイ中のレベルはすべての当たり判定を単色のべた塗りで無地の背景の上に描き、それ以外は何も描きません。消えるもの：シェイプ本来の見た目、コライダーのないシェイプ、エフェクト、テキスト、ポストプロセス、テーマの背景。変わらないもの：音楽、衝突、カメラとその揺れ、チェックポイント、インターフェース、統計。このモードでのプレイも通常のプレイと同じく記録されます。自分のアバターは通常どおり描かれます

このモードが働くのはレベルをプレイしているときだけです。エディター、サンドボックス、メニューの背景は通常どおり描かれます

| オプション | 機能 |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | オン（デフォルト）：塗りは色のアルファに応じて半透明になり、重なった障害物は濃く見えます。アルファは0.15より下がりません。オフ：すべての塗りが不透明になり、色のアルファは固定されます |
| `{{ui:settings_graphics-colliders-mode_color}}` | 塗りの色。デフォルトはアルファ0.6の赤です。エディターのコライダー表示も同じ色相を独自の不透明度で使います |
| `{{ui:settings_graphics-colliders-mode_background}}` | 塗りの後ろに描かれるもの。デフォルトは濃いグレーです。黒にしないのは、カメラの枠の端が周囲の黒帯と区別できるようにするためです |

どちらの色もそれぞれの見出しの下に折りたたまれています。必要な方を展開すると、カラーホイールが表示されます

## 匿名モード

`{{ui:settings_other_title}}` → `{{ui:settings_other_suppress-game-saves}}`でオンにします

このモードの間、ゲームは独自のデータを何も保存しません。`settings.json`、全体の統計、レベルの統計はディスク上でそのまま残ります。変更した設定は、ゲームを閉じるまでは有効です

レベルに関する作業は通常どおり保存されます：保存、エクスポート、インポート、コピー、削除。エディターの自動保存とバックアップも動作します。こちらには専用の切り替えがあります

このモードはゲームを閉じるまで続き、どこにも記憶されません

オフにすると、その時点の設定が保存されます。その間にプレイした記録はすべて破棄されます

> [!info] 補足
> このモードは自動でオンになることもあります。[[12_launch-arguments|起動引数]]`--suppress-game-saves`は起動中ずっとこのモードをオンにし、ゲーム内ではオフにできません。より新しいバージョンのゲームで保存された設定や統計がある場合もオンになります。その場合、ゲームは起動のたびに、それらを残すかデフォルト値で上書きするかを尋ねます
