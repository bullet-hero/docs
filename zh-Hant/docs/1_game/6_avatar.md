---
title: 化身與移動
date: 2026-10-14
tags: [advanced_player]
---

# 化身與移動

化身以每秒{{v:avatar.move-speed}}單位的速度行走，衝刺在{{v:avatar.dash-time}}秒內把它送出{{v:avatar.dash-distance}}單位。判定框是半徑{{v:avatar.hitbox-radius}}單位的圓，比繪製出來的{{v:avatar.body-size}}單位方塊小

本頁是化身的事實標準。遊戲和兩個機器人都按這些數值製作，SDK把它們記錄為`AvatarRules`常量。與本頁不一致的程式碼就是程式碼的錯誤

距離以世界單位表示。預設相機正好{{v:camera.default-height}}單位高（`ValueRules.DefaultZoom`），所以一個單位是螢幕高度的十分之一，化身的身體寬半個單位

相機縮放改變的是你能看到多少，而不是下面的數值

## 數值

| 專案 | 數值 | 通俗地說 |
|---|---|---|
| 行走速度 | `{{v:avatar.move-speed}}`單位/秒 | 三分之二秒從螢幕頂端走到底端 |
| 衝刺速度 | `{{v:avatar.dash-speed}}`單位/秒 | 比行走快{{v:avatar.dash-to-walk-ratio}}倍 |
| 衝刺時長 | `{{v:avatar.dash-time}}`秒 | |
| 衝刺距離 | `{{v:avatar.dash-distance}}`單位 | 速度×時長，螢幕高度的四分之三 |
| 衝刺冷卻 | `{{v:avatar.dash-cooldown}}`秒 | 從衝刺開始時計算 |
| 衝刺無敵時間 | `{{v:avatar.dash-invulnerability}}`秒 | 同樣從開始時計算，所以比移動本身多持續{{v:avatar.dash-invulnerability-margin}}秒 |
| 最短衝刺 | `{{v:avatar.arrival-distance}}`單位 | 與到達距離相同，再近你就已經站在目標上了 |
| 擊退速度 | `{{v:avatar.knockback-speed}}`單位/秒 | 比行走快{{v:avatar.knockback-to-walk-ratio}}倍，[[7_damage]] |
| 擊退時長 | `{{v:avatar.knockback-time}}`秒 | 期間無法操控 |
| 傷害間隔 | `{{v:avatar.damage-timeout}}`秒 | 其間之後的所有命中都會被忽略 |
| 身體尺寸 | `{{v:avatar.body-size}}`單位 | 繪製出來的方塊 |
| 判定框 | 半徑`{{v:avatar.hitbox-radius}}`單位 | 身體的{{v:avatar.hitbox-scale}}，故意比看到的小 |
| 出現與消失 | `{{v:avatar.spawn-time}}`秒 | 長大出現，縮成一點消失 |
| 玩家尺寸對速度的影響 | 完全，`{{v:avatar.size-speed-influence}}` | 更大的化身按比例移動得更快。這是關卡中的玩家尺寸軌道，不是相機縮放 |
| 轉向速度 | `{{v:avatar.turn-speed}}`/秒 | 外觀效果：身體朝向哪裡 |
| 到達距離 | `{{v:avatar.arrival-distance}}`單位 | 離游標比這更近就算站在游標上 |

由它們推匯出的數值，真正決定閃避的是這些：

| 專案 | 數值 |
|---|---|
| 最短衝刺：距離 | `{{v:avatar.arrival-distance}}`單位 |
| 最短衝刺：時長 | 遠短於一幀 |
| 最短衝刺：冷卻和無敵時間 | 各自都遠短於一幀 |
| 最頻繁的衝刺 | 最多每隔一幀一次 |
| 擊退距離 | `{{v:avatar.knockback-distance}}`單位 |

被命中時會發生什麼：[[7_damage]]

## 移動

操控方式有兩種，遊戲從不把它們混在一起：
- **方向**：WASD、手柄搖桿、陀螺儀。化身朝你推的方向以行走速度移動。搖桿推到一半就是一半速度，沒有別的“慢走”
- **游標**：滑鼠或手指。化身追趕這個點，而不是瞬移過去。它以自己的行走速度移動，會落後於快速移動的滑鼠

兩種方式下移動都是即時的：沒有加速、滑行和慣性。你停止操作的那一幀就會停下

## 衝刺

無敵時間比移動多持續{{v:avatar.dash-invulnerability-margin}}秒。正是落地後的這段餘量讓你能衝刺*穿過*障礙物

衝刺期間由你控制方向。衝刺朝你要求的方向前進：沿著按住的方向，或者朝瞄準點，並且可以在衝刺途中改變。沒有按住方向的衝刺不會移動

使用游標時，衝刺朝你指向的地方前進並停在那裡：

| 與游標的距離 | 會發生什麼 |
|---|---|
| 超過{{v:avatar.dash-distance}}單位 | 朝它完整衝刺。你會停在游標之前 |
| {{v:avatar.arrival-distance}}到{{v:avatar.dash-distance}}單位 | 縮短的衝刺，正好結束在游標上 |
| 小於{{v:avatar.arrival-distance}}單位 | 不衝刺 |

