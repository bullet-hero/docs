---
title: ダメージとライフ
date: 2026-10-02
tags: [advanced_player]
---

# ダメージとライフ

被弾するたびにライフが1つ減り、アバターは{{v:avatar.knockback-time}}秒ノックバックされ、{{v:avatar.damage-timeout}}秒の無敵時間を得ます。デフォルトでは、死亡するとレベルが最後のチェックポイントまで巻き戻り、ライフが回復します

## 被弾の3段階

1. **押し出し、`{{v:avatar.knockback-time}}`秒**。当たったものから毎秒`{{v:avatar.knockback-speed}}`ユニットで弾き飛ばされます。約{{v:avatar.knockback-distance}}ユニット、ダッシュ1回分で、デフォルトの画面の高さの4分の3です。その間は入力を受け付けません。ダッシュで押し出しから抜けることはできません：ノックバックはすべてに優先します
2. **操作が戻ります**。その{{v:avatar.knockback-time}}秒の後です
3. **被弾しません**。被弾の瞬間からまる`{{v:avatar.damage-timeout}}`秒間です。その1秒の間の被弾はすべて無視されます

当たったものの真上に立っている場合は、押し出す方向がありません。その場合はノックバックされません

出現中（`{{v:avatar.spawn-time}}`秒）と、ダッシュの無敵時間`{{v:avatar.dash-invulnerability}}`秒の間も被弾しません、[[6_avatar]]

> [!info] 補足
> 危険地帯の中にとどまっても、失うライフは10ではなく1つです。2つ目の危険地帯へ押し出されても生き残れます。密集した弾幕は即死に見えますが、無敵の1秒がちょうど終わるときに届く1発の弾より安く済むことがよくあります

## ライフ

ライフの数はレベル画面で選びます：`{{ui:menu_levelview_options-lifes_option-zen}}`、`{{ui:menu_levelview_options-lifes_option-one}}`、`{{ui:menu_levelview_options-lifes_option-three}}`、または最大16までの`{{ui:menu_levelview_options-lifes_option-custom}}`、[[2_playing-levels]]

被弾するたびにライフが1つ減ります。最後のライフを失う被弾が死亡です。`{{ui:menu_levelview_options-lifes_option-zen}}`も被弾には通常のプレイと同じように反応します。押し出し、シールドの輪、パーティクルの飛散、1秒の無敵は通常どおり働き、被弾は統計に記録されます。ただしライフは決して減らないので、プレイが終わることはありません

ライフはアバターの周りの点の輪で表示されます：点灯している点は残りのライフ、消えている点は失ったライフです。結果ウィンドウには`{{ui:game_game-result_hits}}`と`{{ui:game_game-result_lives-left}}`が表示されます

## 死亡すると何が起きるか

デフォルトでは、死亡してもプレイは終わりません：

1. レベルの時計が実時間で`{{v:checkpoint.rewind-time}}`秒かけてなめらかに止まります。音楽もそれに合わせて沈みます
2. レベルは最後に到達したチェックポイントまで戻ります。ライフが回復します
3. 時計がさらに`{{v:checkpoint.rewind-time}}`秒かけて、なめらかにプレイ速度まで戻ります。この加速中は被弾しません。そうでなければ、危険な場所の近くにあるチェックポイントが最初の1秒ですべてのライフを奪ってしまいます

一時停止すると、この加速も止まります

レベル画面で`チェックポイント`がオフの場合、巻き戻し先はレベルの最初になります

死亡時に結果ウィンドウを開くには、`{{ui:settings_common_title}}` → `{{ui:settings_interface_label}}` → `{{ui:settings_interface_open-menu-on-lose}}`をオンにします。その場合、再生は止まります。そのウィンドウの`{{ui:game_game-result_restart-checkpoint}}`で、到達したチェックポイントから新しい挑戦を始められます

## チェックポイント

チェックポイントはレベルの作者が配置します。それを使うかどうかは、`チェックポイント`の切り替えで自分で決められます

到達したチェックポイントとは、レベル内の現在位置かそれより前にある最後のチェックポイントです。そのため、そこへ戻っても何かが取り消されるわけではなく、巻き戻るだけです

作者はチェックポイントに体力を回復させることもできます。その場合、そこを通過するとプレイの途中でライフが1回回復します

画面下部の進行状況バーには、チェックポイントごとに目盛りがあります。バーは`{{ui:settings_interface_label}}` → `{{ui:settings_interface_show-game-progress}}`でオンにします

チェックポイントありとなしの記録は別々に保存されます、[[10_statistics]]

## 衝突なし

`{{ui:menu_levelview_options-no-collision_title}}`は`{{ui:menu_levelview_options-lifes_option-zen}}`とは別の切り替えで、レベル画面とエディターの起動パネルの`チェックポイント`の横にあります。オンにすると、アバターはすべてをすり抜けます：もう何も触れられません

`{{ui:menu_levelview_options-no-collision_title}}`のプレイは、`{{ui:menu_levelview_options-lifes_option-zen}}`や通常のプレイとは別に独自の記録を持ちます。結果ウィンドウでは`{{ui:menu_levelview_options-lifes_title}}`の値に`· 衝突なし`が付いて区別されます、[[10_statistics]]
