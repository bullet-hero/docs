---
title: 匯出與保護
date: 2026-10-11
tags: [level_author]
---

# 匯出與保護

匯出會把關卡連同它用到的所有檔案，以資料夾或歸檔包的形式儲存到遊戲之外。密碼會在磁碟上加密關卡的內容，忘記的密碼無法找回

## 匯出關卡

匯出位於關卡設定的`{{ui:settings_level-settings_publication}}`標籤頁：去向選`{{ui:editor_share_archive}}`，模式在`{{ui:editor_share_format}}`中選擇，受保護的模式還要填`{{ui:editor_share_passphrase}}`。更多：[[17_publishing]]

歸檔包包含關卡、它的後設資料以及它用到的每個檔案。位於關卡資料夾之外的歌曲也會被複制進去。對它的引用會改為指向歸檔包中的副本

關卡的`ai`資料夾（AI助手在其中儲存它對關卡的筆記）也會被打包，除非在關卡後設資料中取消勾選了`{{ui:settings_level-settings_metadata-level-ai-share}}`。帶密碼的模式從不打包它：加密的關卡旁邊放著可讀的設計筆記，密碼就失去了意義。資料夾沒有打包時，報告會說明。更多：[[7_ai-assistant#ai資料夾]]

| `{{ui:editor_share_format}}` | 得到什麼 | 用什麼開啟 |
|---|---|---|
| `{{ui:settings_level-settings_export-mode_folder}}` | 與磁碟上關卡所在的資料夾相同。把它打包成zip就能傳送 | 不需要任何工具 |
| `{{ui:settings_level-settings_export-mode_folder-protected}}` | 同樣的資料夾，但關卡文件經過加密。後設資料、封面和媒體檔案仍然可讀，所以關卡瀏覽器依然能顯示它的卡片 | 關卡文件用gpg開啟 |
| `{{ui:settings_level-settings_export-mode_zip}}` | 一個檔案 | 在Windows資源管理器中雙擊，無需安裝任何軟體 |
| `{{ui:settings_level-settings_export-mode_targz}}` | 一個檔案 | 任何壓縮軟體 |
| `{{ui:settings_level-settings_export-mode_zip-encrypted}}` | 使用zip自帶AES-256加密的zip。這就是歸檔包密碼通常的含義 | 7-Zip或其他任何壓縮軟體，它會要求輸入密碼 |
| `{{ui:settings_level-settings_export-mode_zip-protected}}`、`{{ui:settings_level-settings_export-mode_targz-protected}}` | 同樣的歸檔包，外面再包一層`.gpg` | gpg |

帶密碼的選項都無法用Windows資源管理器開啟。這是使用密碼的代價

庫中的合集或單個資源也使用同樣五種歸檔包模式，包括帶密碼的模式。兩種資料夾模式僅限關卡。更多：[[17_publishing#壓縮包]]

> [!tip] 提示
> 任何無法帶走的內容（通過URL引用的資源、沒有被任何內容引用的檔案）都會在匯出後的報告中列出

> [!warning] 警告
> 密碼在傳輸過程中保護內容，也能防止隨手複製。它不是DRM：任何同時擁有檔案和密碼的人，始終都能開啟它

## 保護關卡

在磁碟上加密關卡的文件。開啟關卡時會要求輸入密碼

受保護的是**內容**：物體、關鍵幀、主題。後設資料、封面和媒體檔案仍然可讀。所以沒有密碼，關卡瀏覽器也能顯示關卡的卡片

每次會話只詢問一次密碼，且僅儲存在記憶體中。它從不寫入任何地方，所以自動儲存照常工作

要移除保護，請將欄位留空並按`{{ui:settings_level-settings_protect-apply}}`

> [!caution] 注意
> 忘記的密碼無法找回。任何地方都不會儲存金鑰，沒有密碼就無法開啟檔案
