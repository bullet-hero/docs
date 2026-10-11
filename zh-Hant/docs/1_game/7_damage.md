---
title: 傷害與生命
date: 2026-10-02
tags: [advanced_player]
---

# 傷害與生命

每次命中消耗一條命，把化身擊退{{v:avatar.knockback-time}}秒，並給予{{v:avatar.damage-timeout}}秒無敵時間。預設情況下，死亡會把關卡倒回到最後一個檢查點並恢復生命

## 命中的三個階段

1. **擊退，`{{v:avatar.knockback-time}}`秒**。你以每秒`{{v:avatar.knockback-speed}}`單位的速度被推離命中你的東西。這大約是{{v:avatar.knockback-distance}}單位，一整次衝刺，預設螢幕高度的四分之三。期間不接受輸入。無法用衝刺擺脫擊退：擊退優先於一切
2. **操控恢復**，在這{{v:avatar.knockback-time}}秒之後
3. **無法被命中**，從命中那一刻起整整`{{v:avatar.damage-timeout}}`秒。這一秒內的所有命中都會被忽略

如果你正好站在命中你的東西上，就沒有方向可推。這時你完全不會被擊退

出現期間（`{{v:avatar.spawn-time}}`秒）和衝刺保護的`{{v:avatar.dash-invulnerability}}`秒內你同樣無法被命中，[[6_avatar]]

> [!info] 須知
> 待在危險區域裡只消耗一條命，而不是十條。被推進第二個危險區域也能活下來。密集的彈幕看起來像是瞬間死亡，實際往往比一顆正好在保護秒結束時飛來的子彈代價更小

## 生命

生命數量在關卡畫面中選擇：`{{ui:menu_levelview_options-lifes_option-zen}}`、`{{ui:menu_levelview_options-lifes_option-one}}`、`{{ui:menu_levelview_options-lifes_option-three}}`或最多16條的`{{ui:menu_levelview_options-lifes_option-custom}}`，[[2_playing-levels]]

每次命中消耗一條命。拿走最後一條命的命中就是死亡

`{{ui:menu_levelview_options-lifes_option-zen}}`對命中的反應和其他任何一局都一樣：擊退、護盾圓環、粒子爆發和一秒保護照常生效，命中也計入統計。但它永遠不會消耗生命，所以這一局永遠不會結束

生命由化身周圍的圓點圓環顯示：亮著的點是剩餘的命，熄滅的是已消耗的

結果視窗顯示`{{ui:game_game-result_hits}}`和`{{ui:game_game-result_lives-left}}`

## 死亡會發生什麼

預設情況下，死亡不會結束這一局：

1. 關卡時鐘在現即時間`{{v:checkpoint.rewind-time}}`秒內平滑停下。音樂也隨之下沉
2. 關卡跳回到最後到達的檢查點。生命恢復
3. 時鐘在另外`{{v:checkpoint.rewind-time}}`秒內平滑加速回這一局的速度。加速期間你無法被命中，否則危險位置旁邊的檢查點會在第一秒內拿走全部生命

暫停也會停止這次加速

如果在關卡畫面中關閉了`檢查點`，就會倒回到關卡開頭

想讓死亡開啟結果視窗，請開啟`{{ui:settings_common_title}}`→`{{ui:settings_interface_label}}`→`{{ui:settings_interface_open-menu-on-lose}}`。這樣回放會停止

在該視窗中，`{{ui:game_game-result_restart-checkpoint}}`會從已到達的檢查點開始新的嘗試

## 檢查點

檢查點由關卡作者放置。是否計入由你通過`檢查點`開關決定

已到達的檢查點是關卡當前位置或之前的最後一個檢查點。所以回到它不會撤銷任何東西，只是倒回

作者可以讓檢查點恢復生命值。這樣經過它時會在一局中途恢復一次生命

螢幕底部的進度條在每個檢查點處有一個刻度。進度條在`{{ui:settings_interface_label}}`→`{{ui:settings_interface_show-game-progress}}`中開啟

有檢查點和沒有檢查點的記錄分開儲存，[[10_statistics]]

## 無碰撞

`{{ui:menu_levelview_options-no-collision_title}}`是獨立於`{{ui:menu_levelview_options-lifes_option-zen}}`的開關，在關卡畫面和編輯器的啟動面板中位於`檢查點`旁邊。開啟後化身會穿過一切：再也沒有東西能碰到它

`{{ui:menu_levelview_options-no-collision_title}}`的一局儲存自己的記錄，與`{{ui:menu_levelview_options-lifes_option-zen}}`和普通的局分開，結果視窗會在`{{ui:menu_levelview_options-lifes_title}}`的值後面加上`· 無碰撞`來標記它，[[10_statistics]]
