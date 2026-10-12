---
title: ヘルプと不具合の報告
date: 2026-10-02
tags: [player, level_author]
---

# ヘルプと不具合の報告

ゲームの不具合はreleasesのissuesへ、質問はDiscordへ送ってください。設定画面のバージョン文字列と、不具合が起きるまでの手順を添えてください

まず[[5_troubleshooting]]を確認してください。レベルが見つからない、「ゲームの更新が必要」、アーカイブが拒否される、といったケースはそちらで扱っています

## 送り先

| 内容 | 送り先 |
|---|---|
| ゲームやエディターの不具合、ゲームへの要望 | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| SDKやそのコードの不具合 | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| ドキュメントの誤りや古くなった情報 | [bullet-hero/docs](https://github.com/bullet-hero/docs)、[[community]] |
| 質問、レベル制作の相談、議論 | [Discord](https://discord.gg/gkHQrp9NgS) |

GitHubへの投稿は公開されます。誰でも読んだり追記したりできます。ドキュメントにはissueやpull requestを送れます

不具合かどうかわからない場合は、まずDiscordで聞いてください

プロジェクトのリンク一覧：[[links]]

## 不具合報告に書くこと

再現できる不具合は修正されます。「落ちた」だけでは、何を繰り返せばよいかわからないため、たいてい修正できません

1. **バージョン文字列**。設定画面のバージョン文字列をクリックすると、自動でコピーされます。形式は`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`です（[[4_settings]]）
2. **プラットフォームとデバイス**：OS、スマートフォンの場合は機種
3. **手順**：何をしたか、何を期待したか、何が起きたか
4. **レベル**：不具合がレベルに関係する場合は、そのフォルダーをアーカイブにしたもの、または開いたアーカイブ。レベルが保護されている場合は、その旨も書いてください
5. **エラーレポート**：エラーウィンドウが出た場合。`{{ui:root_error_save}}`で`reports`フォルダーに書き出し、`{{ui:root_error_open-reports-folder}}`でそのフォルダーを開けます（[[1_installation]]）

> [!tip] ヒント
> ファイルは本文に貼り付けず、投稿に添付してください。ログは長く、本文の中では読みにくくなります

## ログ

ゲームは動作中にログを書き出します。エラーウィンドウがまったく出なかった場合に役立ちます

- **Windows**：ゲームのデータフォルダー`C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero`にある`Player.log`（Unityの標準の場所）
- **Android**：ログはlogcatに出力されます。デバイスをコンピューターに接続した状態で、`adb logcat -s Unity`を実行すると表示されます
- **その他のOS**：まだ記載がありません
