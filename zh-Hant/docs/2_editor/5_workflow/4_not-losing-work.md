---
title: 避免丟失工作
date: 2026-10-02
tags: [level_author]
---

# 避免丟失工作

保護工作的是自動儲存、撤銷和關卡資料夾的副本。只有資料夾的副本才是關卡的完整快照。更改檔案格式和刪除關卡無法撤銷

每一種保護都覆蓋了其他保護覆蓋不到的部分。自動儲存和撤銷不能代替資料夾的副本，因為整個關卡就是一個資料夾

## 習慣

> [!tip] 建議
> 每完成一段就按`Ctrl+S`。每次重組之前複製一份關卡資料夾。在認定關卡完成之前執行`{{ui:settings_level-settings_rules}}`檢查

## 自動儲存

自動儲存預設開啟，工作方式如下：
1. 出現未儲存的修改時，開始`60`秒倒計時
2. 遊戲把關卡的一份副本寫入遊戲資料夾中的`backups/<level id>/`，它位於`levels`之外
3. 然後像按`Ctrl+S`一樣儲存關卡本身

開啟編輯器但沒有任何改動時，不會寫入任何東西。自上次儲存（你的或自動的）以來改動的一切都只存在於記憶體中

保留`25`份副本，最舊的最先刪除。副本只包含關卡檔案，不含後設資料、音軌和圖片。關卡被刪除後副本仍然存在，除非你勾選了`{{ui:root_level-delete_backups}}`。受保護關卡的副本用該關卡自己的密碼鎖定

開關、間隔和副本數量在`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}`中設定

**恢復**：關卡設定的`{{ui:settings_level-settings_dangerous-zone}}`標籤頁，`{{ui:level_backups_open}}`。副本按從新到舊排列，每份以建立時刻命名。當前檔案會先被複制到`backups`中，所以恢復也可以回退

也可以手動恢復：把備份複製到關卡資料夾中，命名為`level.json`（或`level.blob`）

## 未儲存的修改

會替換當前開啟的關卡或離開它的操作，會先詢問如何處理未儲存的修改：
- 從關卡列表開啟另一個關卡，包括複製關卡並開啟副本
- 建立關卡
- 在編輯器設定和關卡設定中點選`{{ui:settings_level-settings_quit}}`
- `{{ui:level_backups_open}}`
- 在`{{ui:settings_level-settings_dangerous-zone}}`中：複製關卡並開啟副本、更改檔案格式、設定密碼

對話方塊有三個選項：
- `{{ui:editor_save_text}}`：儲存關卡並繼續執行操作
- `{{ui:editor_unsaved-changes_discard}}`：紅色按鈕，唯一會丟失修改的選項
- `{{ui:editor_cancel_text}}`：什麼也不做

從關卡設定中啟動遊玩也會詢問，但只有兩個選項：`{{ui:editor_unsaved-changes_save-play}}`和`{{ui:editor_cancel_text}}`。這裡不能丟棄修改，因為從遊戲返回時會重新從磁碟讀取關卡。沒有未儲存的內容時，對話方塊不會出現

## 撤銷能覆蓋什麼

撤銷覆蓋對關卡的修改，也只覆蓋這些。對物體、關鍵幀、資源、主題、預製件和設定的任何更改都經過同一個操作緩衝區

不改變關卡的內容不會被撤銷：
- 選中的控制柄、時間軸工具，吸附和網格是否開啟
- 面板佈局、開啟的標籤頁、播放頭的位置
- 剪貼簿
- 重新生成的會話種子。重新載入關卡時會再次選取
- **儲存**。撤銷回退的是記憶體中的關卡，而不是磁碟上的檔案

## 完全無法撤銷的操作

有兩個操作會直接寫入磁碟：
- **更改關卡的檔案格式**。把關卡寫成`Blob`會刪除原來的`Json`。而`Blob`無法用肉眼閱讀或修復
- **刪除關卡**。所以它被藏在`{{ui:settings_level-settings_dangerous-zone}}`裡

## 原始資料標籤頁

`{{ui:settings_level-settings_raw}}`標籤頁把整個儲存檔案顯示為一棵欄位樹。它不做任何檢查：沒有規則，沒有限制

這是最後的手段。一次會話中的所有修改作為一次操作應用，這次操作可以撤銷

> [!caution] 注意
> 你在`{{ui:settings_level-settings_raw}}`標籤頁中寫入的內容沒有經過任何檢查。手邊要留一份關卡資料夾的副本。更多：[[4_level-folder-and-backups#備份與恢復]]

## 規則

值得執行的檢查是`{{ui:settings_level-settings_rules}}`標籤頁。它顯示校驗發現的問題：失效的引用、重複的ID、父級迴圈、巢狀過深的預製件、重疊的節拍段

遊戲能修復其中一部分問題：逐個修復，或用`{{ui:settings_level-settings_rules-fix-all}}`按鈕一次修復全部。修復通過`{{ui:editor_save_text}}`按鈕應用，作為一次可撤銷的操作。`{{ui:settings_level-settings_raw-discard}}`會丟棄這些修復。圖結構類的問題沒有修復方法

子物體的時段超出父級並不算錯誤。這是正常資料，行為符合設計。要適配生命週期，請執行`{{ui:mod_span_fit}}`修改器

接下來：[[4_level-folder-and-backups|關卡資料夾與備份]]、[[1_order-of-work|工作順序]]
