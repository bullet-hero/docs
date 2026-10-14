---
title: 轉移檔案
date: 2026-10-14
tags: [player]
---

# 轉移檔案

整個檔案可以放進一個zip檔案：關卡、統計、設定和庫。重灌或換裝置前先匯出，再到新裝置上匯入

按鈕位於`{{ui:settings_common_title}}` → `{{ui:settings_other_title}}` → `{{ui:settings_profile-transfer_title}}`。支援Windows、Mac、Linux和Android。iOS不可用

## 檔案裡有什麼

| 部分 | 在資料資料夾中 | 預設勾選 |
|---|---|---|
| `{{ui:settings_profile-transfer_category-levels}}` | `levels` | 是 |
| `{{ui:settings_profile-transfer_category-statistics}}` | `stats` | 是 |
| `{{ui:settings_profile-transfer_category-settings}}` | `settings.json` | 是 |
| `{{ui:settings_profile-transfer_category-library}}` | `resources` | 是 |
| `{{ui:settings_profile-transfer_category-skins}}` | `skins` | 是 |
| `{{ui:settings_profile-transfer_category-backups}}` | `backups` | 否 |
| `{{ui:settings_profile-transfer_category-reports}}` | `reports` | 否 |
| `{{ui:settings_profile-transfer_category-recordings}}` | `recordings` | 否 |

這個檔案是普通的zip，任何解壓工具都能開啟。裡面是和資料資料夾（[[1_installation]]）相同的資料夾，外加描述檔案的`profile.json`

## 匯出

1. 點選`{{ui:settings_profile-transfer_export}}`
2. 勾選需要的部分
3. 選擇儲存位置

在任何能開啟設定的地方都可以匯出：主選單、遊玩暫停時和編輯器中。統計會先寫入磁碟，所以檔案是最新的

## 匯入

1. 從主選單開啟設定，點選`{{ui:settings_profile-transfer_import}}`
2. 選擇zip檔案
3. 勾選部分並選擇模式
4. 確認

只能在主選單中匯入。正在執行的關卡或開啟的編輯器佔用著自己的檔案，無法在使用中替換

| 模式 | 會發生什麼 |
|---|---|
| `{{ui:settings_profile-transfer_mode-replace}}` | 每個勾選的部分會被清空，並用檔案中的內容填充 |
| `{{ui:settings_profile-transfer_mode-merge}}` | 關卡會被新增。兩邊都有的關卡整體替換為較新的副本。統計保留每個計數中較大的值和更好的記錄。庫檔案、自動儲存和報告只會新增，你的保持不變 |

每次匯入在寫入前都會再確認一次。替換會列出將被清空的部分，合併會說明將新增、替換和保留多少關卡

**來自另一類裝置的設定。**在電腦上匯入來自手機的檔案（或反過來）時，會保留你自己的操作和畫面設定，其餘都取自檔案

遊戲會拒絕來自更新版本遊戲的檔案，請先更新遊戲。也會拒絕不是zip的檔案、不是檔案的zip、有密碼的zip以及損壞的檔案。這些情況下都不會有任何改動

## 備份

每次匯入前，遊戲會把即將被替換的部分儲存到一個備份中。它位於資料資料夾裡的`profile-backups`資料夾。備份只有一個：下一次匯入會覆蓋它

- `{{ui:settings_profile-transfer_backup-restore}}`會恢復備份。被它替換的內容會成為新的備份，所以恢復也可以撤銷
- `{{ui:settings_profile-transfer_backup-save-as}}`會把副本儲存到你選擇的位置
- `{{ui:settings_profile-transfer_backup-delete}}`會刪除它
- `{{ui:settings_profile-transfer_clear-cache}}`會刪除整個`profile-backups`資料夾：備份以及中斷的轉移留下的檔案

匯入時`{{ui:settings_profile-transfer_backup-to-folder}}`預設勾選：遊戲會立即詢問在遊戲外儲存副本的位置

> [!caution] 注意
> 在Android上，備份位於遊戲的資料資料夾中，會隨遊戲一起被刪除。解除安裝前請匯出檔案，或把備份儲存到別處

如果遊戲在匯入中途關閉，下次啟動時檔案會恢復原狀

## Steam Cloud

Steam版中，檔案會自動跟隨你的Steam賬戶。沒有按鈕：遊戲在啟動時同步一次，遊玩時上傳有變化的內容，關閉時再同步最後一次

開關屬於Steam：就是Steam中游戲屬性裡的Steam Cloud核取方塊。它是否開啟、上次同步是什麼時候，顯示在`{{ui:settings_common_title}}`→`{{ui:settings_other_title}}`→`{{ui:settings_cloud_title}}`中

| 部分 | 兩臺裝置都改過它時 |
|---|---|
| `{{ui:settings_profile-transfer_category-statistics}}` | 每個計數器保留較大的值和更好的紀錄，什麼都不會丟失 |
| `{{ui:settings_profile-transfer_category-settings}}` | 較新的副本獲勝。`{{ui:settings_graphics_title}}`和`{{ui:settings_controls_title}}`在每臺裝置上始終保持各自的設定 |
| `{{ui:settings_profile-transfer_category-levels}}` | 關卡較新的副本整體獲勝。另一份會進入落敗裝置上的編輯器備份 |
| `{{ui:settings_profile-transfer_category-library}}` | 每個檔案較新的副本獲勝 |
| `{{ui:settings_profile-transfer_category-skins}}` | 每個檔案較新的副本獲勝 |

- 在一臺裝置上刪除的關卡，在其他裝置上也會被刪除。每臺裝置都會把它的最後狀態儲存在編輯器備份中
- 在一臺裝置上刪除的統計，在其他裝置上也會被刪除。如果另一臺裝置在上次同步後玩過，它的進度會保留
- 超出Steam留給遊戲的空間的關卡，只會留在它所在的裝置上
- `{{ui:settings_profile-transfer_category-backups}}`、`{{ui:settings_profile-transfer_category-reports}}`和`{{ui:settings_profile-transfer_category-recordings}}`不會同步
- 由更新版本的遊戲寫入的雲端副本，在這臺裝置上的遊戲更新之前不會被改動
- 編輯器中開啟的關卡不會被替換，它會在下次啟動時同步
- 開啟`{{ui:settings_other_suppress-game-saves}}`時，什麼都不會同步

## 在Android上切換版本

從檔案安裝的遊戲（itch.io等）無法通過Google Play更新，反之亦然。兩個版本的簽名不同，所以Android會拒絕更新。切換步驟：

1. 匯出檔案並把檔案儲存到遊戲之外
2. 解除安裝遊戲
3. 安裝另一個版本
4. 匯入檔案
