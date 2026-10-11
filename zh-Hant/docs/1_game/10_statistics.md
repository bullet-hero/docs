---
title: 統計
date: 2026-10-02
tags: [advanced_player]
---

# 統計

遊戲按每個關卡和整臺裝置統計嘗試次數、死亡次數、受擊次數和時間。所有資料都儲存在本地的stats資料夾中。每一組遊玩條件單獨記錄紀錄

## 兩個檔案

| 檔案 | 儲存什麼 |
|---|---|
| `stats/statistics.json` | 關於你的一切：涵蓋所有關卡和介面 |
| `stats/<LevelId>.json` | 你對某一個關卡做過的一切 |

檔案為JSON格式，時間為UTC。不會向任何地方傳送任何資料

`stats`資料夾位於遊戲資料夾中`levels`的旁邊，[[1_installation]]。它永遠不會位於關卡內部。這樣發給朋友的關卡不會帶著已通關的狀態到達。你的進度也能在刪除關卡並重新匯入後保留下來

## “檔案”標籤頁

`{{ui:settings_common_title}}`→`{{ui:settings_profile_tab}}`顯示裝置的共享檔案：

| 分割槽 | 行 |
|---|---|
| `{{ui:settings_profile_section-account}}` | `{{ui:settings_profile_first-played}}`、`{{ui:settings_profile_last-played}}`、`{{ui:settings_profile_launches}}`、`{{ui:settings_profile_app-time}}` |
| `{{ui:field_common_time}}` | `{{ui:settings_profile_menu-time}}`、`{{ui:settings_profile_game-time}}`、`{{ui:settings_profile_editor-time}}`、`{{ui:settings_profile_loading-time}}` |
| `{{ui:settings_profile_section-totals}}` | `{{ui:settings_profile_attempts}}`、`{{ui:settings_profile_clears}}`、`{{ui:settings_profile_deaths}}`、`{{ui:settings_profile_hits}}`、`{{ui:settings_profile_levels-played}}`、`{{ui:settings_profile_levels-cleared}}`、`{{ui:settings_profile_frames}}` |
| `{{ui:settings_profile_section-streaks}}` | `{{ui:settings_profile_streak-current}}`、`{{ui:settings_profile_streak-longest}}` |
| `{{ui:settings_profile_section-avatar}}` | `{{ui:settings_profile_dashes}}`、`{{ui:settings_profile_distance}}` |
| `{{ui:settings_profile_section-tutorial}}` | `{{ui:settings_profile_tutorial-completions}}`、`{{ui:settings_profile_tutorial-first}}`、`{{ui:settings_profile_tutorial-last}}`，只有完成[[13_sandbox|沙盒教程]]的所有步驟才算一次完成 |
| `{{ui:settings_profile_section-editor}}` | `{{ui:settings_profile_levels-created}}`、`{{ui:settings_profile_levels-deleted}}`、`{{ui:settings_profile_objects}}`、`{{ui:settings_profile_operations}}`、`{{ui:settings_profile_generators}}`、`{{ui:settings_profile_resources}}` |
| `{{ui:settings_profile_section-devices}}` | `{{ui:settings_profile_device-keyboard}}`、`{{ui:settings_profile_device-touch}}`、`{{ui:settings_profile_device-gamepad}}`、`{{ui:settings_profile_device-gyro}}` |

時間按真實秒數計算，而不是關卡時間。檢查點處的慢動作和半速遊玩，按實際經過的時長計入

裝置行顯示遊玩時由哪臺裝置操控化身。僅僅連線著的裝置不計入

## 按關卡

關卡檔案儲存：

- 你第一次和最近一次遊玩它的時間
- 在關卡中的真即時長和進入次數
- 嘗試次數（每次重開都是新的一次）、通關次數、死亡次數、受擊次數、衝刺次數
- 回到檢查點的次數和放棄的遊玩
- 到達過的最遠位置和首次通關
- 你在關卡中的哪裡死亡：按長度比例和按檢查點

## 紀錄

紀錄按遊玩條件記錄：生命、速度、檢查點開或關、碰撞開或關，以及機器人。速度精確到百分位，與介面上顯示的完全一致

禪（0條生命）依然統計受擊：每次碰撞都計入它的資料，免除的只有生命損失和遊玩結束

一次遊玩在以下情況下打破相同條件的紀錄，按順序比較：

1. 它走得更遠
2. 它受擊更少
3. 它結束時剩餘生命更多
4. 它使用的衝刺更少

紀錄還儲存這次遊玩的種子和當時的關卡版本。版本不屬於條件。因此關卡重做之前創下的紀錄依然可見，旁邊會顯示版本

**從編輯器開始的遊玩會被統計，但不創造紀錄**。它計入嘗試次數、死亡次數和受擊次數。它不產生紀錄、最佳進度和首次通關，因為那個關卡只存在於記憶體中

## 寫入、刪除、凍結

遊戲每30秒寫入一次統計。遊玩結束、切換介面和退出時也會立即寫入。崩潰最多損失30秒的資料

- **刪除**：`{{ui:settings_common_title}}`→`{{ui:settings_other_title}}`→`{{ui:settings_other_cache-title}}`。那裡有`{{ui:settings_other_cache-orphan-statistics}}`和`{{ui:settings_other_cache-all-statistics}}`
- **隨關卡刪除**：刪除關卡時會提供`{{ui:root_level-delete_statistics}}`
- **凍結**：匿名模式會停止一切寫入，直到關閉遊戲，[[4_settings]]
- **轉移到另一臺裝置**：匯出檔案並在那裡匯入。合併會保留每個計數中較大的值，[[14_profile-transfer]]

> [!warning] 警告
> 手動複製的關卡資料夾會保留關卡的ID。原件和副本共用同一個統計檔案
