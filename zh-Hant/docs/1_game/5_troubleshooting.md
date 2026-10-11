---
title: 問題排查
date: 2026-10-03
tags: [player]
---

# 問題排查

手動複製的關卡在重新掃描後出現在列表中。來自更新版本的關卡需要更新遊戲，.7z歸檔包需要重新打包為zip。忘記的密碼無法找回。只有在Steam版本中、並且Discord正在執行時，Discord才會顯示你的活動

沒有找到你的問題？在哪裡報告：[[11_help]]

## 關卡不在列表中

- **手動複製的**。關卡資料夾必須直接放在`levels`中，[[1_installation]]。複製後點擊`{{ui:root_level-browser_refresh}}`
- **創意工坊物品**。Steam版本只顯示你的訂閱。`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general_show-all-found-content}}`會加入在硬碟上找到的資料夾。它們標有`{{ui:root_level-entry_not-listed}}`
- **什麼都看不到**。關卡資料夾可能無法訪問。此時`{{ui:settings_other_title}}`中的儲存清理不會執行，並提示`關卡掃描沒有找到任何內容，因此已拒絕此次清理`

## 關卡無法載入

載入畫面會顯示當前階段：`{{ui:root_loading_reading}}`、`{{ui:root_loading_validating}}`、`{{ui:root_loading_resources}}`、`{{ui:root_loading_building}}`

- **來自網路地址的檔案**。關卡可以通過連結獲取檔案，而不是把它放在資料夾裡。`{{ui:settings_general_title}}`→`{{ui:settings_general_resource-web-timeout}}`是遊戲等待這種檔案的秒數
- **損壞的關卡**。`Json`格式的關卡是文本，可以直接用眼睛讀。損壞的`Blob`會被整個拒絕。更多：[[4_level-folder-and-backups]]
- **錯誤視窗**。視窗中有`{{ui:root_error_copy}}`、`{{ui:root_error_save}}`和`{{ui:root_error_open-reports-folder}}`。報告儲存在`reports`資料夾中。把它附在[bullet-hero/releases](https://github.com/bullet-hero/releases/issues)的錯誤報告裡，[[11_help]]
- **`關卡每幀需要的物體數超過此裝置的上限`**。這不是載入錯誤。關卡可以遊玩，但其中一部分不會被繪製。更多：[[1_level-budget]]

## “需要更新”

舊版本的遊戲不會開啟來自新版本的檔案。請更新遊戲

| 訊息 | 怎麼辦 |
|---|---|
| `這個關卡由更新版本的遊戲製作，當前版本無法讀取...` | 更新遊戲 |
| `這個歸檔包中的關卡來自更新版本的遊戲...` | 更新遊戲 |
| `剪貼簿中的編輯器內容是在更新版本的遊戲中複製的...` | 更新遊戲 |
| `你的設定或統計由更新版本的遊戲儲存...` | `{{ui:root_update-required_download}}`、`{{ui:root_update-required_keep}}`或`{{ui:root_update-required_overwrite}}` |

標有`{{ui:root_level-entry_newer-version}}`或`{{ui:root_level-entry_newer-file}}`的卡片是同一種拒絕。在開啟關卡之前就能看到

### 來自更新版本的設定或統計

這種情況下游戲使用預設值執行。在關閉之前它不儲存任何自己的資料，新檔案保持不變。這就是匿名模式，[[4_settings]]

使用`--suppress-game-saves`時沒有`{{ui:root_update-required_overwrite}}`按鈕

來自更新版本的關卡統計不會顯示。通關該關卡會覆蓋它，除非存檔已被關閉

### 遊戲為什麼拒絕

檔案格式的每次變化都會獲得一個新的代號。版本不讀取更新代號的檔案，以免讀錯

## 受保護的關卡

開啟之前，遊戲會要求輸入`{{ui:level_passphrase_password}}`

每次會話只詢問一次密碼，並且只儲存在記憶體中

只有內容會被加密：物體、關鍵幀、主題。名稱、封面和媒體仍然可讀，所以沒有密碼也能看到卡片

刪除受保護的關卡不需要密碼

> [!caution] 注意
> 忘記的密碼無法找回。金鑰不存放在任何地方：不在遊戲中，不在檔案中，也不在任何人手裡

## 歸檔包被拒絕

| 訊息 | 原因 |
|---|---|
| `{{ui:editor_create-level_archive-unsupported}}` | 這是`.7z`。請重新打包為`.zip` |
| `{{ui:editor_create-level_archive-wrong-password}}` | 密碼不對 |
| `{{ui:editor_create-level_archive-damaged}}` | 歸檔包已損壞，請再要一次 |
| `{{ui:editor_create-level_archive-not-archive}}` | 這個檔案根本不是關卡歸檔包 |

改過名的歸檔包不是問題：遊戲根據檔案的位元組識別格式

接受哪些歸檔包：[[2_playing-levels]]

## Discord不顯示我在玩什麼

- **不是Steam版本。** 只有Steam版本會在Discord中顯示你的活動
- **Discord沒有執行。** 同一臺電腦上必須正在執行Discord桌面應用。在遊戲之後才啟動它？狀態會在下一次切換介面時出現
- **活動被隱藏。** 在Discord中：`使用者設定` -> `活動隱私` -> 分享檢測到的活動
- **自己的關卡沒有名稱。** 這是有意的：只有創意工坊關卡或遊戲自帶的關卡會顯示名稱，編輯器中的關卡永遠不會顯示名稱。原因見[[game-privacy-policy#Discord Rich Presence]]
