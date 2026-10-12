---
title: レベルをプレイする
date: 2026-10-11
tags: [player]
---

# レベルをプレイする

レベル一覧でレベルを選び、プレイの条件を設定して開始します。他の人のレベルはただのフォルダーです：levelsフォルダーにコピーして一覧を更新します

## メインメニュー

| ボタン | 機能 |
|---|---|
| `{{ui:menu_main_levels-btn}}` | レベル一覧。下で説明します |
| `{{ui:menu_main_editor-btn}}` | レベルエディター、[[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | レベルなしのアリーナとチュートリアル、[[13_sandbox]] |
| `{{ui:settings_common_title}}` | すべての設定、[[4_settings]] |
| `{{ui:menu_main_story-btn}}` | まだ動作しません |
| `{{ui:menu_main_multiplayer-btn}}` | まだ動作しません |

## レベル一覧

メインメニューの`{{ui:menu_main_levels-btn}}`でレベル一覧が開きます。レベルの出どころは3つです：

- `{{ui:root_level-source_local}}`：`levels`フォルダー、[[1_installation]]
- `{{ui:root_level-source_builtin}}`：ゲームに付属するレベル
- `ワークショップ`：Steam版のみ。サブスクライブしているレベルが表示されます。サブスクライブしているリソースのコレクションはレベルではなく、エディターのライブラリに表示されます、[[16_library-and-collections]]

上部には検索欄、`{{ui:root_level-browser_sort}}`、`{{ui:root_level-browser_layout}}`（グリッドまたはリスト）、`{{ui:root_level-browser_filters}}`があります。一覧はグリッドで開きます。並べ替えの基準は`{{ui:root_level-browser_sort-relevance}}`、`{{ui:root_level-browser_sort-title}}`、`{{ui:root_level-browser_sort-duration}}`、`{{ui:root_level-browser_sort-progress}}`、`{{ui:root_level-browser_sort-recent}}`です。並べ替えボタンの横の矢印（`{{ui:root_level-browser_reverse}}`）で順序が逆になります。`{{ui:root_level-browser_sort-relevance}}`には方向がありません

検索はまずレベル名、次に作者、次にタグを見ます

`{{ui:root_level-browser_filters}}`を押すと、追加のフィルターのウィンドウが開きます。押すたびに、その後ろの一覧が変わります：

- `{{ui:root_level-filters_ai}}`：`{{ui:root_level-filters_ai-yes}}`、`{{ui:root_level-filters_ai-no}}`、`{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}`：最短と最長のレベル、そして長さが不明なレベルを表示するかどうか
- `{{ui:root_level-filters_progress}}`：`{{ui:root_level-filters_progress-unplayed}}`、`{{ui:root_level-filters_progress-started}}`、`{{ui:root_level-filters_progress-cleared}}`、`{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}`：過去24時間、7日、30日
- `{{ui:root_level-filters_age}}`：表示する年齢レーティングの上限
- `{{ui:root_level-filters_other}}`：パスワード付きのレベルを隠す、新しいバージョンのゲームのレベルを隠す
- `{{ui:root_level-filters_tags}}`：タグを1回押すと必須、2回押すと除外

`{{ui:root_level-filters_progress}}`と`{{ui:root_level-filters_recent}}`があるのはメインメニューの一覧だけです。エディターの一覧には独自のフィルターがあります。ボタンには有効なフィルターの数が表示され、`{{ui:root_level-browser_reset}}`ですべてオフになります。フィルターはゲームを閉じるまで設定されたままです

フォルダーにレベルをコピーしましたか？`{{ui:root_level-browser_refresh}}`を押すと一覧が更新されます

カードに鍵のアイコンがあれば、そのレベルはパスワードで保護されています

カードを長押しまたは右クリックすると、`{{ui:level_passphrase_open}}`と`{{ui:root_level-browser_delete}}`のメニューが開きます。`ワークショップ`のレベルで`{{ui:root_level-browser_delete}}`を押すと、アイテムのサブスクライブを解除し、そのファイルを削除します。これにはSteamが起動している必要があります：起動していないと、Steamがレベルを再びダウンロードします。内蔵レベルは削除できません

## 他の人のレベルを追加する

レベルはファイルの入ったただのフォルダーです。アーカイブにして友達に送ることもできます

**フォルダー**。レベルフォルダーを`levels`にコピーし、`{{ui:root_level-browser_refresh}}`を押します。コピーするのはレベルフォルダーそのもの：`level.json`（または`level.blob`）と`metadata.json`が入っているフォルダーです

**アーカイブ**。エディターを開き、`{{ui:gen_level_archive}}`ジェネレーターで新しいレベルを作成します。次に`{{ui:editor_create-level_archive-choose}}`ボタンでファイルを選びます

| ファイル | 結果 |
|---|---|
| `.zip`、`.tar.gz` | 開けます |
| 独自のパスワード付きの`.zip`、`.zip.gpg`、`.tar.gz.gpg` | `{{ui:editor_create-level_archive-protected}}`の後に開けます |
| `.7z` | 今のところ拒否されます。zipに再圧縮してください |
| それ以外 | 拒否されます、[[5_troubleshooting]] |

名前を変えたアーカイブも開けます：ゲームはファイルのバイト列から形式を判別します。古いバージョンのゲームのアーカイブは、インポート時に更新されます

インポートしたレベルには、デフォルトで独自のidが付きます。そのため、デバイス上にすでにあるレベルを上書きしません

詳細：[[6_sharing-by-hand]]

## レベル画面

レベル画面には、カバー、作者、説明、音楽の作者が表示されます。`{{ui:level_level-view_authors}}`と`{{ui:level_level-view_licenses}}`のボタンもあります

作者名と音楽の行は、レベルのメタデータにリンクがあれば、そのリンクを開きます

年齢レーティングはレベルの作者が設定します。ゲームはそれをチェックしません

「AI生成コンテンツを含む」は、レベル、そのカバー、またはリソースのいずれかがAIで生成されたと作者が申告したときに表示されます。これも作者自身の申告です。この行がないことは「AIなし」を意味しません：作者が何も申告していないだけかもしれません

プレイ前に条件を選べます：

| 条件 | 選択肢 |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}`（プレイが終わらない）、`{{ui:menu_levelview_options-lifes_option-one}}`、`{{ui:menu_levelview_options-lifes_option-three}}`、`{{ui:menu_levelview_options-lifes_option-custom}}`（最大16のスライダー） |
| `{{ui:field_common_speed}}` | `0.5`、`1.0`、`2.0`、`{{ui:menu_levelview_options-lifes_option-custom}}`（最大2のスライダー）。レベルと音楽が一緒に変わります |
| `チェックポイント` | オンまたはオフ、[[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | オンまたはオフ。アバターがすべてをすり抜けます、[[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`、`{{ui:enum_bot-kind_reflex}}`、`{{ui:enum_bot-kind_warm}}`、[[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | 数値、`{{ui:level_level-view_seed-randomize}}`、`{{ui:level_level-view_seed-clear}}`。`0`はプレイごとに新しいシード、[[8_determinism]] |

`プレイ`でプレイが始まります

ポーズには`{{ui:game_pause-window_continue-btn}}`、`{{ui:game_pause-window_restart-btn}}`、`{{ui:game_game-result_restart-checkpoint}}`（チェックポイントに到達した後）、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-options}}`、`{{ui:game_game-result_back-to-menu}}`があります。`{{ui:game_game-result_back-to-options}}`は、プレイを開始したときの条件のままレベル画面に戻ります。エディターの`プレイ`タブから開始した場合は、そのタブに戻ります

## 結果ウィンドウ

ウィンドウには`クリア`または`{{ui:game_game-result_lose}}`と、3つのセクション`進行状況`、`{{ui:game_game-result_section-damage}}`、`{{ui:game_game-result_section-conditions}}`が表示されます

- 行：`到達率`、`{{ui:game_game-result_checkpoint}}`、`{{ui:field_common_time}}`、`{{ui:game_game-result_length}}`、`{{ui:game_game-result_hits}}`、`{{ui:game_game-result_lives-left}}`、`{{ui:game_game-result_streak}}`
- プレイの条件：`{{ui:field_common_speed}}`、`{{ui:menu_levelview_options-lifes_title}}`、`{{ui:menu_levelview_options-bot}}`、`{{ui:game_game-result_seed}}`、`チェックポイント`。`{{ui:menu_levelview_options-no-collision_title}}`のプレイでは、`{{ui:menu_levelview_options-lifes_title}}`に`· 衝突なし`が付きます
- ボタン：`{{ui:game_pause-window_restart-btn}}`、`{{ui:game_game-result_restart-checkpoint}}`、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-options}}`、`{{ui:game_game-result_back-to-menu}}`

デフォルトでは、失敗してもウィンドウは開きません。代わりに、プレイが最後のチェックポイントまで巻き戻ります。変更するには：`{{ui:settings_common_title}}`→`{{ui:settings_interface_label}}`→`{{ui:settings_interface_open-menu-on-lose}}`

## 記録

レベル画面には記録ブロックがあります：`{{ui:menu_levelview_record-best}}`、`{{ui:menu_levelview_record-attempts}}`、`{{ui:menu_levelview_record-clears}}`（または`{{ui:menu_levelview_record-none}}`）

記録は条件の組み合わせごとに別々です：ライフ、速度、チェックポイント、衝突、ボット。ブロックには、今選んでいる条件の記録が表示されます。挑戦回数とクリア回数は、どのプレイでも数えられます

記録の選ばれ方：[[10_statistics]]

## カードのマーカー

| マーカー | 意味 |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | ワークショップのフォルダーはディスク上にあるが、サブスクライブしていない。`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general_show-all-found-content}}`がオンのときだけ表示されます |
| `{{ui:root_level-entry_unverified}}` | レベルのソースが応答しなかった |
| `{{ui:root_level-entry_newer-version}}`、`{{ui:root_level-entry_newer-file}}` | このバージョンのゲームではレベルを開けない、[[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | フォルダーに`level.json`がないため、レベルを開始できない、[[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | フォルダーに読み込める`metadata.json`がない。カードにはフォルダー名が表示され、レベルはプレイできる、[[4_level-folder-and-backups]] |

## レベルを削除する

カードを長押しまたは右クリック→`{{ui:root_level-browser_delete}}`。ゲームはまず確認を求めます

レベルと一緒に、その統計（`{{ui:root_level-delete_statistics}}`）とバックアップ（`{{ui:root_level-delete_backups}}`）も削除できます

保護されたレベルを削除するのにパスワードは不要です
