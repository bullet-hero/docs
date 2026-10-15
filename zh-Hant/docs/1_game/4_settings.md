---
title: 設定
date: 2026-10-15
tags: [player]
---

# 設定

最重要的設定在第一次啟動時完成：遊戲會自動開啟快速設定，包括語言、音量、效能和效果。重置隻影響設定，關卡會保留

## 標籤頁

| 標籤頁 | 內容 |
|---|---|
| `{{ui:settings_general_title}}` | 語言，每種語言都用它自己的語言命名，如`Русский (ru)`。`系統 (zh)`跟隨裝置，並顯示最終使用的語言。還有同時載入的關卡檔案數量、網址檔案的超時時間、`{{ui:settings_general-open_folder}}` |
| `{{ui:field_common_audio}}` | 音量：`{{ui:settings_audio_volume}}`、`{{ui:settings_audio_game}}`、`{{ui:settings_audio_ui}}`、`{{ui:settings_audio_editor-ui}}`、`{{ui:settings_audio_editor-game}}` |
| `{{ui:settings_controls_title}}` | 裝置和操作方式，[[3_controls]] |
| `{{ui:settings_keybindings_label}}` | 快捷鍵，主要是編輯器的，[[3_speed-and-shortcuts]] |
| `{{ui:settings_graphics_title}}` | 顯示、幀率、抗鋸齒、`{{ui:settings_graphics-colliders-mode_title}}`、`{{ui:settings_graphics-performance_title}}` ([[17_performance-rating]])、紋理、特效、後期處理 |
| `{{ui:settings_interface_label}}` | 遊戲介面、`{{ui:settings_interface_open-menu-on-lose}}`、`{{ui:settings_interface_menu-background}}`、`{{ui:settings_interface_levels-layout}}`、螢幕方向、統計疊加層 |
| `{{ui:settings_game-editor_title}}` | 編輯器自己的設定，包括它自己的`{{ui:settings_interface_levels-layout}}` |
| `{{ui:settings_profile_tab}}` | 你的統計，[[10_statistics]] |
| `{{ui:settings_other_title}}` | 清理儲存空間、轉移檔案和Steam Cloud狀態（[[14_profile-transfer]]）、Android上的資料夾訪問許可權、匿名模式、`{{ui:settings_other_reset}}` |

`{{ui:settings_interface_menu-background}}`決定主選單按鈕後面顯示什麼：機器人躲避攻擊的即時競技場、一片旋轉的形狀，或者什麼都不顯示

`{{ui:settings_interface_levels-layout}}`決定關卡選擇以什麼方式開啟：封面組成的`{{ui:enum_level-browser-layout_grid}}`，或帶簡介的`{{ui:enum_level-browser-layout_list}}`。它有兩個：`{{ui:settings_interface_label}}`標籤頁中的用於選單（預設`{{ui:enum_level-browser-layout_grid}}`），`{{ui:settings_game-editor_title}}`標籤頁中的用於編輯器（預設`{{ui:enum_level-browser-layout_list}}`）。在你離開這個介面之前，搜尋框旁邊的按鈕仍然可以切換檢視

## 快速設定

`{{ui:settings_quick-setup_title}}`是`{{ui:settings_general_title}}`標籤頁中位於`{{ui:settings_general-open_folder}}`上方的按鈕。它會問幾個最重要的問題，每頁一個類別。第一次啟動時它會自動開啟，在教程邀請之前。每個選項都有一行說明它的作用。頁面可以按任意順序開啟，`{{ui:settings_quick-setup_next}}`只是提示下一頁

| 頁面 | 問題 | 選項 | 改變什麼 |
|---|---|---|---|
| `{{ui:settings_quick-setup_page-language}}` | `{{ui:settings_general_language}}` | `{{ui:settings_general_language_system}}`以及遊戲的每種語言，各自用本語言命名 | 與`{{ui:settings_general_title}}`標籤頁中的相同 |
| | `{{ui:settings_audio_volume}}` | 滑塊 | 與`{{ui:field_common_audio}}`標籤頁中的相同 |
| `{{ui:settings_graphics_title}}` | `{{ui:settings_quick-setup_performance}}` | `{{ui:settings_quick-setup_performance-minimum}}`、`{{ui:settings_quick-setup_performance-economy}}`、`{{ui:settings_quick-setup_performance-recommended}}`、`{{ui:settings_quick-setup_performance-max}}` | 渲染縮放（PC）、抗鋸齒、紋理尺寸、特效的幀率，但不包括幀率上限：任何選項都按螢幕重新整理率執行。`{{ui:settings_quick-setup_performance-minimum}}`還會關閉粒子特效和後期處理，並把影像限制在512以內 |
| | `{{ui:settings_quick-setup_comfort}}` | `{{ui:settings_quick-setup_comfort-full}}`、`{{ui:settings_quick-setup_comfort-soft}}`、`{{ui:settings_quick-setup_comfort-minimal}}` | 每種後期效果以及化身的碎裂。`{{ui:settings_quick-setup_comfort-soft}}`會關閉故障、顆粒、模糊、鏡頭畸變和色差 |
| `{{ui:settings_controls_title}}` | | `{{ui:settings_quick-setup_open-tutorial}}` | 這裡不改變任何東西：教程讓你試遍每種操作方案並選出自己的。它從主選單或沙盒開啟 |

