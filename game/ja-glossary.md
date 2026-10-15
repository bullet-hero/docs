# Japanese term base

The terms `ja.yaml` (Japanese) is translated with. Every value in `ja.yaml` follows this table: a thing is named the
same way on every screen, in every hint, in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its Japanese value must contain the `ja` term.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `ja` for a different concept.
- A row whose `ja` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.
- Loanwords follow the Japanese Unity editor: katakana, a trailing `ー` kept (`インスペクター`, `レイヤー`).

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `ja.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for Japanese: `Assets/Addressables/TEXT-STYLE.md`, section 9, in
the game's repository.

| en | ja | kind | note |
|---|---|---|---|
| Level | レベル | strict | 1回のプレイの中身すべて：オブジェクト、オーディオ、イベント、独自のリソース。音量の「level」は別の意味 |
| Object | オブジェクト | strict | タイムライン上で作者が作るもの。存続期間、トランスフォーム、親を持つ |
| Rect | 空オブジェクト | loose | 何も描画しないオブジェクト：トランスフォーム、存続期間、子だけを持つ。ru と同じく二語に分ける：型としては「空オブジェクト」、図形（長方形）としては「長方形」 |
| Shape | シェイプ | loose | オブジェクトが描画する実際のジオメトリ。画像ではない。ゲームが約 500 種類を生成する |
| Collider | コライダー | strict | オブジェクトが当たる範囲。描画と一致しなくてもよい。Unity 日本語版の用語 |
| Prefab | プレハブ | strict | 何度でも配置できる再利用可能なオブジェクトのテンプレート。Unity 日本語版の用語 |
| Prefab Mode | プレハブモード | strict | 周囲のレベルではなくテンプレート自体の中身を編集するモード |
| Effect | エフェクト | loose | ジェネレーター型のオブジェクト：いくつかのパラメーターから毎フレーム自分のオブジェクトを生成する。Bloom や Vignette などは「ポストプロセス効果」で、「エフェクト」ではない |
| Inframe Object | フレーム内オブジェクト | loose | エフェクトが生成するオブジェクト。エンジンが管理し、選択も編集もできない |
| Theme | テーマ | strict | レベルがインデックスで参照するパレット。色の変更は1か所で済む |
| Frame | フレーム | strict | レベルの時間の単位。フレームはマス目、時間はマス目の境界 |
| Keyframe | キーフレーム | strict | あるフレームで作者が決めた値。2つのキーフレームの間は補間される |
| Key | キーフレーム | loose | 「キーフレーム」の略なら「キーフレーム」、キーボードのキーは「キー」、ローカライズのキーは「キー」 |
| Track | トラック | strict | アニメーションできるプロパティ1つ分のキーフレームの行：位置、回転、音量。Audio Track は「オーディオトラック」 |
| Timeline | タイムライン | strict | レベルを編集するフレームの軸。内容の種類ごとにタブが1つ |
| Span | スパン | loose | オブジェクトが存在する期間：終了フレームではなく開始フレームと長さ。動詞の span（「またがる」）は「スパン」と訳さない |
| Playhead | 再生ヘッド | strict | 今表示しているフレーム |
| Ease | イージング | strict | 前のキーフレームからこのキーフレームへの値の動き方 |
| Marker | マーカー | strict | レベルのルーラー上の名前付きの点。位置をもう一度見つけるためのもの |
| Checkpoint | チェックポイント | strict | 死亡したプレイヤーが戻される位置 |
| Anchor | アンカー | strict | 親の辺に追従する辺。親が縮むと子も一緒に動く |
| Layer | レイヤー | strict | 描画順。親からの相対値：子のレイヤーに親のレイヤーが足される |
| Pivot | ピボット | loose |  |
| Gizmo | ギズモ | strict | ビューポートで選択中のオブジェクトの上に描かれるドラッグ用ハンドル。Unity 日本語版の用語 |
| Snapping | スナップ | strict | ドラッグを何かに吸い付ける機能：磁石なら他の内容、ビートのトグルなら音楽 |
| Snap | スナップ | strict | Snapping と同じ |
| Beat | ビート | strict | 音楽自体のグリッド。レベルが設定し、再生中は読まれない |
| Beat Segment | ビートセグメント | strict | テンポが一定の区間。独自のテンポ、位相、小節の長さを持つ |
| BPM | BPM | strict | 1分あたりの拍数。ラテン文字のまま、日本の音ゲーコミュニティでも共通 |
| Tap | タップ | loose |  |
| Generator | ジェネレーター | strict | 制作の自動化：いくつかのパラメーターからレベルの内容を生成する |
| Modifier | モディファイアー | strict | 追加ではなく既存の内容を編集または削除するジェネレーター。Blender 日本語版の用語 |
| Seed | シード | strict | レベル内のすべてのランダム値の元になる数。同じシードなら同じ結果が再現される |
| Raw Data | 生データ | strict | 保存モデル全体を編集可能なツリーとして表示したもの。意図的に検証しない |
| Recommendation | 推奨 | strict | 5つのラベルの1つ。`<b>推奨：</b>` と書く |
| Tip | ヒント | strict | 5つのラベルの1つ。`<b>ヒント：</b>` と書く |
| Worth knowing | 補足 | strict | 5つのラベルの1つ。`<b>補足：</b>` と書く |
| Warning | 警告 | strict | 5つのラベルの1つ。`<b>警告：</b>` と書く |
| Caution | 注意 | strict | 5つのラベルの1つ。`<b>注意：</b>` と書く |
| More | 詳細 | loose | ヒント末尾のリンク行 `More:` は `詳細：` |
| Bullet Hero | Bullet Hero | strict | 製品名。翻訳しない |
| Steam | Steam | loose |  |
| JSON | JSON | strict | フォーマット名。翻訳しない |
| MSAA | MSAA | strict | 技術用語の略語。翻訳しない |
| FXAA | FXAA | strict | 技術用語の略語。翻訳しない |
| HDR | HDR | loose |  |
| VFX | VFX | loose |  |
| URL | URL | loose |  |
| Ctrl | Ctrl | loose |  |
| Shift | Shift | loose |  |
| Enter | Enter | loose |  |
| Hierarchy | ヒエラルキー | strict | 親子関係でオブジェクトを一覧するエディターのパネル。Unity 日本語版の「ヒエラルキー」ウィンドウ |
| Inspector | インスペクター | strict | 選択中の内容のプロパティを表示するエディターのパネル。Unity 日本語版の用語 |
| Viewport | ビューポート | strict | エディター内でレベルの画面を表示する領域 |
| Command Palette | コマンドパレット | strict | 名前でコマンドを検索して実行するウィンドウ。VS Code 日本語版の用語 |
| Command | コマンド | loose |  |
| Selection | 選択 | loose | 選択中の項目の集まりは「選択中の項目」とも書ける |
| Select | 選択 | loose |  |
| Marquee | 矩形選択 | strict | 矩形をドラッグして選択すること |
| Apply | 適用 | loose |  |
| Reset | リセット | loose |  |
| Cancel | キャンセル | loose |  |
| Confirm | 確認 | loose |  |
| OK | OK | loose |  |
| Save | 保存 | loose |  |
| Load | 読み込み | loose |  |
| Open | 開く | loose |  |
| Close | 閉じる | loose |  |
| Exit | 終了 | loose |  |
| Create | 作成 | loose |  |
| Add | 追加 | loose |  |
| Remove | 除去 | loose | Delete（削除）と区別する：Remove は一覧から外す、Delete は消す |
| Delete | 削除 | loose |  |
| Duplicate | 複製 | loose |  |
| Copy | コピー | loose |  |
| Paste | 貼り付け | loose |  |
| Cut | 切り取り | loose |  |
| Undo | 元に戻す | loose |  |
| Redo | やり直し | loose |  |
| History | 履歴 | loose |  |
| Edit | 編集 | loose |  |
| Rename | 名前を変更 | loose |  |
| Move | 移動 | loose |  |
| Import | インポート | loose |  |
| Export | エクスポート | loose |  |
| Archive | アーカイブ | loose |  |
| Folder | フォルダー | loose |  |
| File | ファイル | loose |  |
| Search | 検索 | loose |  |
| Filter | フィルター | loose |  |
| Refresh | 更新 | loose |  |
| Toggle | 切り替え | loose |  |
| Show | 表示 | loose |  |
| Hide | 非表示 | loose |  |
| Hidden | 非表示 | loose |  |
| Visible | 表示中 | loose |  |
| Enabled | 有効 | loose |  |
| Disabled | 無効 | loose |  |
| On | オン | loose |  |
| Off | オフ | loose |  |
| None | なし | loose |  |
| Auto | 自動 | loose |  |
| Custom | カスタム | loose |  |
| Default | デフォルト | loose |  |
| All | すべて | loose |  |
| Nothing | なし | loose |  |
| Current | 現在 | loose |  |
| Active | アクティブ | loose |  |
| Global | グローバル | loose |  |
| Local | ローカル | loose |  |
| Parent | 親 | loose |  |
| Child | 子 | loose |  |
| Root | ルート | loose |  |
| Fold | 折りたたむ | loose |  |
| Unfold | 展開 | loose |  |
| Flatten | フラット化 | loose |  |
| Transform | トランスフォーム | loose |  |
| Position | 位置 | loose |  |
| Rotation | 回転 | loose |  |
| Scale | スケール | loose |  |
| Size | サイズ | loose |  |
| Offset | オフセット | loose |  |
| Angle | 角度 | loose |  |
| Radius | 半径 | loose |  |
| Width | 幅 | loose |  |
| Height | 高さ | loose |  |
| Min | 最小 | loose |  |
| Max | 最大 | loose |  |
| Step | ステップ | loose |  |
| Random | ランダム | loose |  |
| Rnd | ランダム | loose |  |
| From | 開始値 | loose |  |
| To | 終了値 | loose |  |
| Value | 値 | loose |  |
| Type | タイプ | loose |  |
| Name | 名前 | loose |  |
| Mode | モード | loose |  |
| Count | 数 | loose |  |
| Speed | 速度 | loose |  |
| Velocity | 速度 | loose |  |
| Gravity | 重力 | loose |  |
| Particle | パーティクル | loose |  |
| Orbital | 軌道 | loose |  |
| Lifetime | 寿命 | loose |  |
| Color | 色 | loose |  |
| Alpha | アルファ | loose |  |
| Opacity | 不透明度 | loose |  |
| Opaque | 不透明 | loose |  |
| Transparent | 透明 | loose |  |
| Gradient | グラデーション | loose |  |
| Texture | テクスチャ | loose |  |
| Font | フォント | loose |  |
| Text | テキスト | loose |  |
| Localized Text | ローカライズテキスト | loose |  |
| Language | 言語 | loose |  |
| Audio | オーディオ | loose |  |
| Audio Track | オーディオトラック | loose |  |
| Volume | 音量 | loose |  |
| Music | 音楽 | loose |  |
| Sound | サウンド | loose |  |
| Resource | リソース | loose |  |
| Resources | リソース | loose |  |
| Metadata | メタデータ | loose |  |
| Meta | メタ | loose |  |
| License | ライセンス | loose |  |
| Author | 作者 | loose |  |
| Artist | アーティスト | loose |  |
| Settings | 設定 | loose |  |
| Editor | エディター | loose |  |
| Game | ゲーム | loose |  |
| Player | プレイヤー | loose |  |
| Avatar | アバター | loose |  |
| Dash | ダッシュ | loose |  |
| Hitbox | 当たり判定 | loose |  |
| Damage | ダメージ | loose |  |
| Health | 体力 | loose |  |
| Death | 死亡 | loose |  |
| Camera | カメラ | loose |  |
| Zoom | ズーム | loose |  |
| Pan | パン | loose |  |
| Shake | 揺れ | loose |  |
| Grid | グリッド | loose |  |
| Ruler | ルーラー | loose |  |
| Loop | ループ | loose |  |
| Play | 再生 | loose | エディターでの再生は「再生」、レベルを遊ぶことは「プレイ」 |
| Pause | 一時停止 | loose |  |
| Stop | 停止 | loose |  |
| Preview | プレビュー | loose |  |
| Render | レンダリング | loose |  |
| Post-processing | ポストプロセス | loose |  |
| Post | ポスト | loose |  |
| Bloom | ブルーム | loose |  |
| Vignette | ビネット | loose |  |
| Chromatic Aberration | 色収差 | loose |  |
| Lens Distortion | レンズ歪み | loose |  |
| Film Grain | フィルムグレイン | loose |  |
| Grain | グレイン | loose |  |
| Motion Blur | モーションブラー | loose |  |
| Blur | ブラー | loose |  |
| Color Curves | カラーカーブ | loose |  |
| Curve | カーブ | loose |  |
| Lift Gamma Gain | リフト/ガンマ/ゲイン | loose |  |
| Shadows Midtones Highlights | シャドウ/中間調/ハイライト | loose |  |
| White Balance | ホワイトバランス | loose |  |
| Analog Glitch | アナロググリッチ | loose |  |
| Digital Glitch | デジタルグリッチ | loose |  |
| Glitch | グリッチ | loose |  |
| Gamma | ガンマ | loose |  |
| Background | 背景 | loose |  |
| Framerate | フレームレート | loose |  |
| Fixed Framerate | シミュレーション更新頻度 | loose |  |
| Collision | 衝突 | loose |  |
| Screen Limit | 画面制限 | loose |  |
| Cursor | カーソル | loose |  |
| Control | 操作 | loose |  |
| Controls | 操作 | loose |  |
| Keybinding | キー割り当て | loose |  |
| Shortcut | ショートカット | loose |  |
| Button | ボタン | loose |  |
| Interface | インターフェース | loose |  |
| Screen | 画面 | loose |  |
| Window | ウィンドウ | loose |  |
| Panel | パネル | loose |  |
| Tab | タブ | loose |  |
| Menu | メニュー | loose |  |
| Tool | ツール | loose |  |
| Library | ライブラリ | loose |  |
| Bot | ボット | loose |  |
| Tutorial | チュートリアル | loose |  |
| Sandbox | サンドボックス | loose |  |
| Hint | ヒント | loose |  |
| Glossary | 用語集 | loose |  |
| Validation | 検証 | loose |  |
| Rules | ルール | loose |  |
| Format | フォーマット | loose |  |
| Version | バージョン | loose |  |
| Desktop | デスクトップ | loose |  |
| Mobile | モバイル | loose |  |
| Alignment | 揃え | loose | Placement（配置）と区別する |
| Align | 揃える | loose |  |
| Center | 中央 | loose |  |
| Left | 左 | loose |  |
| Right | 右 | loose |  |
| Top | 上 | loose |  |
| Bottom | 下 | loose |  |
| Horizontal | 水平 | loose |  |
| Vertical | 垂直 | loose |  |
| Linear | リニア | loose |  |
| Appearing | 出現 | loose |  |
| Scissors | ハサミ | loose |  |
| Edges | エッジ | loose |  |
| Point | ポイント | loose |  |
| Continue | 続ける | loose |  |
| Next | 次へ | loose |  |
| Back | 戻る | loose |  |
| Loading | 読み込み中 | loose |  |
| Progress | 進行状況 | loose |  |
| Statistics | 統計 | loose |  |
| Preset | プリセット | loose |  |
| Clipboard | クリップボード | loose |  |
| Console | コンソール | loose |  |
| Ping | 位置を表示 | loose |  |
| Override | オーバーライド | loose |  |
| Placement | 配置 | loose |  |
| Template | テンプレート | loose |  |
| Clip | クリップ | loose |  |
| Slip | スリップ | loose |  |
| Slot | スロット | loose |  |
| Beat Grid | ビートグリッド | loose |  |
| Bar | 小節 | loose |  |
| Tempo | テンポ | loose |  |
| Tap Tempo | タップテンポ | loose |  |
| Stereo Pan | ステレオパン | loose |  |
| Font Size | フォントサイズ | loose |  |
| Word Wrap | 折り返し | loose |  |
| Backup | バックアップ | loose |  |
| Branch | ブランチ | loose |  |
| Fit | フィット | loose |  |
| Finding | 問題 | loose |  |
| Fix | 修正 | loose |  |
| Group | グループ | loose |  |
| Id | ID | loose |  |
| Mipmap | ミップマップ | loose |  |
| Sampling | サンプリング | loose |  |
| Tiling | タイリング | loose |  |
| Wrapping | ラップ | loose |  |
| Pixel art | ドット絵 | loose |  |
| Drawing | 描画 | loose |  |
| Emission Shape | 放出形状 | loose |  |
| Over Lifetime | 寿命内の変化 | loose |  |
| Forces | 力 | loose |  |
| Scatter | 散布 | loose |  |
| Spread | 拡散 | loose |  |
| Tangent | 接線 | loose |  |
| Clamp | クランプ | loose |  |
| Ping Pong | ピンポン | loose |  |
| Temperature | 色温度 | loose |  |
| Tint | 色合い | loose |  |
| Modifier Key | 修飾キー | loose |  |
| Dead Zone | デッドゾーン | loose |  |
| Sensitivity | 感度 | loose |  |
| Stick | スティック | loose |  |
| Shoulder | ショルダーボタン | loose |  |
| Gamepad | ゲームパッド | loose |  |
| Touchscreen | タッチスクリーン | loose |  |
| Motion Sensor | モーションセンサー | loose |  |
| Handedness | 利き手 | loose |  |
| Double Tap | ダブルタップ | loose |  |
| Workshop | ワークショップ | loose | Steam 日本語版の用語 |
| Story | ストーリー | loose |  |
| Wave | ウェーブ | loose |  |
| Immortal | 無敵 | loose |  |
| Dodge | 回避 | loose |  |
| Zen | 禅 | loose |  |
| Clears | クリア回数 | loose |  |
| Hits | 被弾数 | loose |  |
| Profile | プロファイル | loose |  |
| Frame Hierarchy | フレームヒエラルキー | loose | strict の Hierarchy（ヒエラルキー）に合わせる |
| Stop Frame | 停止フレーム | loose |  |
| Runtime Seed | 実行時シード | loose |  |
| Level Logo | レベルカバー | loose | レベル一覧に表示される画像 |
| Post-processing effect | ポストプロセス効果 | loose |  |
| Audio effect | オーディオエフェクト | loose |  |
| Chorus | コーラス | loose |  |
| Compressor | コンプレッサー | loose |  |
| Distortion | ディストーション | loose |  |
| Echo | エコー | loose |  |
| Flange | フランジャー | loose |  |
| Highpass | ハイパス | loose |  |
| Lowpass | ローパス | loose |  |
| Normalize | ノーマライズ | loose |  |
| Param EQ | パラメトリックEQ | loose |  |
| Pitch Shifter | ピッチシフター | loose |  |
| Reverb | リバーブ | loose |  |
| Emitter | エミッター | loose |  |
| Variant | バリアント | loose |  |
| Fader | フェーダー | loose |  |
| Signal level | 信号レベル | loose | オーディオエフェクトのヒントでの「level」。LocalizationGlossaryTests で除外済み |
| Swatch | スウォッチ | loose |  |
| Device library | このデバイスの共有ライブラリ | loose |  |
| Collection | コレクション | strict | 再利用できるリソースのフォルダー：プレハブ、テーマ、シェイプ、エフェクト、テクスチャ、フォント、オーディオ。Steam の Collections（ワークショップアイテムの選集）とは無関係。データ構造の collection（検証ルール名）は「コレクション」と訳さなくてよく、それらのキーは LocalizationGlossaryTests で除外済み |
| Anti-aliasing | アンチエイリアス | loose |  |
| Overlay | オーバーレイ | loose |  |
| Scrub | スクラブ | loose |  |
| Gradient stop | カラーストップ | loose |  |
| Link to a docs page | ページタイトル | loose | ドキュメントへのリンクは、リンク先ページの日本語タイトルで書く |
| Difficulty | 難易度 | loose | 難易度の段階。弾幕を天気に見立て、数滴から崩壊まで。直訳ではなくイメージを保つ |
| Auto (difficulty) | オート | loose |  |
| Drizzle (difficulty) | 霧雨 | loose |  |
| Rain (difficulty) | 雨 | loose |  |
| Downpour (difficulty) | 豪雨 | loose |  |
| Hail (difficulty) | 雹 | loose |  |
| Barrage (difficulty) | スコール | loose |  |
| Onslaught (difficulty) | 猛襲 | loose |  |
| Deluge (difficulty) | 大洪水 | loose |  |
| Inferno (difficulty) | 煉獄 | loose |  |
| Singularity (difficulty) | 特異点 | loose |  |
