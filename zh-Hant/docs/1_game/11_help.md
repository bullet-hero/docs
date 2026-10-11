---
title: 幫助與錯誤報告
date: 2026-10-02
tags: [player, level_author]
---

# 幫助與錯誤報告

遊戲錯誤提交到releases的issues，問題發到Discord。附上設定中的版本字串，以及出現錯誤之前的操作步驟

先看看[[5_troubleshooting]]。關卡消失、“需要更新遊戲”和歸檔包被拒絕都在那裡有說明

## 發到哪裡

| 內容 | 位置 |
|---|---|
| 遊戲或編輯器的錯誤，對遊戲的建議 | [bullet-hero/releases](https://github.com/bullet-hero/releases/issues) |
| SDK或其程式碼中的錯誤 | [bullet-hero/sdk](https://github.com/bullet-hero/sdk/issues) |
| 文件中的錯誤或過時的事實 | [bullet-hero/docs](https://github.com/bullet-hero/docs)，[[community]] |
| 提問、關卡求助、討論 | [Discord](https://discord.gg/gkHQrp9NgS) |

GitHub上的訊息是公開的。任何人都可以閱讀並補充。可以向文件提交issue或pull request

不確定是不是錯誤？先在Discord裡問一下

專案的所有連結：[[links]]

## 錯誤報告裡寫什麼

能復現的錯誤會被修復。“它崩了”通常沒法修復：不知道該重複什麼

1. **版本字串**。點選設定介面上的版本字串，它會自動複製。格式如下：`gv X, sv Y, mg Z, <Platform>, <Channel>, <Debug|Release>`，[[4_settings]]
2. **平臺和裝置**：系統，如果是手機，還有型號
3. **步驟**：你做了什麼，期望發生什麼，實際發生了什麼
4. **關卡**，如果錯誤與它有關：打包成歸檔包的關卡資料夾，或你開啟過的歸檔包。如果關卡受保護，請註明
5. **錯誤報告**，如果出現過錯誤視窗。`{{ui:root_error_save}}`把它寫入`reports`資料夾，`{{ui:root_error_open-reports-folder}}`開啟該資料夾，[[1_installation]]

> [!tip] 提示
> 把檔案作為附件新增到訊息中，而不是貼上到正文裡。日誌很長，放在正文裡很難閱讀

## 日誌

遊戲執行時會寫日誌。完全沒有出現錯誤視窗時，它會有幫助

- **Windows**：遊戲資料資料夾中的`Player.log`，`C:\Users\<你>\AppData\LocalLow\vertoker\Bullet Hero`（Unity的標準位置）
- **Android**：日誌輸出到logcat。裝置連線到電腦時，用`adb logcat -s Unity`檢視
- **其他系統**：暫無說明
