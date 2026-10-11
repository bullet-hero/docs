---
title: 操作
date: 2026-10-02
tags: [player]
---

# 操作

可以用滑鼠、觸屏、手柄或體感遊玩。用滑鼠時，按住左鍵控制化身，Space、Shift或右鍵用來衝刺

輸入可以在操作設定中重新繫結，手柄按鍵不行

想一步步學習操作，或者不開關卡就試遍所有模式：[[13_sandbox]]

## 裝置

所有操作都在`{{ui:settings_common_title}}`→`{{ui:settings_controls_title}}`中設定，每種裝置一組

| 裝置 | 預設模式 | 移動 | 衝刺 |
|---|---|---|---|
| `{{ui:enum_control-device_keyboard-mouse}}` | `{{ui:enum_control-mode_absolute}}` | 按住左鍵，化身跟隨滑鼠 | `Space`、`Shift`、滑鼠右鍵或雙擊（0.3秒） |
| `{{ui:enum_control-device_touchscreen}}` | `{{ui:enum_control-mode_relative}}` | 在螢幕任意位置拖動手指 | 第二根手指 |
| `{{ui:enum_control-device_gamepad}}` | `{{ui:field_common_direction}}` | 任意一個搖桿 | 除`Start`和`Select`以外的任意按鍵 |
| `{{ui:enum_control-device_device-gyro}}` | `{{ui:field_common_direction}}` | 讓裝置偏離水平，傾斜20°時達到全速 | 點按螢幕任意位置 |

只用滑鼠就夠了：左鍵控制化身，`{{ui:settings_controls-keyboard-mouse_km-dash-button}}`用來衝刺。鍵盤不是必需的

在手柄上，`Start`用於暫停和繼續。手柄按鍵不能重新繫結：遊戲中除`Start`和`Select`以外的任意按鍵都會衝刺，包括正面右側的按鍵。在暫停選單中，正面右側的按鍵用作“返回”，和在任何選單中一樣

## 操作模式

| 模式 | 你的輸入代表什麼 |
|---|---|
| `{{ui:enum_control-mode_absolute}}` | 位置。游標跳到那裡，化身追上它 |
| `{{ui:enum_control-mode_relative}}` | 移動量。游標把它累加起來，化身追上游標 |
| `{{ui:field_common_direction}}` | 方向。完全沒有游標 |

在任何模式下移動都是即時的：沒有加速，也沒有滑行

在有游標的模式下，化身以自己的行走速度追趕游標。所以滑鼠移動很快時，化身會落在後面。衝刺朝游標進行。如果游標離得近，衝刺會更短，並正好停在游標上

鬆開控制按鍵或抬起手指之後會發生什麼，由一個核取方塊決定。滑鼠是`{{ui:settings_controls-keyboard-mouse_km-cursor-return}}`，觸屏是`{{ui:settings_controls-touchscreen_touch-cursor-return}}`：

- 開啟：化身停在原地，游標回到化身身上。滑鼠預設如此
- 關閉：游標留在你放開的位置，化身會走到那裡。只有受到傷害才能移動游標。觸屏預設如此

在`{{ui:field_common_direction}}`模式下，搖桿推到一半就是一半速度。衝刺總是衝滿全程

在觸屏的`{{ui:enum_control-mode_absolute}}`模式下，游標位於手指上方（`{{ui:settings_controls-touchscreen_touch-finger-offset-y}}`）。這樣手指不會擋住化身

一根手指控制化身時，第二根手指無論落在哪裡都會衝刺，落在面板或按鈕上也一樣。介面收不到這次觸控，所以衝刺永遠不會誤按任何東西

精確數字：[[6_avatar]]

## 體感

體感沒有校準。手機螢幕朝上平放時，化身保持不動

- 讓右邊緣向下傾斜，化身向右移動
- 讓上邊緣向下傾斜，化身向上移動
- `{{ui:settings_controls-device_sensitivity}}`為1時，傾斜20°達到全速。為2時，一半的傾斜角度就夠了

體感跟隨螢幕方向：把手機轉到橫屏再轉回來，右依然是右。體感有兩種模式：`{{ui:enum_control-mode_absolute}}`和`{{ui:field_common_direction}}`

## 重新繫結

- **遊戲輸入**在`{{ui:settings_controls_title}}`中：模式、`{{ui:settings_controls-keyboard-mouse_dash-keys}}`、`{{ui:settings_controls-keyboard-mouse_km-dash-button}}`、靈敏度、死區、平滑、反轉、螢幕搖桿和衝刺按鈕。`{{ui:settings_controls_reset}}`會把所有裝置恢復為當前平臺的預設值
- **快捷鍵**在`{{ui:settings_keybindings_label}}`中，幾乎都是編輯器用的。編輯器之外有`{{ui:settings_keybindings_window_toggle_fullscreen}}`（預設`F11`）、`{{ui:settings_keybindings_window_settings_save}}`（設定開啟時按`Ctrl+S`）和導航按鍵。`{{ui:settings_keybindings_reset}}`會撤銷所有重新繫結

遊戲等待按鍵時會顯示`請按下要繫結到“...”的按鍵`。之後的規則是`{{ui:settings_escape-cancels_backspace}}`

對於按鍵，遊戲只儲存你重新繫結過的部分。如果以後某個預設繫結變得更好，你也會得到它，除非你自己改過這個繫結。`{{ui:settings_controls_title}}`標籤頁會被完整儲存，所以它的新預設值不會影響你

編輯器的快捷鍵：[[3_speed-and-shortcuts]]

## 同時使用多個裝置

控制化身的只有一個裝置：你最後使用的那個。切換會自動發生，在同一幀內完成，不需要任何選單

遊戲每幀都會讀取所有已啟用的裝置。沒被碰過的手柄傳送的是零，這不算使用

第一幀時還沒有使用過任何裝置，所以由平臺決定：電腦上是滑鼠，手機上是觸屏

衝刺和暫停在任何已啟用的裝置上都有效，無論當前由哪個裝置控制。滑鼠控制化身時，手柄按鍵也能衝刺。單獨一次衝刺不會接管控制

一個裝置只有在以下情況下才能控制化身：

- 它被標記為啟用
- 平臺支援它
- 它此刻已連線

頂部的`{{ui:settings_controls-active_now}}`顯示當前由哪個裝置控制

> [!tip] 提示
> 某種操作方式好像沒有反應？通常是在它之後碰了另一個裝置。先看`{{ui:settings_controls-active_now}}`
