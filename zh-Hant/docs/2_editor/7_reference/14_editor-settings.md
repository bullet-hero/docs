---
title: 編輯器設定
date: 2026-10-11
tags: [level_author]
---

# 編輯器設定

自動儲存、網格、選擇、控制柄和新關卡的預設都在這裡設定。自動儲存預設開啟，在編輯後{{v:editor.autosave-delay}}秒觸發

## 編輯器

自動儲存、相機、選擇和檔案格式都在這裡設定

| 設定 | 作用 | 預設值 |
|---|---|---|
| `{{ui:settings_game-editor_autosave}}` | 開啟自動儲存 | 開 |
| `{{ui:settings_game-editor_autosave-rate}}` | 從出現未儲存的編輯到自動儲存之間經過多少秒 | {{v:editor.autosave-delay}} |
| `{{ui:settings_game-editor_max-autosave-files}}` | 保留多少份副本。達到上限時刪除最舊的一份 | {{v:editor.autosave-copies}} |

只有存在未儲存的編輯時，計時器才會計時

一次自動儲存做兩件事：
1. 把關卡的副本寫入`<game folder>/backups/<level id>/`
2. 儲存關卡本身，和按`Ctrl+S`一樣

副本只包含關卡檔案。有兩種方式恢復它：
- 在關卡設定中：`{{ui:settings_level-settings_dangerous-zone}}` → `{{ui:level_backups_open}}`
- 手動：把它複製到關卡資料夾中，命名為`level.json`（或`level.blob`）

