---
title: エディター設定
date: 2026-10-11
tags: [level_author]
---

# エディター設定

自動保存、グリッド、選択、ギズモ、新しいレベルのプリセットはここで設定します。自動保存はデフォルトでオンで、編集から{{v:editor.autosave-delay}}秒後に実行されます

## レベルエディター

自動保存、カメラ、選択、ファイル形式はここで設定します

| 設定 | 働き | デフォルト |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | 自動保存をオンにします | オン |
| `{{ui:settings_game-editor_autosave-rate}}` | 保存されていない編集から自動保存までの秒数 | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | 保持するコピーの数。上限に達すると、いちばん古いものが削除されます | {{v:editor.autosave-copies}} |

タイマーは、保存されていない編集がある間だけ動きます

1回の自動保存は2つのことをします：
1. レベルのコピーを`<game folder>/backups/<level id>/`に書き込みます
2. `Ctrl+S`と同じように、レベルそのものを保存します

コピーにはレベルファイルだけが入っています。復元する方法は2つあります：
- レベル設定で：`{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- 手動で：レベルフォルダーに`level.json`（または`level.blob`）という名前でコピーします

詳細：[[4_not-losing-work#自動保存]]

`{{ui:settings_game-editor_camera-min-size}}`と`{{ui:settings_game-editor_camera-max-size}}`は、エディターのビューポートをどこまでズームイン、ズームアウトできるかを制限します

`{{ui:settings_game-editor-multi-select-requires_hold}}`と`{{ui:settings_game-editor-pick-invisible_aabb}}`は、ビューポートでのクリックの意味を変えます。選択が急にいつもと違う動きをするようになったら、この2つを確認してください

`{{ui:settings_game-editor-level-serialize_mode}}`と`{{ui:settings_game-editor-resources-serialize_mode}}`は、ディスクに書き込むときのデフォルトの形式を決めます

`{{ui:settings_game-editor_publish-language}}`は、ワークショップアイテムのタイトルと説明を最初にどの言語で公開するかを選びます：`{{ui:enum_publish-language_english}}`（デフォルト）か、デバイスの言語である`{{ui:enum_publish-language_system}}`です

詳細：[[3_speed-and-shortcuts]]

## グリッド

ビューポートのグリッドはレベルの後ろに描画され、オブジェクトを置くのに役立ちます

| 設定 | 働き | デフォルト |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | エディターを開いたときにグリッドがオンかどうか。これは開始時の状態にすぎません | オフ |
| `{{ui:settings_game-editor-grid_size}}` | 1マスの辺の長さ（ワールド単位） | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | 線の見えやすさ。0から1まで | 0.25 |

ツールバーのグリッドボタンでオンとオフを切り替えます。その状態はセッションをまたいで保存されません

グリッドの見た目：
- 端はありません。ズームに合わせてマスの大きさが10倍刻みで変わり、細かいグリッドは徐々に現れます
- あるグリッドの段階に線が多くなりすぎる場合、その段階は間引かれるのではなくオフになります
- 線の色は常に、現在のフレームでのカメラ背景の反転色です。だから背景が変わってもグリッドは見えたままです。設定するのは不透明度だけです

スナップがオンのとき、位置のドラッグはマスの半分に吸い付きます：交点とマスの中心です。使われるのは見えているグリッドです。グリッドがオフのときは、位置は固定のステップに吸い付きます

## 選択

| 設定 | 働き | デフォルト |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | オン：複数選択モードでは、`Ctrl`を押している間だけクリックで追加され、ふつうのクリックは選択を置き換えます。オフ：モードがオンの間は、どのクリックも追加します | オン |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | 選択中のすべてのオブジェクトのヒットボックスを半透明の塗りで描画します | オフ |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | クリックが、オブジェクトの描画内容ではなく長方形全体でオブジェクトを選びます | オフ |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | メニューが開くまでの長押しの時間（秒） | 0.5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | 長押し中にカーソルがどこまで動いたらドラッグになるか | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | 選択中のオブジェクトのヒットボックスをどれだけ濃く描画するか | 0.5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | すべてのヒットボックスの表示で同じことを決めます。そこでは何百個も重なるので、より薄くなっています | 0.25 |

複数選択モードで`Ctrl`を離しても、何も解除されず、モードも終わりません。選択を置き換えるのは次のふつうのクリックだけです。モードの詳細：[[4_hierarchy-and-clipboard]]

ツールバーのコライダーボタンは、プレイヤーの円も含めて、フレーム内のすべてのヒットボックスを表示します。その状態はセッションをまたいで保存されません。画面上のヒットボックスが多すぎる場合、一部だけを描画するのではなく、メッセージを出して表示が自動的にオフになります

コライダーのないオブジェクトは、どちらの表示でもヒットボックスを描画しません。非アクティブなオブジェクトも同じです

両方の表示の塗りの色は`設定 > グラフィック > コライダーのみモード > 塗りの色`で、ゲームの「コライダーのみ」モード（[[4_settings]]）と共通です。上の2つの不透明度は、引き続きエディター独自の設定です

## ギズモ

| 設定 | 働き | デフォルト |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | ビューポートのドラッグ用ハンドルの大きさ。0.1から10まで。マウス用の大きさのハンドルは、指では押しにくいです | 1 |

ハンドルはどのズームでも画面上で同じ大きさを保ちます

## AIエージェント

`{{ui:settings_game-editor_mcp_title}}`を使うと、MCPに対応したAIクライアントが開いているレベルを編集できます。Windows、Linux、Macのみです：スマートフォンとタブレットにはこのセクションは表示されません

| 設定 | 働き | デフォルト |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | クライアントの接続を許可します。接続できるのはこのコンピューターだけで、一度に1つのクライアントだけです | オフ |
| `{{ui:settings_game-editor_mcp-port}}` | エディターが待ち受けるポート。`0`なら起動のたびに空いているポートを選び、それ以外は{{v:mcp.port-min}}から{{v:mcp.port-max}}まで。範囲外の数値は元に戻ります | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | AIがフレームを見た後、再生ヘッドがどこへ行くか。オフ：離れる前の位置に戻ります。オン：そのフレームに一時停止したまま留まります | オン |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | AIが編集するたびに、作成または変更したものを選択して位置を表示します。ドラッグ中、入力中、プレイ中は決して行いません | オン |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | AIの2つの操作の間にエディターが待つ秒数。0から{{v:mcp.operation-delay-max}}まで。`0`なら各操作をすぐに適用します。再生、一時停止、再生ヘッドの移動は決して遅延されず、AIが読み取るだけの操作も同じです | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}`は、MCPクライアントが受け取る設定を、サーバーへのパスとゲームの接続ファイルへのパスを記入した状態でコピーします

