---
title: 安裝
date: 2026-10-02
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

## 更新

新版本的遊戲能順利讀取所有舊資料，無論經過什麼更新、有什麼變化

舊版本不會開啟新版本的關卡。如果遊戲要求你更新，就更新

> [!caution] 注意
> 在Android上，解除安裝遊戲也會刪除你所有的關卡。解除安裝前請匯出檔案，[[14_profile-transfer]]
