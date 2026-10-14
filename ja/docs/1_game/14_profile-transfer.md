---
title: プロファイル転送
date: 2026-10-14
tags: [player]
---

# プロファイル転送

プロファイル全体は1つのzipファイルに収まります：レベル、統計、設定、ライブラリ。再インストールや別のデバイスへの移行の前にエクスポートし、移行先でインポートしてください

ボタンは`{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`にあります。Windows、Mac、Linux、Androidで使えます。iOSでは使えません

## ファイルに入るもの

| 項目 | データフォルダー内 | デフォルトでチェック |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | あり |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | あり |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | あり |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | あり |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | なし |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | なし |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | なし |

ファイルは普通のzipで、どのアーカイバーでも開けます。中身はデータフォルダー（[[1_installation]]）と同じフォルダーに、ファイルの内容を記述した`profile.json`を加えたものです

## エクスポート

1. `{{ui:settings_profile-transfer_export}}`を押す
2. 必要な項目にチェックを入れる
3. ファイルの保存先を選ぶ

エクスポートは設定を開ける場所ならどこでも使えます：メインメニュー、一時停止中のプレイ、エディター。統計は先にディスクへ書き込まれるので、ファイルは最新の状態になります

## インポート

1. メインメニューから設定を開き、`{{ui:settings_profile-transfer_import}}`を押す
2. zipファイルを選ぶ
3. 項目にチェックを入れ、モードを選ぶ
4. 確定する

インポートはメインメニューからしか使えません。実行中のレベルや開いているエディターは自分のファイルを使用中で、その下でファイルを差し替えることはできないためです

| モード | 結果 |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | チェックした各項目を空にし、ファイルの内容で埋める |
| `{{ui:settings_profile-transfer_mode-merge}}` | レベルが追加される。両方にあるレベルは、新しいほうのコピーで丸ごと置き換えられる。統計は各カウンターの大きいほうの値と、よいほうの記録が残る。ライブラリのファイル、自動保存、レポートは追加されるだけで、手元のものは残る |

どのインポートも、何かを書き込む前にもう一度確認します。置き換えでは空にする項目が、統合では追加、置き換え、維持されるレベルの数が表示されます

**別の種類のデバイスの設定**。スマートフォンのプロファイルをコンピューターにインポートした場合（またはその逆）、自分の操作設定とグラフィック設定はそのまま残ります。それ以外はすべてファイルから読み込まれます

新しいバージョンのゲームで作られたファイルは拒否されます。先にゲームを更新してください。zipではないファイル、プロファイルではないzip、パスワード付きのzip、壊れたファイルも拒否されます。どの場合も何も変更されません

## バックアップ

どのインポートの前にも、ゲームは置き換える予定の項目を1つのバックアップに保存します。バックアップはデータフォルダー内の`profile-backups`フォルダーにあります。バックアップは1つだけで、次のインポートで上書きされます

- `{{ui:settings_profile-transfer_backup-restore}}`は、バックアップを元に戻します。それによって置き換えられた内容が新しいバックアップになるので、復元も取り消せます
- `{{ui:settings_profile-transfer_backup-save-as}}`は、選んだ場所にコピーを保存します
- `{{ui:settings_profile-transfer_backup-delete}}`は、バックアップを削除します
- `{{ui:settings_profile-transfer_clear-cache}}`は、`profile-backups`フォルダー全体を削除します：バックアップと、中断した移行が残したもの

インポート時には`{{ui:settings_profile-transfer_backup-to-folder}}`がデフォルトでチェックされています：ゲームはすぐに、ゲームの外のどこにコピーを保存するかを尋ねます

> [!caution] 注意
> Androidではバックアップはゲームのデータフォルダーにあり、ゲームと一緒に削除されます。アンインストールの前に、プロファイルをエクスポートするか、バックアップを別の場所に保存してください

インポートの途中でゲームが閉じた場合、次回の起動時にプロファイルは元の状態に戻ります

## Steam Cloud

Steam版では、プロファイルはSteamアカウントに自動で付いていきます。ボタンはありません。ゲームは起動時に1回同期し、プレイ中に変わったものを送り、終了時に最後の同期をします

スイッチはSteam側にあります：Steamのゲームのプロパティにある「Steam Cloud」のチェックボックスです。オンかどうか、最後の同期がいつかは`{{ui:settings_common_title}}`→`{{ui:settings_other_title}}`→`{{ui:settings_cloud_title}}`に表示されます

| 部分 | 2台のデバイスの両方で変更したとき |
|---|---|
| `{{ui:settings_profile-transfer_category-statistics}}` | 各カウンターは大きい方の値と良い方の記録を残し、何も失われません |
| `{{ui:settings_profile-transfer_category-settings}}` | 新しい方のコピーが優先されます。`{{ui:settings_graphics_title}}`と`{{ui:settings_controls_title}}`は、各デバイスで常にそのデバイスのものが残ります |
| `{{ui:settings_profile-transfer_category-levels}}` | レベルの新しい方のコピーが丸ごと優先されます。もう一方は、負けた側のデバイスでエディターのバックアップに入ります |
| `{{ui:settings_profile-transfer_category-library}}` | ファイルごとに新しい方のコピーが優先されます |

- 1台のデバイスで削除したレベルは、他のデバイスでも削除されます。それぞれのデバイスは、そのレベルの最後の状態をエディターのバックアップに残します
- 1台のデバイスで削除した統計は、他のデバイスでも削除されます。最後の同期の後に別のデバイスでプレイしていた場合、その進行状況は残ります
- Steamがゲームに割り当てる容量より大きいレベルは、そのデバイスにだけ残ります
- `{{ui:settings_profile-transfer_category-backups}}`、`{{ui:settings_profile-transfer_category-reports}}`、`{{ui:settings_profile-transfer_category-recordings}}`は同期されません
- 新しいバージョンのゲームが書いたクラウドのコピーは、このデバイスのゲームを更新するまで変更されません
- エディターで開いているレベルは置き換えられません。次の起動時に同期されます
- `{{ui:settings_other_suppress-game-saves}}`がオンのときは、何も同期されません

## Androidでのビルド間の移行

ファイルからインストールしたゲーム（itch.ioなど）はGoogle Playから更新できず、その逆もできません。ビルドの署名が異なるため、Androidが更新を拒否します。乗り換えるには：

1. プロファイルをエクスポートし、ファイルをゲームの外に保存する
2. ゲームをアンインストールする
3. もう一方のビルドをインストールする
4. プロファイルをインポートする
