---
title: 安裝
date: 2026-10-14
tags: [player]
---

# 安裝

遊戲把關卡、設定和統計儲存在同一個資料資料夾中。更新是安全的：新版本能讀取所有舊資料。在Android上，解除安裝遊戲也會清除關卡

在這裡下載：[[download]]

## 你的檔案在哪裡

| 系統 | 資料夾 |
|---|---|
| Windows | `C:\Users\<你>\AppData\LocalLow\vertoker\Bullet Hero` |
| Android | `/storage/emulated/0/Android/data/com.vertoker.BulletHero/files` |

最快的開啟方式是在遊戲中：`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general-open_folder}}`

裡面有什麼：

| 資料夾 | 內容 |
|---|---|
| `levels` | 你的關卡，每個關卡一個資料夾 |
| `backups` | 編輯器的自動儲存 |
| `stats` | 統計資料 |
| `settings.json` | 設定 |
| `reports` | 錯誤報告 |

## 解除安裝

在Windows、Linux和Mac上，免費版在遊戲旁邊附帶解除安裝程式：Windows上是`unins000.exe`，Linux上是`unins000`，Mac上是`Bullet Hero.app`旁邊的`unins000`。執行它，它會自動刪除遊戲，不會詢問任何問題。你的關卡、設定和統計資料留在資料資料夾中

它只刪除遊戲自身的檔案。你自己放進遊戲資料夾的東西會保留，資料夾只有在清空後才會被刪除。如果遊戲正在執行，解除安裝程式會先關閉它，就像點選視窗的關閉按鈕一樣，並同時關閉AI的MCP伺服器。關卡中未儲存的更改會丟失，所以請在解除安裝前先儲存關卡

用Windows安裝程式安裝的遊戲，像解除安裝其他程式一樣，在Windows設定的“應用”中解除安裝

商店版本由商店自己解除安裝

## 更新

新版本的遊戲能順利讀取所有舊資料，無論經過什麼更新、有什麼變化

舊版本不會開啟新版本的關卡。如果遊戲要求你更新，就更新

在 Google Play 版和 RuStore 版中，主選單會提示新的更新，並在後臺下載。更新就緒後，主選單會顯示 `{{ui:menu_update-ready_text}}`，點選 `{{ui:menu_update-ready_install-btn}}` 即可。通關一個關卡後，它可能會請你為遊戲評分

> [!caution] 注意
> 在Android上，解除安裝遊戲也會刪除你所有的關卡。解除安裝前請匯出檔案，[[14_profile-transfer]]