標有`{{ui:settings_quick-setup_default-badge}}`的選項就是遊戲在你的裝置上開始時使用的設定。選擇會立即生效，並在完整設定中可見。如果你的設定與任何選項都不符，就不會高亮任何選項，並有一行文字說明。這是你自己的設定，按下任一選項會替換它們

## 摺疊的部分

較長的標籤頁被分成幾個部分。經常修改的部分是展開的，細節調整是摺疊的：點選標題即可展開。標籤頁重置按鈕旁邊的按鈕可以一次摺疊或展開所有部分

在`{{ui:settings_controls_title}}`標籤頁中，只有你手上正在用的裝置是展開的

## 重置

每個標籤頁都有自己的重置。`{{ui:settings_other_title}}`中的`{{ui:settings_other_reset}}`會一次重置所有標籤頁

重置隻影響設定。你的關卡會保留

## 版本行

設定介面上有一行版本資訊。點選它即可複製

它的格式是：`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`。報告錯誤時應該附上的就是這一行，[[11_help]]

## 圖形

**抗鋸齒**。PC上預設使用`{{ui:enum_anti-aliasing-type_msaa}}`。手機一開始不開抗鋸齒。遊戲中的所有形狀都是真正的幾何體，`{{ui:enum_anti-aliasing-type_msaa}}`在所有平臺上都能讓邊緣平整而不發糊

`{{ui:enum_anti-aliasing-type_fxaa}}`適用於效能較弱的手機。它對整個螢幕只做一次處理，開銷是固定的。當許多透明形狀疊在一起繪製時，`{{ui:enum_anti-aliasing-type_msaa}}`的開銷會增加

刻意沒有提供TAA。它會在快速移動的子彈後面留下拖影，它的抖動還會干擾故障效果

**幀率**。目標幀率是手動設定的，而不是通過垂直同步。這樣關卡的時間在60Hz和144Hz的螢幕上完全相同。開啟`{{ui:settings_graphics_vsync}}`時（僅PC），幀率上限不起作用

> [!tip] 建議
> 在效能較弱的裝置上，先把**渲染縮放**降到1以下。它只損失清晰度，介面仍保持完整尺寸。僅PC

更多：[[2_mobile-devices]]

## “僅碰撞體”模式

用於練習的模式，是`{{ui:settings_graphics_title}}`標籤頁中一個摺疊的部分。開啟`{{ui:settings_graphics-colliders-mode_active}}`後，遊玩中的關卡會把每個判定框畫成同一種顏色的平面填充，放在純色背景上，此外什麼都不畫。消失的有：形狀本身的外觀、沒有碰撞體的形狀、特效、文本、後期處理和主題背景。不變的有：音樂、碰撞、相機及其震動、檢查點、介面和統計，這種模式下的一局和其他任何一局一樣計入統計。你的化身照常繪製

這個模式只在遊玩關卡時生效。編輯器、沙盒和選單背景照常繪製

| 選項 | 作用 |
|---|---|
| `{{ui:settings_graphics-colliders-mode_use-alpha}}` | 開啟（預設）：填充按顏色的Alpha半透明顯示，重疊的障礙看起來更暗。Alpha不會低於0.15。關閉：每個填充都是實心的，顏色的Alpha被鎖定 |
| `{{ui:settings_graphics-colliders-mode_color}}` | 填充的顏色，預設是Alpha為0.6的紅色。編輯器中的碰撞體檢視使用同樣的色相，但有自己的不透明度 |
| `{{ui:settings_graphics-colliders-mode_background}}` | 填充後面繪製的顏色，預設是深灰色。不用黑色，是為了讓相機畫面的邊緣在周圍的黑邊前仍然可見 |

兩種顏色都摺疊在各自的標籤下：展開需要的那一個，就能看到色輪

## 匿名模式

在`{{ui:settings_other_title}}`→`{{ui:settings_other_suppress-game-saves}}`中開啟

開啟這個模式時，遊戲不儲存任何自己的資料。`settings.json`、總體統計和關卡統計在硬碟上保持原樣。修改過的設定在關閉遊戲之前仍然有效

關卡相關的操作照常儲存：儲存、匯出、匯入、複製和刪除。編輯器的自動儲存和備份也照常工作，它們有自己的開關

這個模式持續到關閉遊戲為止，不會被記住

關閉這個模式時，當前設定會被儲存。在此期間遊玩的一切都會被丟棄

> [!info] 須知
> 這個模式也會自動開啟。[[12_launch-arguments|啟動引數]]`--suppress-game-saves`會在整個執行期間開啟它，並且無法在遊戲中關閉。來自更新版本遊戲的設定或統計也會開啟它。這時遊戲會在每次啟動時詢問是保留它們，還是用預設值覆蓋