更多：[[4_not-losing-work#自動儲存]]

`{{ui:settings_game-editor_camera-min-size}}`和`{{ui:settings_game-editor_camera-max-size}}`限制編輯器視口能放大和縮小到什麼程度

`{{ui:settings_game-editor-multi-select-requires_hold}}`和`{{ui:settings_game-editor-pick-invisible_aabb}}`會改變在視口中單擊的含義。如果選擇的行為突然和你習慣的不一樣，請檢查這兩項

`{{ui:settings_game-editor-level-serialize_mode}}`和`{{ui:settings_game-editor-resources-serialize_mode}}`設定寫入磁碟時的預設格式

`{{ui:settings_game-editor_publish-language}}`決定創意工坊物品的標題和描述優先以哪種語言釋出：`{{ui:enum_publish-language_english}}`（預設）或`{{ui:enum_publish-language_system}}`，即裝置的語言

更多：[[3_speed-and-shortcuts]]

## 網格

視口網格繪製在關卡後面，幫助你擺放物體

| 設定 | 作用 | 預設值 |
|---|---|---|
| `{{ui:settings_game-editor_grid-active-default}}` | 開啟編輯器時是否顯示網格。這只是初始狀態 | 關 |
| `{{ui:settings_game-editor-grid_size}}` | 一個格子的邊長，以世界單位計 | 1 |
| `{{ui:settings_game-editor-grid_opacity}}` | 線條的明顯程度，從0到1 | 0.25 |

工具欄上的網格按鈕用於開關網格。這個狀態不會在會話之間儲存

網格的外觀：
- 它沒有邊界。縮放時格子以10倍為一級變化，更細的網格會逐漸顯現
- 如果某一級網格需要的線條太多，這一級會被關閉，而不是被稀疏化
- 線條顏色始終與當前幀相機背景的顏色相反，所以背景變化時網格依然可見。你只設置不透明度

開啟吸附時，拖動位置會吸附到半個格子：吸附到交叉點和格子中心。使用的是你能看到的那一級網格。關閉網格時，位置會吸附到固定的步長

## 選擇

| 設定 | 作用 | 預設值 |
|---|---|---|
| `{{ui:settings_game-editor-multi-select-requires_hold}}` | 開：在多選模式中，只有按住`Ctrl`時單擊才會新增，普通單擊會替換選中項。關：多選模式開啟期間，每次單擊都會新增 | 開 |
| `{{ui:settings_game-editor-preview-collider-on_select}}` | 用半透明填充繪製每個選中物體的判定框 | 關 |
| `{{ui:settings_game-editor-pick-invisible_aabb}}` | 單擊時按物體的整個矩形來選取，而不是按它繪製的內容 | 關 |
| `{{ui:settings_game-editor_selection-long-press-delay}}` | 按住多久才會開啟選單，以秒計 | 0.5 |
| `{{ui:settings_game-editor_selection-long-press-threshold}}` | 按住期間游標可以移動多遠，超過就變成拖動 | 8 |
| `{{ui:settings_game-editor_selection-collider-opacity}}` | 選中物體的判定框繪製得有多實 | 0.5 |
| `{{ui:settings_game-editor_selection-collider-opacity-view}}` | 顯示所有判定框時的同一設定，更淡一些，因為那裡有數百個判定框相互重疊 | 0.25 |

在多選模式中鬆開`Ctrl`不會取消任何選擇，也不會退出該模式。只有下一次普通單擊才會替換選中項。關於這個模式的更多內容：[[4_hierarchy-and-clipboard]]

工具欄上的碰撞體按鈕會顯示幀中所有內容的判定框，包括玩家的圓形。這個狀態不會在會話之間儲存。如果螢幕上的判定框太多，顯示會自行關閉並給出提示，而不是隻繪製其中一部分

沒有碰撞體的物體在兩種模式下都不繪製判定框，未啟用的物體也一樣

兩種模式的填充顏色是`設定 > 圖形 > “僅碰撞體”模式 > 填充顏色`，與遊戲的“僅碰撞體”模式共用（[[4_settings]]）。上面的兩個不透明度仍是編輯器自己的設定

## 控制柄

| 設定 | 作用 | 預設值 |
|---|---|---|
| `{{ui:settings_game-editor_gizmos-scale}}` | 視口中拖拽手柄的大小，從0.1到10。為滑鼠設計的手柄很難用手指點中 | 1 |

無論如何縮放，手柄在螢幕上的大小都保持不變

## AI代理

`{{ui:settings_game-editor_mcp_title}}`讓支援MCP的AI客戶端編輯開啟的關卡。僅限Windows、Linux和Mac：手機和平板上不顯示這一部分

| 設定 | 作用 | 預設值 |
|---|---|---|
| `{{ui:settings_game-editor_mcp-enabled}}` | 允許客戶端連線。只有本機可以連線，同一時間只能連線一個客戶端 | 關閉 |
| `{{ui:settings_game-editor_mcp-port}}` | 編輯器監聽的埠。`0`表示每次啟動自動選一個空閒埠，否則填{{v:mcp.port-min}}到{{v:mcp.port-max}}。其他數字會被還原 | 0 |
| `{{ui:settings_game-editor_mcp-follow-ai}}` | AI檢視某一幀之後播放頭停在哪裡。關閉：回到你離開時的位置。開啟：停在那一幀並暫停 | 開 |
| `{{ui:settings_game-editor_mcp-reveal-edits}}` | 每次AI編輯後，選中並定位它建立或修改的內容。你在拖動、輸入或遊玩時不會這樣做 | 開 |
| `{{ui:settings_game-editor_mcp-operation-delay}}` | 編輯器在兩次AI操作之間等待的秒數，範圍0到{{v:mcp.operation-delay-max}}。`0`表示每次立即執行。播放、暫停和移動播放頭從不延遲，AI只讀取的內容也不延遲 | {{v:mcp.operation-delay}} |

`{{ui:settings_game-editor_mcp-copy-config}}`會複製MCP客戶端所需的配置，其中已填好伺服器路徑和遊戲連線檔案的路徑

設定下方的一行顯示編輯器的狀態：已關閉、正在監聽某個埠、已連線，或已通過編輯器中的AI標記停止

這些設定只儲存在本裝置上

更多：[[7_ai-assistant]]

## 建立關卡

`{{ui:settings_editor-settings_level-presets}}`決定新關卡從什麼開始：空的，或者帶一小套基礎框架。沒有預設的話，你每次都得手工搭建這套框架

> [!caution] 注意
> `{{ui:settings_editor-settings_parameters}}`中設定的是之後不便修改的內容：以幀計的長度和幀率

> [!tip] 提示
> `{{ui:settings_editor-settings_quot-level-quot-file-format}}`和`{{ui:settings_editor-settings_quot-metadata-quot-file-format}}`列表決定關卡及其後設資料以何種格式寫入磁碟。兩者之後都可以在關卡的`{{ui:settings_level-settings_dangerous-zone}}`中修改

更多：[[2_first-level]]

## 庫

`{{ui:settings_editor-settings_library}}`是最後一個標籤頁，位於`{{ui:settings_editor-settings_community}}`之後。這裡存放你在關卡之間複用的資源：本裝置的共享庫、你自己的合集，以及在Steam版本中你在Steam創意工坊訂閱的合集

左側一列選擇類別：先是`{{ui:settings_level-settings_collections}}`，然後是預製件、主題、形狀和特效，最後是紋理、字型和音訊。你可以在這裡建立和編輯合集，在合集之間複製條目，匯入和匯出合集，並在Steam版本中釋出你自己的合集

更多：[[16_library-and-collections]]

## 使用他人的作品

關卡中的每個外部資源（音樂、圖片、字型、文本）都必須符合以下兩種情況之一：
- 許可證至少與`CC BY-NC`同等自由
- 版權所有者本人給出的公開非商業分發許可

> [!caution] 注意
> 私下一句“沒問題”是不夠的。採用`CC BY-NC`的關卡會被公開分發。許可必須涵蓋的正是這一點，而不只是你的個人使用

留在你裝置上的關卡不會接受檢查。規則只在一個時刻生效：關卡被交給某個服務的時候

完整規則、可接受的許可證列表、請求模板以及去哪裡找資源：
- [[2_legal-resource-paths]]
- [[6_asking-permission]]
- [[3_where-to-get-resources]]
