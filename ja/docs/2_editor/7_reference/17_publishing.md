---
title: 公開
date: 2026-10-11
tags: [level_author]
---

# 公開

レベルを送れるのは、レベル設定の「公開」タブからだけです：アーカイブとして、またはSteamワークショップへ送ります。レポートがレベルを自動でチェックし、エラーがあると送信できません

## 「公開」タブ

`公開`はレベル設定のタブです。レベルをどこかへ送れるのはここだけです

上部の`{{ui:editor_share_destination}}`に、選んだ送信方法が表示されます。押すと`{{ui:editor_share_pick-title}}`が開きます：このビルドがこのデバイスで提供する方法が、それぞれ1行の説明付きで並びます。デフォルトでは`{{ui:editor_share_archive}}`が選ばれています。最後の選択はゲームを閉じるまで記憶されます

その下にあるもの：
- 方法ごとの設定
- そのレポート
- 実行ボタン：`{{ui:editor_share_export}}`または`公開`

このビルドにこのデバイスで使える方法がない場合、タブには`{{ui:editor_share_none}}`と表示されます

## レポート

レポートは自動でチェックします：方法を開いたときと、その設定のどれかが変わったときです。チェック用のボタンはありません。レポートは`エラー：N、警告：N、アドバイス：N`の行で始まり、その後に問題ごとに1行が続きます

エラーがあると実行できません。警告とアドバイスへの対応は任意です

レベルを判定するルールは、方法によって決まります。`{{ui:editor_share_archive}}`は`{{ui:editor_publish_profile-local}}`のセットで、`{{ui:editor_share_steam}}`はワークショップのルールでチェックします。各セットの要件と各判定の意味：[[5_publish-readiness]]

## 送信方法

| 方法 | 使える場所 | 送れるもの |
|---|---|---|
| `{{ui:editor_share_archive}}` | 保存ダイアログがあるすべてのデバイス。iOSにはありません | レベル、コレクション、または1つのリソースをファイルとして |
| `{{ui:editor_share_steam}}` | Steam版のみ | レベル、または自分のコレクション |

このビルドやこのデバイスにない方法は、単にリストに表示されません

## アーカイブ

レベルの場合：

| 要素 | 機能 |
|---|---|
| `{{ui:editor_share_format}}` | 7つのエクスポートモードの1つ。普通のフォルダーからパスワード付きアーカイブまで |
| `{{ui:editor_share_passphrase}}` | 保護モードでのみ表示されます。パスワードが空の保護モードは実行されません |
| `{{ui:editor_share_export}}` | 指定した場所にレベルを書き出します |

