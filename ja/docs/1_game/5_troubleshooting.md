---
title: トラブルシューティング
date: 2026-10-03
tags: [player]
---

# トラブルシューティング

手動でコピーしたレベルは再スキャンで一覧に出ます。新しいバージョンのレベルはゲームの更新、.7zアーカイブはzipへの再圧縮が必要です。忘れたパスワードは復元できません。Discordへの表示はSteam版でDiscordアプリ起動中のみです

問題が見つかりませんか？報告先はこちら：[[11_help]]

## レベルが一覧にない

- **手動でコピーした**：レベルフォルダーは`levels`の直下に置く必要があります、[[1_installation]]。コピーしたら`{{ui:root_level-browser_refresh}}`を押してください
- **ワークショップのアイテム**：Steam版にはサブスクライブしたアイテムだけが表示されます。`{{ui:settings_common_title}}` → `{{ui:settings_general_title}}` → `{{ui:settings_general_show-all-found-content}}`で、ディスク上で見つかったフォルダーが追加されます。それらには`{{ui:root_level-entry_not-listed}}`の印が付きます
- **何も表示されない**：レベルフォルダーにアクセスできない可能性があります。この状態では`{{ui:settings_other_title}}`のストレージ消去は実行されず、`レベルのスキャンで何も見つからなかったため、消去を中止しました`と表示されます

## レベルが読み込めない

読み込み画面には段階が表示されます：`{{ui:root_loading_reading}}`、`{{ui:root_loading_validating}}`、`{{ui:root_loading_resources}}`、`{{ui:root_loading_building}}`

- **Webアドレスにあるファイル**：レベルはファイルを自分のフォルダーに置く代わりに、リンク先から取得することもできます。`{{ui:settings_general_title}}` → `{{ui:settings_general_resource-web-timeout}}`は、ゲームがそのようなファイルを何秒待つかを決めます
- **壊れたレベル**：`Json`形式のレベルはテキストなので、目で読めます。壊れた`Blob`は丸ごと拒否されます。詳細：[[4_level-folder-and-backups]]
- **エラーウィンドウ**：`{{ui:root_error_copy}}`、`{{ui:root_error_save}}`、`{{ui:root_error_open-reports-folder}}`があります。レポートは`reports`フォルダーに保存されます。[bullet-hero/releases](https://github.com/bullet-hero/releases/issues)へのバグ報告に添付してください、[[11_help]]
- **`このレベルが必要とする1フレームあたりのオブジェクト数が、このデバイスの上限を超えています`**：これは読み込みエラーではありません。レベルはプレイできますが、一部が描画されません。詳細：[[1_level-budget]]

## 「更新が必要」

古いバージョンのゲームは、新しいバージョンのファイルを開きません。ゲームを更新してください

| メッセージ | 対処 |
|---|---|
| `このレベルはより新しいバージョンのゲームで作られており…` | ゲームを更新する |
| `このアーカイブには、より新しいバージョンのゲームで作られたレベルが入っています…` | ゲームを更新する |
| `クリップボードには、より新しいバージョンのゲームでコピーされたエディターの内容が入っています…` | ゲームを更新する |
| `設定または統計が、より新しいバージョンのゲームで保存されています…` | `{{ui:root_update-required_download}}`、`{{ui:root_update-required_keep}}`、`{{ui:root_update-required_overwrite}}`のいずれか |

`{{ui:root_level-entry_newer-version}}`または`{{ui:root_level-entry_newer-file}}`の印が付いたカードも同じ拒否です。レベルを開く前から表示されます

### 新しいバージョンの設定や統計

この場合、ゲームはデフォルト値で動作します。ゲームを閉じるまで独自のデータは何も保存せず、新しいファイルはそのまま残ります。これは匿名モードです、[[4_settings]]。`--suppress-game-saves`を使っている場合、`{{ui:root_update-required_overwrite}}`ボタンはありません

新しいバージョンのレベル統計は表示されません。保存がオフになっていなければ、そのレベルをプレイすると上書きされます

### ゲームが拒否する理由

ファイル形式が変わるたびに、新しい世代番号が付きます。ビルドは誤って読み込まないように、より新しい世代のファイルを読み込みません

## 保護されたレベル

開く前に、ゲームが`{{ui:level_passphrase_password}}`を尋ねます。パスワードを尋ねるのはセッションごとに1回で、メモリ上にだけ保持されます

暗号化されるのは中身だけです：オブジェクト、キーフレーム、テーマ。タイトル、カバー、メディアは読めるままなので、パスワードがなくてもカードは表示されます

保護されたレベルの削除にパスワードは不要です

> [!caution] 注意
> 忘れたパスワードは復元できません。鍵はどこにも保存されていません。ゲームにも、ファイルにも、誰の手元にもありません

## アーカイブが拒否される

| メッセージ | 原因 |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | `.7z`です。`.zip`に再圧縮してください |
| `{{ui:editor_create-level_archive-wrong-password}}` | パスワードが一致しません |
| `{{ui:editor_create-level_archive-damaged}}` | アーカイブが壊れています。もう一度送ってもらってください |
| `{{ui:editor_create-level_archive-not-archive}}` | そもそもレベルのアーカイブではありません |

名前を変えたアーカイブは問題ありません：ゲームはファイルのバイト列から形式を判別します。受け付けるアーカイブ：[[2_playing-levels]]

## Discordにプレイ中の内容が表示されない

- **Steam版ではない**：Discordにアクティビティを表示するのはSteam版だけです
- **Discordが閉じている**：同じコンピューターでDiscordのデスクトップアプリが起動している必要があります。ゲームの後にDiscordを起動した場合は、次に画面が切り替わったときにステータスが表示されます
- **アクティビティが非表示**：Discordで`ユーザー設定` -> `アクティビティのプライバシー` -> 検出されたアクティビティを共有する
- **自作レベルの名前が表示されない**：仕様です。名前が表示されるのはワークショップのレベルとゲームに同梱されたレベルだけで、エディターのレベルの名前は決して表示されません。理由：[[game-privacy-policy#Discord Rich Presence]]
