---
title: スピードとショートカット
date: 2026-10-02
tags: [level_author]
---

# スピードとショートカット

最も時間を節約できるのは、コマンドパレット（Ctrl+Shift+P）、コンテンツ検索（Ctrl+F）、「位置を表示」ボタン、タイムライン上の矢印キーです。どのキーも設定で割り当て直せます

## 時間を最も節約する4つの機能

- **`{{ui:editor_search-title_command}}`**（`Ctrl+Shift+P`）：エディターでできることのすべてを、名前で検索できます。ボタンがどのパネルにあるかを思い出すより速く済みます
- **`コンテンツを検索`**（`Ctrl+F`）：名前でオブジェクトやオーディオトラックに移動します。再生ヘッドも一緒に移動します
- **`{{ui:cmd_editor_ping}}`**：ビューポートが選択中の項目を画面に収め、タイムラインとヒエラルキーがそこまでスクロールします。すべて同時です。もう一度押すと、複数選択の次のオブジェクトに進みます
- **タイムライン上の矢印キー**：リスト内の順番ではなく、方向で移動します。マウスを使わずに隣のキーフレームへ移れます

## デフォルト

以下のグループと名前は、`{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`に表示されるものと同じです

### 再生

| キー | 設定での名前 | 動作 |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | 再生と一時停止 |

### 編集

| キー | 設定での名前 | 動作 |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | 元に戻す |
| `Ctrl+Y`または`Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | やり直し |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | 保存 |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | コピー |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | 貼り付け |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | 複製 |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | 選択からプレハブを作成 |

### 選択

| キー | 設定での名前 | 動作 |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | 選択中の項目を削除 |
| `Ctrl`を押し続ける | `{{ui:settings_keybindings_editor_multi_select}}` | 複数選択 |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | すべての選択を一度に解除：オブジェクト、キーフレーム、オーディオ、ビート |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | プレハブモードを終了してレベルに戻る |

### 表示

| キー | 設定での名前 | 動作 |
|---|---|---|
| `Ctrl+F` | `コンテンツを検索` | コンテンツを検索 |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | コマンドを実行 |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | 左パネルの表示と非表示を切り替え |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | 右パネルの表示と非表示を切り替え |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | 下パネルの表示と非表示を切り替え |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | ビューポート上のツールグループの表示と非表示を切り替え |
| `` ` ``を押し続ける | `{{ui:settings_keybindings_editor_preview}}` | プレビュー：キーを押している間、エディターのインターフェースが非表示になります |

### タイムライン

| キー | 設定での名前 | 動作 |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | 折りたたみを順に切り替え：すべてのサブツリー、選んだ種類のみ、なし |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | スナップのオンとオフを切り替え |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | 選択ツール |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | 矩形選択ツール |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | ハサミツール |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | エッジツール |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | タイムライン上の選択したオブジェクトを折りたたむ |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | レベルタイムラインを開く |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | ローカルタイムラインを開く |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | オーディオタイムラインを開く |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | イベントタイムラインを開く |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | プレハブタイムラインを開く |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | ビートグリッドのウィンドウ。ここでテンポをタップして刻みます。`{{ui:settings_keybindings_editor_beat_tap}}`自体にはデフォルトのキーがないので、必要なら割り当ててください |
| `Ctrl`を押しながらホイール | `{{ui:settings_keybindings_timeline_pan_modifier}}` | パン |
| `Shift`を押しながらホイール | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | ズーム |

`Z X C V B N`はタイムラインのツールバーの左から右の順、`Q W E R T`はタブの並びの順です。ツールが少ないタイムラインでは右側から欠けます：ローカルタイムラインには`Z X C V`しかありません。開いているタイムラインに対応するツールがない文字は、何もしません

### ギズモ

| キー | 設定での名前 | 動作 |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | 選択 |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | 位置 |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | 回転 |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | スケール |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | サイズ |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | アンカー |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | ピボット |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | 非表示：選択は残りますが、ハンドルも枠も描画されません |

### ウィンドウ