各モードが書き出すものと、それを開く方法：[[13_export-and-protection#レベルのエクスポート]]

コレクションまたは1つのリソースの場合、`{{ui:editor_share_format}}`ではそのうち5つのモードを選べ、すべてアーカイブです。フォルダーのモードはありません：

| `{{ui:editor_share_format}}` | できるもの | 開く方法 |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_zip}}` | 1つのファイル | Windowsエクスプローラーでダブルクリック。インストールは不要です |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | AES-256暗号化が組み込まれたzip | 7-Zipなどのアーカイバー。パスワードを求められます |
| `{{ui:settings_level-settings_export-mode_zip-protected}}` | zip全体をOpenPGPで包んだもの | gpg |
| `{{ui:settings_level-settings_export-mode_targz}}` | 1つのファイル | 任意のアーカイバー |
| `{{ui:settings_level-settings_export-mode_targz-protected}}` | OpenPGPで包んだtar.gz | gpg |

`{{ui:editor_share_passphrase}}`は3つのパスワードモードで表示されます。パスワードが空だと何もエクスポートされません。下のコレクションのチェックが、同じ`{{ui:editor_publish_profile-local}}`のルールで適用されます

## Steamワークショップ

Steam版のみです。要素は次のとおりです：

| 要素 | 機能 |
|---|---|
| `{{ui:editor_publish_visibility}}` | アイテムを見られる人：`{{ui:editor_publish_visibility-public}}`、`{{ui:editor_publish_visibility-friends-only}}`、`{{ui:editor_publish_visibility-private}}`。デフォルトは`{{ui:editor_publish_visibility-private}}` |
| `{{ui:editor_publish_changelog}}` | 今回のアップロードの変更メモ。複数行のフィールドで、ラベルは独立した行にあります |
| `タイトルと説明の言語` | アイテムのテキストを取る言語（下記参照） |
| `{{ui:editor_share_steam-descriptors}}` | 5つのチェックボックス。Steam独自のコンテンツ記述子です（下記参照） |
| `公開` | レベルをアップロードします |

レベルは常にワークショップのルールでチェックされます。ここではルールを選べません

ワークショップのアイテムは、レベルの内容で埋められます：
- タイトルと説明は、レベルの名前と説明で、1つの言語です
- プレビューはレベルのカバーで、pngまたはjpg、1MB以下です。それ以外のカバーはスキップされ、アイテムは画像なしでアップロードされます
- タグはゲームが自動で設定します。下の「ワークショップのタグ」を参照してください

`公開`を初めて押すと、アイテムが作成されます。2回目以降は同じアイテムが更新されます。ゲームは公開済みのアイテムの中からレベル自身のIDでそれを見つけるので、レベルには何も保存されません

保護されたレベルは公開できません。詳細：[[13_export-and-protection]]

アップロードには、AIアシスタントがレベルについてのメモを保存するレベルの`ai`フォルダーが含まれます。ただし、レベルのメタデータで`{{ui:settings_level-settings_metadata-level-ai-share}}`のチェックを外した場合は含まれません。サブスクライブした全員が、レベルと一緒にそれを受け取ります。詳細：[[7_ai-assistant#aiフォルダー]]

> [!warning] 警告
> Steamワークショップの法的同意書に同意していない場合、アイテムはアップロードされますが、非表示のままです。アイテムのページで同意してください。ゲームはそのページをSteamオーバーレイで開きます

### タイトルの言語

Steamはアイテムごとにタイトルと説明を1つずつ表示します。ゲームは、次の順で最初に見つかった言語を使います：
1. `{{ui:settings_game-editor_title}}`設定の`{{ui:settings_game-editor_publish-language}}`：`{{ui:enum_publish-language_english}}`（デフォルト）または`{{ui:enum_publish-language_system}}`（デバイスの言語）。詳細：[[14_editor-settings]]
2. 自分の言語、つまりゲームのインターフェースの言語
3. 英語
4. テキストが最初に書かれた言語

説明は、タイトルと一致するよう、まずタイトルの言語で探されます。ローカライズされていない名前（プレーンテキスト）は書かれたとおりにアップロードされ、その行には`{{ui:editor_share_steam-language-as-written}}`と表示されます

### コンテンツ記述子

`{{ui:editor_share_steam-descriptors}}`には、Steam独自のコンテンツ記述子である5つのチェックボックスがあります：
- `{{ui:editor_share_steam-descriptor-mature}}`
- `{{ui:editor_share_steam-descriptor-violence}}`
- `{{ui:editor_share_steam-descriptor-some-nudity}}`
- `{{ui:editor_share_steam-descriptor-frequent-nudity}}`
- `{{ui:editor_share_steam-descriptor-adult-only}}`

記述子は公開のたびに送信され、レベルには保存されません。公開のたびにセット全体が送信されるので、チェックを外すと、すでに公開済みのアイテムからもその記述子が外れます。記述子は、アップロード直後の2回目の更新で送られます。この部分が失敗してもアイテムは公開済みで、結果に記述子が設定されなかったことが表示されます

### 公開後

成功すると、作成または更新されたアイテムと、`{{ui:editor_publish_open-item}}`ボタンがフォームに表示されます。このボタンはSteamでアイテムのページを開きます

失敗すると、フォームに次の内容が表示されます：
- わかりやすい言葉での理由：`公開に失敗しました：...`
- `送信内容とSteamの応答：...`：英語の技術的な行です。問題を報告するときは、この行を開発者に引用して伝えることをおすすめします
- `?`：Steamがこのように拒否する理由を展開し、3つのリンクを示します：`{{ui:editor_publish_help-docs}}`（このページ）、`{{ui:editor_publish_help-steam-support}}`、`{{ui:editor_publish_help-agreement}}`

公開に関するゲーム自身のログの行は、インターフェースの言語に関係なく常に英語です

| 理由 | 対処 |
|---|---|
| `{{ui:enum_workshop-failure_steam-not-running}}` | Steamを起動し、Steamからゲームを再起動します |
| `{{ui:enum_workshop-failure_not-owner}}` | そのアカウントから公開するか、レベルのコピーを作ります。コピーは新しいアイテムとしてアップロードされます |
| `{{ui:enum_workshop-failure_access-denied}}` | アカウントがゲームを所有していない、アカウントが制限されている（Steamでまだ購入したことがない）、またはそのアカウントにはワークショップが閉じられています |
| `{{ui:enum_workshop-failure_invalid-param}}` | ゲームのワークショップがアップロード用に設定されていないか、Steamが別のゲームのIDで動いています。Steamとゲームを再起動します |
| `{{ui:enum_workshop-failure_limit-exceeded}}` | ワークショップのファイルで古いアイテムを削除します |
| `{{ui:enum_workshop-failure_connection}}` | 接続とSteamのステータスを確認します |
| `{{ui:enum_workshop-failure_invalid-request}}` | タイトルは128文字まで、説明は8000文字まで、プレビューはpngまたはjpgで1MBまで |
| `{{ui:enum_workshop-failure_staging}}` | ディスクの空き容量と、レベルのファイルが別のプログラムで開かれていないことを確認します |

新しいアイテムが作成されたのにアップロードが拒否された場合、ゲームはその空のアイテムを削除します。ワークショップに放置されたアイテムが残らないようにするためです

## Steamなしのビルド

Steamなしのビルドでは、リストに`{{ui:editor_share_steam}}`が表示されません。`{{ui:editor_share_archive}}`は残ります

## コレクションを共有する方法

コレクションは、「ライブラリ」タブにあるそのページから共有します。`{{ui:editor_share_share}}`で同じパネルがウィンドウで開きます：`{{ui:editor_share_archive}}`があり、Steam版では自分のコレクションに`{{ui:editor_share_steam}}`も使えます

コレクションのチェック：
- 名前がある
- ライセンスが指定されている
- 空ではない
- 指定しているファイルがすべて中にある
- エントリーが参照するリソースがすべて含まれている

ライセンスがない場合の扱いは、方法によって違います。`{{ui:editor_share_archive}}`では警告で、エクスポートは実行されます。`{{ui:editor_share_steam}}`ではエラーです。エラーがあると実行できません。コレクションの詳細：[[16_library-and-collections]]

## 1つのリソースを共有する方法

ライブラリのテーマ、シェイプ、エフェクト、プレハブの各行にも`{{ui:editor_share_share}}`ボタンがあります。このボタンは、リソースを必要なものすべて（たとえばプレハブのシェイプ、テクスチャ、入れ子のプレハブ）と一緒に、1エントリーのコレクションとしてまとめます

使えるのは`{{ui:editor_share_archive}}`だけで、コレクションと同じ5つの形式（パスワード付きの形式を含む）を選べます。受け取った側は、ほかのコレクションと同じく`{{ui:editor_library_import-archive}}`でファイルをインポートします

## ワークショップのタグ

タグはゲームが自動で設定します：

| アイテム | タグ |
|---|---|
| レベル | `level` |
| コレクション | `collection`と、中にある種類ごとに1つ：`prefabs`、`themes`、`shapes`、`effects` |

テクスチャ、フォント、オーディオにはタグが付かず、単独ではワークショップに送られません。これらはコレクションの中に、そのプレハブ、テーマ、シェイプ、エフェクトが使うものとして入ります。メディアだけのコレクションは、理由を示す行とともに拒否されます。そのようなコレクションは、アーカイブで共有するほうが適しています

> [!info] 補足
> Steam独自の「コレクション」は、ワークショップのアイテムを集めたリストで、Valveの機能です。Bullet Heroのコレクションとは関係ありません

## サブスクリプション

Steam版は、サブスクライブしているものを読み込みます：
- レベルは、レベル一覧の`{{ui:editor_library-source_workshop}}`に表示されます。[[2_playing-levels]]
- コレクションは、エディターのライブラリの`{{ui:editor_library-source_workshop}}`チップに、読み取り専用で表示されます

次へ：[[5_publish-readiness]]、[[1_licensing-basics]]、[[16_library-and-collections]]
