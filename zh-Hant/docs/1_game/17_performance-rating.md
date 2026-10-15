---
title: 效能評分
date: 2026-10-15
tags: [player, level_author]
---

# 效能評分

開始遊玩之前，遊戲會顯示關卡在你的裝置上執行起來有多吃力。綠色表示執行流暢，黃色表示吃緊，紅色表示過重，幀率會下降

評分是一個數字，`{{v:performance.score-limit}}` 正好等於在你的目標幀率下一幀可用的時間。檔位由評分決定：

| 檔位 | 評分 |
|---|---|
| `{{ui:level_performance_holds}}` | 低於 `{{v:performance.score-warning}}` |
| `{{ui:level_performance_tight}}` | 從 `{{v:performance.score-warning}}` 到 `{{v:performance.score-limit}}` |
| `{{ui:level_performance_does-not-hold}}` | 高於 `{{v:performance.score-limit}}` |
| `{{ui:level_performance_unknown}}` | 關卡或裝置尚未測量 |

評分預測的是關卡最吃力的時刻，而不是平均情況。一個關卡輕鬆執行三分鐘、卡住一秒鐘，得到的就是那一秒的評分

## 在哪裡看到

- 關卡瀏覽器：每張關卡卡片上的彩色圓點，以及篩選中的 `{{ui:root_level-filters_performance}}` 分組
- 選單中的關卡頁面：檔位和評分
- 關卡編輯器中關卡的後設資料：在你的裝置和參考裝置上的評分，以及關卡最吃力的時刻（時間戳）

## 評分的兩半

**關卡的一半**在編輯器中儲存關卡時測量，並存放在它的後設資料裡。它描述關卡的需求：有多少物件存活、它們覆蓋了多少螢幕、運行了多少特效和後期處理通道。在此功能出現之前儲存的關卡沒有這條記錄，在再次儲存之前顯示為 `{{ui:level_performance_unknown}}`。編輯器在開啟關卡時會測量它，並保留結果直到關閉遊戲，但不寫入檔案

**裝置的一半**說明你的裝置做這些事情的速度。在你測量裝置之前，遊戲使用你所在平臺的參考裝置。你的設定也會計入：渲染縮放、抗鋸齒、特效和後期處理都會改變評分，無需重新測量

## 測量你的裝置

1. 從主選單開啟 `{{ui:settings_common_title}}` → `{{ui:settings_graphics_title}}` → `{{ui:settings_graphics-performance_title}}`
2. 按下 `{{ui:settings_graphics-performance_measure}}`
3. 等待幾分鐘。設定介面會隱藏，遊戲播放測試關卡。不要切換到其他應用

完成後，該部分會顯示你的裝置受什麼限制（處理器或圖形晶片），以及推薦哪個 `{{ui:settings_quick-setup_performance}}` 預設

如果測量不穩定（裝置過熱、其他應用佔用資源），遊戲會忽略它並繼續使用參考裝置。關閉其他應用後重新測量

## 換到另一臺裝置

測量結果屬於進行測量的那臺裝置。檔案轉移（[[14_profile-transfer]]）和雲存檔都不會帶上它，所以新裝置會從它的參考裝置開始，直到你重新測量
