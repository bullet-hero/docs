---
title: 沙盒與教程
date: 2026-10-02
tags: [player]
---

# 沙盒與教程

沙盒是主選單中的一個競技場，你可以在這裡移動化身，向自己發射六種攻擊中的任意一種，並完成六個步驟的教程。不需要任何關卡

首次啟動時，遊戲會提供一次教程：`{{ui:menu_tutorial-offer_confirm}}`在教程中開啟沙盒，`{{ui:menu_tutorial-offer_cancel}}`永久關閉這個提示。無論如何，沙盒本身都會留在選單中

## 面板

沙盒左側有一個面板。點選面板的把手可以摺疊面板，拖動把手可以把面板拉寬或拉窄。面板有五個標籤頁：

| 標籤頁 | 作用 |
|---|---|
| `{{ui:sandbox_tab_home}}` | 沙盒是什麼，以及每個標籤頁的作用 |
| `{{ui:sandbox_tab_tutorial}}` | 教程的步驟，以及現在要做什麼 |
| `{{ui:sandbox_tab_controls}}` | 你當前操控所用裝置的模式、體感開關，以及前往全部操作設定的入口 |
| `{{ui:sandbox_tab_attacks}}` | 手動發射六種攻擊中的任意一種，或讓波次自動出現 |
| `{{ui:sandbox_tab_game}}` | 生命、攻擊速度、機器人和自由相機 |

`{{ui:settings_common_title}}`在沙盒上方開啟遊戲設定。`{{ui:sandbox_panel_exit}}`返回主選單

## 暫停

暫停按鈕在螢幕右上角。`Esc`同樣開啟暫停，而不是退出沙盒。暫停會停止一切，和在關卡中一樣：化身、攻擊和教程。暫停視窗中有`{{ui:root_error_continue}}`、`{{ui:settings_common_title}}`和`{{ui:game_game-result_back-to-menu}}`

## 教程

六個步驟，按順序：

1. `{{ui:sandbox_tutorial_move_title}}`：移動大約一個螢幕寬度的距離
2. `{{ui:sandbox_tutorial_dash_title}}`：衝刺三次
3. `{{ui:sandbox_tutorial_dodge_title}}`：在減速的齊射下堅持10秒不被擊中。被擊中會重新開始計時
4. `{{ui:sandbox_tutorial_dash-through_title}}`：圓環會擴大到螢幕邊緣之外，所以只能通過沖刺穿過它的邊緣離開。需要穿過兩個圓環，失敗的圓環不會取消已經穿過的圓環。衝刺期間什麼都擊不中你
5. `{{ui:sandbox_tutorial_choose-mode_title}}`：在`{{ui:sandbox_tab_controls}}`標籤頁上嘗試各個模式，然後按`{{ui:sandbox_tutorial_confirm-mode}}`
6. `{{ui:sandbox_tutorial_done_title}}`：`{{ui:sandbox_tutorial_play-level}}`啟動教程關卡

在競技場上進行某個步驟時，面板會摺疊，步驟以一張小卡片顯示在螢幕上方。觸控會穿過卡片。把手依然可以打開面板。在`{{ui:sandbox_tutorial_choose-mode_title}}`和`{{ui:sandbox_tutorial_done_title}}`步驟中，面板會自動開啟在`{{ui:sandbox_tab_tutorial}}`標籤頁上

被擊中或死亡只會重新開始發生時所在的步驟，而不是整個教程，並且這個步驟會變成紅色，直到完成為止。已完成的步驟是綠色的

點選列表中的步驟會開始該步驟，包括已經完成的步驟。完成一個步驟後，教程會轉到下一個未完成的步驟。只有完成所有步驟，教程才算完成，也是在那時寫入統計。同一標籤頁上的`{{ui:sandbox_tutorial_restart}}`可以隨時重新開始教程

> [!warning] 警告
> 在`{{ui:sandbox_tab_game}}`標籤頁上開啟`{{ui:sandbox_game_immortal}}`時，擊中完全不計入，所以`{{ui:sandbox_tutorial_dodge_title}}`和`{{ui:sandbox_tutorial_dash-through_title}}`步驟也看不到擊中。完成教程時請保留幾條生命

## 操作

模式針對當前正在操控的裝置更改，並立即儲存。體感沒有`{{ui:enum_control-mode_relative}}`模式。每種模式的含義：[[3_controls#操作模式]]

## 攻擊與遊戲

- `{{ui:sandbox_attacks_auto}}`以`{{ui:sandbox_attacks_gap}}`為間隔發射隨機波次，和主選單背景一樣
- `{{ui:sandbox_attacks_clear}}`移除螢幕上的所有攻擊
- `{{ui:sandbox_game_speed}}`只讓攻擊變慢或變快。化身始終以自己的速度移動
- 生命：`{{ui:sandbox_game_immortal}}`、1、3或5。生命耗盡後會恢復，沙盒不會結束
- `{{ui:sandbox_game_bot}}`把化身交給在主選單背景中游玩的同一個機器人
- `{{ui:sandbox_game_free-camera}}`讓你看到螢幕邊緣之外：用滑鼠中鍵或兩根手指移動檢視，用滾輪或雙指捏合縮放。藍色邊框顯示關卡相機看到的範圍，`{{ui:sandbox_camera_back}}`把檢視恢復到它。操作、衝刺和攻擊與不使用它時完全相同
- 死亡的表現和在關卡中一樣：攻擊減速並消失，化身以滿生命出現在中央
