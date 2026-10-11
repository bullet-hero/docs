---
title: 主題
date: 2026-10-02
tags: [level_author]
---

# 主題

主題是由64種顏色組成的調色盤，物體按槽位編號引用這些顏色。更換主題，所有引用它的內容都會隨之改變

型別為`主題`的顏色不儲存自己的顏色，只儲存一個槽位編號。它取當前幀上活動主題中該槽位的顏色

為什麼這比手動輸入的顏色更好，以及如何讓關卡在任何主題下都保持可讀：[[5_color-and-postprocessing]]

## 主題包含什麼

- **名稱**：顯示在列表和選擇視窗中
- **ID**，即`ThemeId`。主題關鍵幀按這個ID引用主題，而不是按名稱
- **64種顏色**，排成8×8的網格，每種顏色都帶透明度
- 每個槽位的**槽位名稱**，可選。在你給任何一個槽位命名之前，檔案中儲存的是`null`而不是名稱列表

主題是`level.json`中的資料，而不是關卡資料夾中的單獨檔案（見[[1_level-needs]]）。一個關卡可以包含任意數量的主題

遊戲不給槽位分配任何固定用途：遊戲自帶的`Balanced`主題只是把它的64種顏色按色相分組

## 顏色如何找到自己的值

分兩步：
1. 事件時間軸上的`主題`軌道決定這一幀哪個主題處於活動狀態
2. 型別為`主題`的顏色指定活動主題中0到63之間的一個槽位

可以引用主題的有，例如形狀的顏色（每個角單獨設定）、文本的顏色和關卡背景

**槽位的位置就是它的身份**。把一種顏色移到另一個槽位，所有引用舊槽位的內容都會被重新著色

## 隨時間切換主題

在兩個主題關鍵幀之間，遊戲會把整個調色盤從一個主題平滑地混合到另一個主題。緩動取自較晚的關鍵幀（見[[5_keyframes-and-easing]]）

完全沒有主題關鍵幀時，每個槽位都是白色

> [!warning] 警告
> 新關鍵幀使用`Linear`，所以調色盤會在從上一個主題關鍵幀到這一個的整個區間內逐漸變化。要讓主題恰好在drop處切換，把drop處的關鍵幀設為`Constant`

> [!caution] 注意
> 主題關鍵幀可能比主題本身存在得更久。刪除一個仍被關鍵幀引用的主題，所有這些幀都會變成白色。關鍵幀本身會保留。刪除這樣的主題之前，編輯器會再次確認

## 如何建立和編輯主題

關卡資源中的`主題`標籤頁顯示關卡的所有主題，上面有`{{ui:settings_level-settings_resources-themes-add}}`和`{{ui:settings_level-settings_resources-themes-import}}`。點選某一行會開啟`{{ui:settings_level-settings_theme-editor}}`：
- 主題的`{{ui:field_common_name}}`
- `主題ID`和`{{ui:settings_level-settings_theme-editor-regenerate-id}}`
- 8×8的網格。點選一個格子會選中它，顯示帶編號的`顏色：`，並把顏色載入網格下方的色輪
- 選中格子的`{{ui:editor_theme-editor_color-name}}`

編輯器在副本上工作。儲存之前，任何改動都不會進入關卡。儲存本身是一個撤銷步驟

## 如何選擇槽位

把顏色切換為`主題`，然後開啟`{{ui:editor_select-theme_color}}`

網格顯示的是在正在編輯的關鍵幀所在幀上混合後的調色盤，而不是播放頭處的。旁邊顯示該幀前後的兩個主題關鍵幀，以及選中的槽位在每個關鍵幀中的顏色。未命名的槽位顯示為`{{ui:editor_search_unnamed}}`

## 如何分享和匯入

- **本裝置的共享庫**。主題行上的`{{ui:editor_level-theme-item_export}}`會把主題儲存到`resources/themes`，這是本裝置的共享庫，`resources`與`levels`位於同一目錄下（見[[4_level-folder-and-backups]]）。`{{ui:settings_level-settings_theme-library}}`列出其中的主題，並標記已經`{{ui:editor_theme-library-item_in-level}}`的主題。`{{ui:editor_library_delete}}`會把主題從庫中移除。匯入會把主題複製到關卡中，所以關卡永遠不依賴你的庫。`{{ui:settings_level-settings_theme-library}}`也會列出合集中的主題，並顯示來源標籤：[[16_library-and-collections]]
- **遊戲自帶的主題**。`{{ui:editor_search-title_theme}}`會在關卡的主題旁邊列出遊戲自帶的主題

接下來：[[5_color-and-postprocessing|顏色、主題與後期處理]]、[[1_readability-and-fairness|可讀性與公平]]