縮短的衝刺就是縮小比例的同一個衝刺。路程、無敵時間和冷卻一起縮小：短一半的衝刺保護時間少一半，冷卻也快一倍。它不會更划算。兩次半程衝刺的代價正好等於一次完整衝刺，走過的距離也相同

沒有發生的衝刺沒有任何代價：冷卻不會開始，也不消耗任何東西。使用方向操控卻什麼都沒按的玩家得到同樣的結果：不衝刺

衝刺時身體變成更深的藍色，之後在{{v:avatar.dash-tint-fade}}秒內恢復正常顏色。沒有別的東西會改變身體顏色，被命中也不會。衝刺是你自己的動作，所以只有它會改變顏色

衝刺拖尾和這種藍色取決於衝刺長度：完整衝刺完全顯示，最短的衝刺顯示`{{v:avatar.dash-effect-min}}`，介於兩者之間的按比例顯示。短衝刺的粒子飛得更慢，所以拖尾看起來正好和衝刺一樣長

### 兩種風格，同一份預算

- 在`{{ui:field_common_direction}}`模式下，衝刺總是走滿{{v:avatar.dash-distance}}單位。距離可靠，無需瞄準，但也無法中途停下
- 使用游標時由你選擇長度，可以正好停在某一點。短衝刺意味著更短的保護，以及每次衝刺多一個可被命中的幀。指向遠處，完整衝刺就會回來

沿直線移動時，兩者在相同時間內走過相同距離。哪種風格都不更強：一種提供精確，另一種提供簡單

### 連續衝刺

**按住衝刺不等於無敵**。冷卻和保護時長相同，所以按住按鍵會產生連續不斷的衝刺鏈。但兩次衝刺之間總有正好一幀可以被命中，任何幀率下都是如此，慢手機和快電腦一樣

最密集的衝刺鏈是最多每隔一幀衝刺一次

## 判定框

化身上的圓點圓環正好沿著判定框繪製。子彈擦過輪廓卻什麼也沒發生？這是有意為之

當你處於無敵狀態時（衝刺中或剛被命中之後），完全沒有判定框

同一個圓環也顯示生命：亮著的點是一條剩餘的命

圓環的明顯程度由`{{ui:settings_common_title}}`→`{{ui:settings_interface_label}}`→`{{ui:settings_interface_hitbox-ring-opacity}}`決定。`0`會隱藏它，但關卡是按能看到圓環的玩家來平衡的

身體是由{{v:avatar.grid-cells}}個方塊組成的{{v:avatar.grid-side}}×{{v:avatar.grid-side}}網格。失去生命值時，方塊從邊緣到中心不是消失而是變暗：失去的方塊留作淡淡的殘影，所以網格總是顯示全部{{v:avatar.grid-cells}}個，生命值通過仍亮著的方塊數量來讀取

這是經典皮膚的樣子。皮膚可以改變網格、每個格子的形狀和顏色 - [[16_skins]]

殘影方塊足夠透明，可以透過它們看到身體下方的判定框圓環

生命值為零時正好亮著一個方塊，也就是最後一個

任何生命值的減少都在`{{v:avatar.health-loss-time}}`秒內顯示，任何恢復都在`{{v:avatar.health-gain-time}}`秒內顯示，不論涉及多少條命

如果關閉`{{ui:settings_graphics_title}}`→`{{ui:settings_graphics_avatar-render}}`，身體會變成一個會變暗的方塊。這是為效能較弱的裝置準備的

## 出現與消失

化身在`{{v:avatar.spawn-time}}`秒內在關卡中長大出現，死亡時在`{{v:avatar.spawn-time}}`秒內縮成一點。兩種情況下它都不響應輸入，出現期間也無法被命中

## 縮放

關卡可以用自己的軌道為化身的尺寸和速度製作動畫。它還可以暫時收回操控，或關閉碰撞

- 行走、衝刺和擊退的速度乘以同一個數。所以在一半速度下，衝刺也短一半（{{v:avatar.half-speed-dash-distance}}單位）
- 更大的化身按比例移動得更快，因為它的閃避也變大了。這裡的尺寸是化身自己的尺寸，來自玩家尺寸軌道。相機縮放不改變速度、距離和時間視窗：不論相機怎樣，化身都每秒移動{{v:avatar.move-speed}}單位
- 判定框是繪製身體的一部分，所以隨化身一起變大變小
- 衝刺瞄準使用當前的距離，而不是表中的{{v:avatar.dash-distance}}。在一半速度的關卡中，{{v:avatar.half-speed-dash-distance}}單位外的游標就已經要求完整衝刺，{{v:avatar.arrival-distance}}單位的閾值變成{{v:avatar.half-speed-arrival-distance}}，因為高於它的衝刺也短了一半
- 以秒計的時間視窗不縮放：冷卻、無敵時間、傷害間隔、出現。只有衝刺本身的長度會縮放它自己的兩個時間視窗

機器人遵循同樣的規則，[[9_bots]]
