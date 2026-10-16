---
title: 效能評分
date: 2026-10-17
tags: [player, level_author]
---

# 效能評分

開始遊玩之前，遊戲會用一個五格的指示條顯示關卡在你的裝置上執行起來有多吃力：亮起的格越多，關卡越輕鬆。綠色的格表示執行流暢，黃色表示吃緊，紅色表示幀率會下降

評分是一個數字，`{{v:performance.score-limit}}` 正好等於在你的目標幀率下一幀可用的時間。檔位由評分決定：

| 格數 | 檔位 | 評分 |
|---|---|---|
| 5 | `{{ui:level_performance_holds}}` | 低於 `{{v:performance.score-warning}}` |
| 4 | `{{ui:level_performance_tight}}` | 從 `{{v:performance.score-warning}}` 到 `{{v:performance.score-limit}}` |
| 3 | `{{ui:level_performance_drops}}` | 高於 `{{v:performance.score-limit}}`，最高到 `{{v:performance.score-heavy}}` |
| 2 | `{{ui:level_performance_severe-drops}}` | 高於 `{{v:performance.score-heavy}}`，最高到 `{{v:performance.score-severe}}` |
| 1 | `{{ui:level_performance_does-not-hold}}` | 高於 `{{v:performance.score-severe}}` |
| 無 | `{{ui:level_performance_unknown}}` | 關卡或裝置尚未測量 |

評分預測的是關卡最吃力的時刻，而不是平均情況。一個關卡輕鬆執行三分鐘、卡住一秒鐘，得到的就是那一秒的評分

## 在哪裡看到

- 關卡瀏覽器：每張關卡卡片上的指示條，以及篩選中的 `{{ui:root_level-filters_performance}}` 分組
- 選單中的關卡頁面：指示條、檔位和評分
- 關卡編輯器中關卡的後設資料：在你的裝置和參考裝置上的評分，以及關卡最吃力的時刻（時間戳）

## 評分的兩半

**關卡的一半**在每次儲存後的幾秒內由編輯器測量（你可以繼續工作），並存放在它的後設資料裡。如果在測量完成前離開編輯器，檔案保留上一次的測量。它描述關卡的需求：有多少物件存活、它們覆蓋了多少螢幕、運行了多少特效和後期處理通道。在此功能出現之前儲存的關卡沒有這條記錄，在再次儲存之前顯示為 `{{ui:level_performance_unknown}}`。編輯器在開啟關卡時會測量它，並保留結果直到離開編輯器，但不寫入檔案

**裝置的一半**說明你的裝置做這些事情的速度。在你測量裝置之前，遊戲使用你所在平臺的參考裝置。你的設定也會計入：渲染縮放、抗鋸齒、特效和後期處理都會改變評分，無需重新測量

## 測量你的裝置

1. 從主選單開啟 `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. 按下 `{{ui:settings_graphics-performance_measure}}`。一個視窗會說明哪些做法有助於測量：關閉其他應用和遊戲，將手機或筆記型電腦接上充電器，不要觸碰裝置
3. 按下 `{{ui:settings_graphics-performance_start}}`，最多等待 {{v:performance.benchmark-max-seconds}} 秒。設定介面會隱藏，遊戲播放測試關卡，並在上方兩角顯示正在測量的內容。不要切換到其他應用

`{{ui:settings_graphics-performance_stop}}` 可提前結束測量。被停止或超時的測量不會儲存任何內容，之前的結果保持不變

完成後，視窗會顯示結果：演示關卡在你的裝置上的指示條、你的裝置受什麼限制（處理器或圖形晶片）、推薦哪個 `{{ui:settings_quick-setup_performance}}` 預設，以及你的關卡在每個檔位各有多少個。`{{ui:settings_graphics-performance_again}}` 會再測量一次

如果測量不穩定（裝置過熱、其他應用佔用資源），遊戲仍會使用它，因為它比任何參考裝置都更接近你的裝置，視窗也會對此提示。關閉其他應用後重新測量，評分會更準確

## 換到另一臺裝置

測量結果屬於進行測量的那臺裝置。檔案轉移（[[14_profile-transfer]]）和雲存檔都不會帶上它，所以新裝置會從它的參考裝置開始，直到你重新測量
