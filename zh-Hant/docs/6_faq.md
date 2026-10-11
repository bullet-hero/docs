---
title: 常見問題
date: 2026-10-02
tags: [player, level_author]
---

# 常見問題

Bullet Hero是免費的節奏遊戲與彈幕射擊（bullet hell）混合體。不需要賬號，目前還沒有伺服器。關卡由玩家在內建編輯器中製作，以資料夾或歸檔包的形式互相傳遞

## 遊戲

### Bullet Hero是什麼？

節奏遊戲與*bullet hell*（彈幕射擊）的混合體。關卡就是音樂，加上隨音樂運動的形狀。你操控一個小方塊，它要一直活到曲目結束

Bullet Hero是作為這一型別的引擎來打造的。所以大部分關卡由玩家在內建編輯器中製作。更多：[[1_game/index]]

### 遊戲免費嗎？

是的。遊戲沒有內購、沒有廣告，也沒有付費內容。更多：[[1_licensing-basics]]

### 在哪裡獲取？

所有版本和商店：[[download]]

遊戲已正式釋出，版本`gv {{v:version.gv}}`。構建版本沒有數字簽名

### 需要賬號或聯網嗎？

不需要。沒有賬號，也沒有伺服器，遊戲不會向任何地方傳送任何資料

只有一種關卡需要聯網：從作者的網址載入檔案的關卡。更多：[[1_installation]]

### 關卡儲存在哪裡？

儲存在遊戲資料資料夾中的`levels`資料夾裡。開啟方式：`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general-open_folder}}`。更多：[[1_installation]]

## 遊玩關卡

### 怎麼玩別人發給你的關卡？

把資料夾放進`levels`，然後在關卡列表中按`{{ui:root_level-browser_refresh}}`。歸檔包（`.zip`、`.tar.gz`）要在編輯器中用`{{ui:gen_level_archive}}`生成器開啟。更多：[[2_playing-levels]]

### 遊戲提示關卡來自更新的版本，怎麼辦？

更新遊戲。舊版本不會開啟新版本的檔案，以免讀錯。更多：[[5_troubleshooting]]

### 忘記的關卡密碼能找回嗎？

不能。金鑰不儲存在任何地方：遊戲裡沒有，檔案裡沒有，任何人手裡也沒有。更多：[[5_troubleshooting]]

### 遊戲能自己通關嗎？

可以，用關卡介面上的`{{ui:menu_levelview_options-bot}}`條件：`{{ui:enum_bot-kind_reflex}}`或`{{ui:enum_bot-kind_warm}}`。機器人的操作方式和你一樣，它也可能失敗。更多：[[9_bots]]

## 製作關卡

### 怎麼做第一個關卡？

主選單中的`{{ui:menu_main_editor-btn}}`，然後是`{{ui:settings_editor-settings_editor-settings}}`，再然後是`{{ui:settings_editor-settings_create-level}}`。把曲目複製到關卡資料夾，設定速度（bpm），放一個帶兩個關鍵幀的物體，然後開始試玩。更多：[[2_first-level]]

### 支援哪些音樂檔案？

`ogg`、`mp3`和`wav`，沒有別的。`flac`、`aiff`和tracker模組音樂都無法載入

`ogg`是最好的選擇。它比`wav`小8到10倍，而且不像`mp3`那樣會在開頭加入靜音。更多：[[2_preparing-the-track]]

### 可以用任何歌曲嗎？

在你自己的硬碟上不會做任何檢查。只有把關卡提交給某個服務時，音樂的許可證才重要，而這樣的服務目前還不存在。更多：[[1_licensing-basics]]

### 怎麼分享關卡？

手動分享，以資料夾或歸檔包的形式。Steam版本還可以把關卡釋出到Steam創意工坊。目前還沒有官方伺服器。更多：[[6_sharing-by-hand]]，[[17_publishing]]

## 專案

### 有線上排行榜或關卡目錄嗎？

還沒有。官方伺服器和社群伺服器正在開發中。更多：[[4_server/index]]

### 為什麼遊戲的程式碼不開源？

我有個人原因。等到開發徹底停止時，所有倉庫都會開源，[bullet-hero](https://github.com/bullet-hero)組織也可能交給其他人

SDK、文件和未來的伺服器現在就是開源的。更多：[[index]]

### 發現了bug？

遊戲的bug請提交到[bullet-hero/releases](https://github.com/bullet-hero/releases/issues)。有問題請到[Discord](https://discord.gg/gkHQrp9NgS)提問。去哪裡寫、要附上什麼：[[11_help]]

專案的所有連結：[[links]]