| キー | 設定での名前 | 動作 |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | フルスクリーンのオンとオフを切り替え。どの画面でも動作しますが、デスクトップのみです |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | 設定を開いている間に、設定を今すぐディスクに書き込みます。エディターでは、`Ctrl+S`は代わりにレベルを保存します |

### ナビゲーション

| キー | 設定での名前 | 動作 |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | 最後にクリックした領域で上へ移動 |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | 最後にクリックした領域で下へ移動 |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | 最後にクリックした領域で左へ移動 |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | 最後にクリックした領域で右へ移動 |

ギズモの数字、タイムラインの文字、`Space`のような単独のキーは、テキストフィールドに入力している間は何もしません。フレームのフィールドに`2`と入力しても、ギズモは切り替わりません

## タイムライン上の矢印キー

矢印キーは、画面上でその方向にある最も近い項目を選びます。同じキーを押せば、どのズームでも同じ項目が見つかります

- 複数選択の状態からは、押した方向に最も遠い項目から移動を始めます。選択したブロックの中へ戻ることはありません
- 矢印キーでの移動は、常に選択を置き換えます。選択に追加することはありません
- タイムラインは、新しい項目を表示するのに必要な分だけスクロールします。再生ヘッドの数値表示をクリックすれば、これまでどおり表示が中央に合わせられます
- プレビュープレイヤーがオンの間は、矢印キーはタイムラインではなくプレイヤーを操作します。ヒエラルキーと`{{ui:settings_level-settings_raw}}`タブは、一度クリックすると矢印キーをそちらで使います

## レベルを見る

**プレビュー**。`` ` ``を押し続けると、エディターのインターフェースが隠れ、レベルだけを見られます。切り替えではなく押している間だけの機能で、キーを離せばすべて元に戻ります。レベル、レターボックスの帯、プレイヤー、カメラの範囲は表示されたままです。これ用のボタンや設定はありません。キーは`{{ui:settings_keybindings_editor_preview}}`として割り当て直せます

**ビューポートのグリッド**は、ツールバーのボタンまたは`{{ui:cmd_editor_viewport-grid}}`コマンドで切り替えます。最初はオフです。これは`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`で変更でき、オンにしたかどうかはセッションをまたいで記憶されません

**ギズモの磁石**は、ギズモでドラッグしているものをグリッドにスナップさせます。デフォルトでオンで、ギズモのモードには依存しません。ツールバーのボタンと`{{ui:cmd_editor_gizmo-magnet}}`コマンドで切り替えます

**一時停止は、見るときの通常の状態です**。グリッド、コライダー、ボットのオーバーレイ、ギズモのハンドル、選択枠は、再生が一時停止している間も描画され続けます。ギズモのハンドルをつかむと、再生は一時停止します

## キーの割り当て直し

どのキーも割り当て直せます：`{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

保存されるのは変更したキーだけです。残りはデフォルトから取られます。そのため、触っていないキーには、改善されたデフォルトがそのまま反映されます。`{{ui:settings_keybindings_reset}}`は変更を削除するだけで、すべてのキーがデフォルトに戻ります

> [!tip] ヒント
> キーの表示は、インターフェースに直接書き込まれていません。割り当て直すと、コマンドパレットとすべてのコンテキストメニューに、すぐに新しいキーが表示されます

## 押すキーと押し続けるキー

押すキーは、修飾キーが完全に一致したときだけ動作します。`Ctrl+Shift+P`が`Ctrl+P`としても動作することはなく、単独の`T`は`Ctrl`を押している間は動作しません

押し続けるキーは、その修飾キーが押されているキーの中に含まれていれば動作します。すでに進行中の操作を細かく調整するためのものです

> [!info] 補足
> そのため、押し続けるキー2つが、意図的に同じボタンを共有できます。複数選択とタイムラインのパンはどちらも`Ctrl`ですが、互いに邪魔しません

次へ：[[1_order-of-work|作業の順番]]、[[2_reuse|再利用：プレハブ、コピー、ジェネレーター]]
