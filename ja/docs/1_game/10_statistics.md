---
title: 統計
date: 2026-10-02
tags: [advanced_player]
---

# 統計

ゲームはレベルごと、そしてデバイス全体について、試行回数、死亡回数、被弾数、時間を数えます。すべてstatsフォルダーにローカル保存されます。記録はプレイ条件の組み合わせごとに別々に残ります

## 2つのファイル

| ファイル | 中身 |
|---|---|
| `stats/statistics.json` | プレイヤー自身のすべて：全レベルと全画面にわたる |
| `stats/<LevelId>.json` | 1つのレベルで行ったことのすべて |

ファイルはJSONで、時刻はUTCです。どこにも何も送信されません

`stats`フォルダーはゲームフォルダー内の`levels`の隣にあります（[[1_installation]]）。レベルの中にあることはありません。そのため、友人に送ったレベルがクリア済みの状態で届くことはありません。また、レベルを削除してもう一度インポートしても、進行状況は残ります

## 「プロファイル」タブ

`{{ui:settings_common_title}}` → `{{ui:settings_profile_tab}}`には、デバイス共通のファイルが表示されます：

| セクション | 行 |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`、`{{ui:settings_profile_last-played}}`、`{{ui:settings_profile_launches}}`、`{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`、`{{ui:settings_profile_game-time}}`、`{{ui:settings_profile_editor-time}}`、`{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`、`{{ui:settings_profile_clears}}`、`{{ui:settings_profile_deaths}}`、`{{ui:settings_profile_hits}}`、`{{ui:settings_profile_levels-played}}`、`{{ui:settings_profile_levels-cleared}}`、`{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`、`{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`、`{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`、`{{ui:settings_profile_tutorial-first}}`、`{{ui:settings_profile_tutorial-last}}`。完了として数えられるのは、[[13_sandbox|サンドボックスのチュートリアル]]のすべてのステップを終えたときだけです |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`、`{{ui:settings_profile_levels-deleted}}`、`{{ui:settings_profile_objects}}`、`{{ui:settings_profile_operations}}`、`{{ui:settings_profile_generators}}`、`{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`、`{{ui:settings_profile_device-touch}}`、`{{ui:settings_profile_device-gamepad}}`、`{{ui:settings_profile_device-gyro}}` |

時間はレベル内の時間ではなく、現実の秒数で数えられます。チェックポイントでのスローモーションや半分の速度でのプレイも、実際にかかった時間だけ数えられます

デバイスの行は、プレイ中にどのデバイスでアバターを操作したかを示します。接続されているだけのデバイスは数えられません

## レベルごと

レベルのファイルには次の内容が保存されます：

- 最初と最後にプレイした日時
- レベル内で過ごした現実の時間とセッション数
- 試行（リスタートのたびに新しい試行になる）、クリア、死亡、被弾、ダッシュ
- チェックポイントへの復帰と途中で放棄したプレイ
- 到達した最も遠い地点と初クリア
- レベルのどこで死亡するか：長さに対する割合ごとと、チェックポイントごと

## 記録

記録はプレイ条件ごとに残ります：ライフ、速度、チェックポイントのオン/オフ、衝突のオン/オフ、ボット。速度は画面の表示どおり、小数第2位まで区別されます

禅（ライフ0）でも被弾は数えられます。衝突はすべて数値に入り、免除されるのはライフの減少とプレイの終了だけです

同じ条件の記録を更新するのは、次の順に比べて上回ったプレイです：

1. より遠くまで進んだ
2. 被弾が少なかった
3. 残りライフが多い状態で終わった
4. ダッシュの使用が少なかった

記録には、そのプレイのシードと、その時点のレベルのバージョンも保存されます。バージョンは条件に含まれません。そのため、レベルが作り直される前に出した記録も、横にバージョンが表示された状態で見え続けます

**エディターからのプレイは数えられますが、記録にはなりません**。試行回数、死亡回数、被弾数には加算されます。レベルがメモリ上にしか存在しなかったため、記録、最高進行度、初クリアにはなりません

## 書き込み、削除、凍結

ゲームは統計を30秒ごとに書き込みます。さらに、プレイの終了時、画面の切り替え時、終了時にはすぐに書き込みます。クラッシュで失われるのは最大30秒分のデータです

- **削除**：`{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_other_cache-title}}`。そこに`{{ui:settings_other_cache-orphan-statistics}}`と`{{ui:settings_other_cache-all-statistics}}`があります
- **レベルと一緒に削除**：レベルを削除するときに`{{ui:root_level-delete_statistics}}`が表示されます
- **凍結**：匿名モードは、ゲームを閉じるまですべての書き込みを止めます（[[4_settings]]）
- **別のデバイスへ移す**：プロファイルをエクスポートし、移行先でインポートします。統合では各カウンターの大きいほうの値が残ります（[[14_profile-transfer]]）

> [!warning] 警告
> 手作業でコピーしたレベルフォルダーは、レベルのIDをそのまま保ちます。元のレベルとコピーは1つの統計ファイルを共有します