設定の下の行は、エディターの状態を示します：オフ、ポートで待ち受け中、接続済み、またはエディターのAIバッジから停止済み

これらの設定はこのデバイスにだけ保存されます

詳細：[[7_ai-assistant]]

## レベルの作成

`{{ui:settings_editor-settings_level-presets}}`は、新しいレベルが何から始まるかを決めます：空か、小さな骨組みがあるかです。プリセットがなければ、その骨組みを毎回手で作ることになります

> [!caution] 注意
> `{{ui:settings_editor-settings_parameters}}`では、後から変えにくいものを設定します：フレーム単位の長さとフレームレートです

> [!tip] ヒント
> `{{ui:settings_editor-settings_quot-level-quot-file-format}}`と`{{ui:settings_editor-settings_quot-metadata-quot-file-format}}`のリストは、レベルとそのメタデータをディスクに書き込む形式を選びます。どちらもあとからレベルの`{{ui:settings_level-settings_dangerous-zone}}`で変更できます

詳細：[[2_first-level]]

## ライブラリ

`{{ui:settings_editor-settings_library}}`は`{{ui:settings_editor-settings_community}}`の後にある最後のタブです。レベルをまたいで再利用するリソースが入っています：このデバイスの共有ライブラリ、自分のコレクション、Steam版ではさらにSteamワークショップで購読したコレクションです

左の列で種類を選びます：`{{ui:settings_level-settings_collections}}`、次にプレハブ、テーマ、シェイプ、エフェクト、次にテクスチャ、フォント、オーディオ。ここではコレクションの作成と編集、コレクション間での項目のコピー、インポートとエクスポートができ、Steam版では自分のコレクションを公開できます

詳細：[[16_library-and-collections]]

## 他人の作品を使う

レベル内のすべての外部リソース（音楽、画像、フォント、テキスト）は、次の2つのどちらかに当てはまる必要があります：
- 少なくとも`CC BY-NC`と同じくらい自由なライセンス
- 公開の非営利配布について、権利者自身が出した許可

> [!caution] 注意
> 個人的な「いいよ、問題ない」では足りません。`CC BY-NC`のレベルは公開で配布されます。許可は、個人的な利用だけでなく、まさにその配布を対象にしている必要があります

デバイスに留まっているレベルはチェックされません。ルールが適用されるのは1つの時点だけです：レベルがサービスに渡されるときです

ルールの全文、受け入れられるライセンスの一覧、依頼文のテンプレート、リソースの探し方：
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
