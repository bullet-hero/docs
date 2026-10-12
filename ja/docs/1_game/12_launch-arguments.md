---
title: 起動引数
date: 2026-10-12
tags: [advanced_player, developer]
---

# 起動引数

起動引数を使うと、画面、レベル、プレイをすぐに開けます。スイッチはゲームの1回の起動だけを変えます。引数は実行ファイルの後ろに書きます：ショートカット、ターミナル、Steamの起動オプションのいずれかです

引数なしでは、ゲームはメインメニューを開きます

MCPで接続したAIアシスタントは、すでに起動しているゲームに同じ引数を送れます（[[7_ai-assistant]]）

## 構文

- 引数はすべてハイフン2つで始まります：`--editor`
- 値はスペースか`=`の後に続けます：`--speed 1.5`と`--speed=1.5`は同じです
- キーの大文字と小文字は区別されません：`--Editor`でも動きます
- 数値はシステムの言語にかかわらずドットを使います：`1.5`と書き、`1,5`とは書きません
- スペースを含む値はダブルクォートで囲みます：`--level "D:\My Levels\Volcano"`

**ゲームが使えない引数で起動が止まることはありません**。その引数は捨てられ、ログに1行記録され、ゲームはいつもの画面を開きます。ログの場所：[[11_help#ログ]]

**知らない引数は無視されます**。ゲームが読むのは、ハイフン2つで始まる自分の引数だけです。ハイフン1つで始まるUnity自体の引数（たとえば`-screen-width`）は、そのまま渡されます。解像度とフルスクリーンはそちらで設定してください

## 画面

| 引数 | 開くもの |
|---|---|
| `--menu` | メインメニュー。引数なしと同じ |
| `--editor` | レベルエディター |
| `--game` | `--level`で指定したレベル。プレイがすぐに始まる |
| `--settings` | メインメニューと、その上に重なる設定画面 |

画面を指定する引数は1つまでです。異なる2つを渡すと互いに打ち消し合い、ログに警告が出てメニューが開きます

`--settings`にはタブ名を指定できます：`general`、`audio`、`controls`、`keybindings`、`graphics`、`interface`、`game-editor`、`profile`、`other`。名前がなければ、前回開いていたタブで設定が開きます。知らない名前は捨てられ、設定はそのまま開きます

設定が開くのは1回の起動につき1回だけです。後でメニューに戻っても、もう一度は開きません。各タブの内容：[[4_settings]]

## レベルの指定

`--level`は、レベルをその識別子（`LevelId`）またはフォルダーへのパスで指定します。タイトルは使えません：タイトルは重複し、翻訳され、編集されるためです。識別子として読める値は、常に識別子として扱われます

レベルは、ゲームがすでに一覧に表示しているものの中から探されます。一覧にないフォルダーは見つかりません

| 組み合わせ | 結果 |
|---|---|
| なし | メニューがレベル画面で開き、`{{ui:menu_levelview_play-btn}}`を待つ |
| `--editor` | このレベルを開いた状態でエディターが開く |
| `--game` | プレイがすぐに始まる |

パスワードが引数で渡されることはありません。保護されたレベルは画面上でパスワードを尋ね、入力後に開きます

## プレイ条件

これらの条件はレベル画面の各項目を埋め、`{{ui:menu_levelview_play-btn}}`を押したときと同じようにプレイが始まります。`--game`と一緒のときだけ有効です。`--game`がなければ、ログに警告が出て無視されます

| 引数 | 値 | レベル画面の項目 |
|---|---|---|
| `--speed` | `0`より大きく`2`以下、`0.1`単位に丸められる | `{{ui:field_common_speed}}` |
| `--lives` | `0`から`16`、`0`は`{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0`または正の整数、`0`はプレイのたびに新しいシード | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`、`reflex`、`warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`、`--no-checkpoints` | なし | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | なし | `{{ui:menu_levelview_options-no-collision_title}}` |

省略した条件はデフォルト値になります：ライフ3、速度`1.0`、チェックポイントあり、ボットなし、シード`0`、衝突あり

この方法で始めたプレイは通常のプレイです。ほかのプレイと同じく統計に入ります（[[10_statistics]]）

## 起動全体のスイッチ

次の3つはどの画面とも組み合わせられ、保存された設定を変えることはありません：

| 引数 | 動作 |
|---|---|
| `--autosave on`、`--autosave off` | この起動の間だけ、エディターの自動保存をオンまたはオフにする。設定の`{{ui:settings_game-editor_title}}`タブには強制された値が表示され、変更できない |
| `--suppress-game-saves` | 起動全体を匿名モードにする。ゲーム内ではオフにできない（[[4_settings#匿名モード]]） |
| `--frame-stats` | フレーム時間の集計を、GPUとCPUの時間つきでログに書き出す。パフォーマンス計測に使う |

`--frame-stats`は画面ごとに30秒に1回、さらに画面の上のウィンドウが切り替わるたびに1行書き出します。画面の最初の3秒は数えられません

## 組み合わせ

| コマンド | 結果 |
|---|---|
| なし、または`--menu` | メニュー |
| `--editor` | レベルを開いていないエディター |
| `--settings` | メニュー。設定は前回開いていたタブで開く |
| `--settings graphics` | 同上。`{{ui:settings_graphics_title}}`タブで開く |
| `--level X` | レベルXの画面を表示したメニュー。`{{ui:menu_levelview_play-btn}}`を待つ |
| `--level X --game` | レベルX、プレイ中 |
| `--level X --editor` | レベルXを開いたエディター |
| `--level`なしの`--game` | メニューと警告 |
| `--menu --editor` | メニューと警告 |
| `--game`なしの`--speed 2` | 条件は警告とともに無視される |
| `--editor --autosave off` | エディター。この起動の間だけ自動保存がオフ |
| `--autosave maybe` | 警告とともに無視され、自分の設定が使われる |
| `--suppress-game-saves` | メニュー。この起動中のゲーム自体の保存は、どれもディスクに書かれない |
| `--level X --game --suppress-game-saves` | レベルX、プレイ中。プレイ後に統計は残らない |
| `--editor --suppress-game-saves` | エディター。レベルの保存、自動保存、バックアップは書かれるが、設定と統計は書かれない |

## 例

Windowsで、ターミナルまたはショートカットから：

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

Steamでは、ゲームの起動オプションに実行ファイルなしで引数だけを書きます：`--editor --autosave off`

## Android

Androidにはコマンドラインがありません。引数は、ゲームを起動するインテントの文字列エクストラ`bh`で渡され、入力した1行とまったく同じように分割されます。コンピューターからは`adb`で行います：

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **クォートが重要です**。`am start`全体をダブルクォートで、`bh`の値をシングルクォートで囲みます。そうしないとデバイスのシェルが行を分割してしまい、`bh`には最初の引数だけが入り、残りは`am`自身のパラメーターとして渡されます
- **`-S`は、起動中のゲームを先に停止します**。引数は起動時に1回だけ読まれます。すでに起動しているゲームに送っても何も変わりません

iOSには起動引数がまったくありません
