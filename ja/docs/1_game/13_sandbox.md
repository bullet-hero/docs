---
title: サンドボックスとチュートリアル
date: 2026-10-02
tags: [player]
---

# サンドボックスとチュートリアル

サンドボックスはメインメニューにあるアリーナです。アバターを動かし、6種類の攻撃のどれでも自分に向けて撃ち、6ステップのチュートリアルを受けられます。レベルは必要ありません

初回起動時、ゲームはチュートリアルを1回だけ勧めます：`{{ui:menu_tutorial-offer_confirm}}`でチュートリアルの状態のサンドボックスが開き、`{{ui:menu_tutorial-offer_cancel}}`でこの案内は二度と表示されなくなります。どちらを選んでも、サンドボックス自体はメニューに残ります

## パネル

サンドボックスには左側にパネルが1つあります。ハンドルをクリックするとパネルが折りたたまれ、ハンドルをドラッグするとパネルの幅を変えられます。パネルには5つのタブがあります：

| タブ | 機能 |
|---|---|
| `{{ui:sandbox_tab_home}}` | サンドボックスとは何か、各タブで何ができるか |
| `{{ui:sandbox_tab_tutorial}}` | チュートリアルのステップと、今やるべきこと |
| `{{ui:sandbox_tab_controls}}` | 今操作しているデバイスのモード、モーションセンサーのスイッチ、すべての操作設定への入口 |
| `{{ui:sandbox_tab_attacks}}` | 6種類の攻撃のどれでも手動で撃つ、またはウェーブを自動で来させる |
| `{{ui:sandbox_tab_game}}` | ライフ、攻撃速度、ボット、フリーカメラ |

`{{ui:settings_common_title}}`は、サンドボックスの上にゲームの設定を開きます。`{{ui:sandbox_panel_exit}}`でメインメニューに戻ります

## 一時停止

一時停止ボタンは画面の右上にあります。`Esc`でも、サンドボックスを抜けるのではなく一時停止が開きます。一時停止はレベルと同じくすべてを止めます：アバター、攻撃、チュートリアル。一時停止ウィンドウには`{{ui:root_error_continue}}`、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-menu}}`があります

## チュートリアル

6つのステップを順に進めます：

1. `{{ui:sandbox_tutorial_move_title}}`：画面の幅くらいの距離を移動する
2. `{{ui:sandbox_tutorial_dash_title}}`：ダッシュを3回する
3. `{{ui:sandbox_tutorial_dodge_title}}`：スローになった弾幕の中で、被弾せずに10秒耐える。被弾するとカウントが最初からやり直しになる
4. `{{ui:sandbox_tutorial_dash-through_title}}`：リングが画面の端の外まで広がるので、抜け出すにはリングの縁をダッシュで通り抜けるしかない。リングを2つ通過する必要がある。失敗したリングがあっても、すでに通過したリングは取り消されない。ダッシュ中は何にも当たらない
5. `{{ui:sandbox_tutorial_choose-mode_title}}`：`{{ui:sandbox_tab_controls}}`タブでモードを試し、`{{ui:sandbox_tutorial_confirm-mode}}`を押す
6. `{{ui:sandbox_tutorial_done_title}}`：`{{ui:sandbox_tutorial_play-level}}`でチュートリアルレベルが始まる

アリーナでステップを進めている間、パネルは折りたたまれ、ステップは画面上部の小さなカードとして表示されます。タッチはカードを通り抜けます。ハンドルでは引き続きパネルを開けます。`{{ui:sandbox_tutorial_choose-mode_title}}`と`{{ui:sandbox_tutorial_done_title}}`のステップでは、パネルが`{{ui:sandbox_tab_tutorial}}`タブで自動的に開きます

被弾や死亡でやり直しになるのは、それが起きたステップだけです。チュートリアル全体ではありません。そのステップは通過するまで赤くなります。通過したステップは緑です

一覧のステップをクリックすると、通過済みのものも含めてそのステップが始まります。ステップを通過すると、チュートリアルは次の未通過のステップに進みます。チュートリアルが完了扱いになるのは、すべてのステップを通過したときだけです。統計に記録されるのもそのときです。同じタブの`{{ui:sandbox_tutorial_restart}}`で、いつでも最初からやり直せます

> [!warning] 警告
> `{{ui:sandbox_tab_game}}`タブで`{{ui:sandbox_game_immortal}}`にすると被弾がまったく数えられないため、`{{ui:sandbox_tutorial_dodge_title}}`と`{{ui:sandbox_tutorial_dash-through_title}}`のステップでも被弾が認識されません。チュートリアルを受ける間は、ライフをいくつか残しておいてください

## 操作

モードは今操作しているデバイスについて切り替わり、すぐに保存されます。モーションセンサーには`{{ui:enum_control-mode_relative}}`モードがありません。各モードの意味：[[3_controls#操作モード]]

## 攻撃とゲーム

- `{{ui:sandbox_attacks_auto}}`は、メインメニューの背景と同じように、`{{ui:sandbox_attacks_gap}}`の間隔でランダムなウェーブを撃ちます
- `{{ui:sandbox_attacks_clear}}`は、画面上の攻撃をすべて消します
- `{{ui:sandbox_game_speed}}`は、攻撃だけを遅くしたり速くしたりします。アバターは常に自分の速度で動きます
- ライフ：`{{ui:sandbox_game_immortal}}`、1、3、5。ライフが尽きても元に戻り、サンドボックスは終わりません
- `{{ui:sandbox_game_bot}}`は、メインメニューの背景でプレイしているのと同じボットにアバターを任せます
- `{{ui:sandbox_game_free-camera}}`で、画面の端の外を見られます：マウスの中ボタンか2本指で視点を動かし、ホイールかピンチでズームします。青い枠はレベルのカメラに映る範囲を示し、`{{ui:sandbox_camera_back}}`で視点をそこに戻せます。操作、ダッシュ、攻撃は、フリーカメラなしのときと同じように動きます
- 死亡はレベルと同じように演出されます：攻撃がスローになって消え、アバターがライフ満タンで中央に現れます
