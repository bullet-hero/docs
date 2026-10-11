---
title: AI助手
date: 2026-10-12
tags: [level_author]
---

# AI助手

支援MCP的AI客戶端可以在你眼前編輯編輯器中開啟的關卡。每個AI批次操作都是一個撤銷步驟，AI不能釋出、刪除檔案，也不能覆蓋其他關卡

為此，Windows、Linux和Mac上的遊戲自帶一個MCP伺服器。AI用和你相同的操作進行編輯，所以每處改動都會立刻出現在視口中，並像你自己的操作一樣進入歷史記錄

任何支援MCP的客戶端都可以，比如聊天應用或程式設計助手。遊戲中沒有任何東西繫結在某一個AI上

## 連線客戶端

1. 開啟`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. 勾選`{{ui:settings_game-editor_mcp-enabled}}`。設定下方的狀態行會顯示編輯器監聽的埠
3. 按下`{{ui:settings_game-editor_mcp-copy-config}}`。剪貼簿中就有了已填好兩個路徑的客戶端配置
4. 把它貼上到你的客戶端的MCP伺服器設定中
5. 在編輯器中開啟一個關卡，或者讓AI自己開啟編輯器或關卡

複製的配置是這樣的：

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to mcp>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

伺服器檔案`mcp`位於遊戲旁邊：

| 系統 | 伺服器檔案 |
|---|---|
| Windows | `<遊戲資料夾>/mcp.exe` |
| Linux | `<遊戲資料夾>/mcp` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/mcp`，Intel上用`osx-x64`代替`osx-arm64` |

只有本機可以連線，並且同一時間只能連線一個客戶端。手機和平板上沒有MCP部分：助手只在電腦上可用

## AI能做什麼，不能做什麼

你能做的事，AI幾乎都能做：
- 讀取關卡：層級、物體、關鍵幀、事件和資源
- 建立、修改和刪除物體、關鍵幀、標記、檢查點、音訊軌道和節拍網格
- 執行生成器，打包和放置預製件，在預製件模式中工作
- 把紋理、字型或音訊檔案匯入關卡
- 撤銷和重做，儲存開啟的關卡，開啟其他關卡，建立新關卡
- 用與啟動時相同的引數把遊戲切換到其他介面，例如編輯器、某個關卡或設定 - [[12_launch-arguments]]
- 在遊戲未執行時啟動遊戲，前提是伺服器位於已安裝的遊戲旁邊且MCP已經開啟

這樣開始的遊玩和其他遊玩一樣計入你的統計，所以AI只在你要求時才會開始遊玩

它不能：
- 釋出到Steam創意工坊
- 刪除關卡或任何檔案
- 覆蓋其他關卡或其他檔案。檔名已被佔用的匯入會被拒絕
- 開啟只讀關卡，或者本次會話中你還沒輸入過密碼的受保護關卡
- 在開啟的關卡有未儲存的修改時開啟其他關卡

**一個AI批次操作就是歷史記錄中的一步**。它在`{{ui:settings_level-settings_history}}`標籤頁中顯示為`{{ui:op_group_ai-batch}}`，並帶有AI自己寫的說明。按一次`Ctrl+Z`就會撤銷整個批次操作。關於歷史記錄的更多內容：[[10_level-settings#歷史]]

第一個修改關卡的AI批次操作會把關卡的`{{ui:settings_level-settings_metadata-level-ai-generated}}`設為`{{ui:enum_ai-generation_yes}}`，而且是在同一步中。撤銷這個批次操作也會把它還原。更多：[[2_metadata-and-sharing#AI生成]]

## 你優先

AI從不和你爭奪編輯器：
- 你拖動控制柄手柄或拖動時間軸時，AI的編輯會被拒絕，它會等待並重試
- AI只在你空閒時才使用播放頭：沒有在遊玩、拖動、輸入或儲存
- AI檢視某一幀時你動了編輯器，AI會立刻停下。播放頭留在你放的位置
- 歷史記錄跳轉進行期間，AI也無法編輯

客戶端連線期間，視口右上角的搜尋按鈕下方會顯示`AI`標記。它的顏色就是狀態：綠色表示已連線，黃色表示AI正在工作，紅色表示AI的上一次呼叫以錯誤結束。把指標停在它上面可以看到文字狀態：`{{ui:editor_agent-badge_connected}}`，AI工作時則顯示它正在做的事的說明。旁邊的叉號會斷開客戶端並拒絕它連線，標記隨之消失

停止狀態不會儲存。關閉再重新開啟`{{ui:settings_game-editor_mcp-enabled}}`或重啟遊戲都會解除它

## AI看到什麼

AI用兩種方式觀察關卡：
- **示意圖**。任意一幀的圖片，在螢幕外計算出來。它不移動播放頭。上面有形狀和判定框，但沒有文本和特效
- **截圖**。真實的畫素，和關卡繪製的完全一樣，通過你的播放頭拍下。播放頭會短暫跳到那一幀，編輯器的疊加層會隱藏。然後播放頭回到你離開時的位置，除非開啟了`{{ui:settings_game-editor_mcp-follow-ai}}`。畫面由關卡攝像機取景，而不是編輯器攝像機

跳轉之後的特效截圖接近連續播放時的樣子，但不一定完全相同

AI聽不到音樂。它把音軌變成數字：速度、節拍、小節、段落、每個頻段的響度。這只是帶置信度的估計，可能出錯，比如速度差一半或一倍。你在關卡中設定的節拍網格比AI的估計更可信

所以在時機很重要時，AI可能會請你聽一下。它在編輯器中播放最長{{v:mcp.max-play-seconds}}秒的一段，這也會移動播放頭。你一動編輯器，播放就停在當前位置

## ai資料夾

AI把關於關卡的記憶儲存在關卡資料夾內的`ai`資料夾中。下一次會話，無論用哪個客戶端，都會先讀它，從上一次停下的地方繼續

裡面有：
- `CONTEXT.md`：任務、音樂、段落計劃、決定、你的意見和未解決的問題
- AI決定保留的其他檔案，只能是`.md`或`.json`
- `manifest.json`：資料夾是否隨關卡一起傳送。AI無法修改它

只有當AI第一次有東西要寫時，這個資料夾才會出現。一個檔案最多{{v:mcp.ai-file-max-kb}}KB，整個資料夾最多{{v:mcp.ai-folder-max-mb}}MB。這些都是普通的文本檔案：你可以自己閱讀、編輯或刪除

> [!warning] 警告
> `ai`資料夾不屬於關卡的歷史記錄。`Ctrl+Z`不會撤銷AI寫進去的內容

**預設情況下，資料夾會隨關卡一起傳送**：進入匯出的歸檔包和Steam創意工坊上傳內容。想把它留在本地，就在關卡設定的`{{ui:settings_level-settings_metadata}}`標籤頁中取消勾選`{{ui:settings_level-settings_metadata-level-ai-share}}`。資料夾存在後這個核取方塊才會出現。它會立即儲存到檔案，所以`Ctrl+Z`也不會還原它

帶密碼的匯出模式從不包含這個資料夾，無論核取方塊怎麼設定。更多：[[13_export-and-protection#匯出關卡]]

在本裝置上覆制關卡時，資料夾會一起復制，因為複製不是分享

## 設定

所有設定都在`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`中，只儲存在本裝置上：
- `{{ui:settings_game-editor_mcp-enabled}}`：客戶端到底能不能連線。預設關閉
- `{{ui:settings_game-editor_mcp-port}}`：編輯器監聽的埠。`0`表示每次啟動自動選一個空閒埠
- `{{ui:settings_game-editor_mcp-follow-ai}}`：開啟時，截圖之後播放頭停在AI檢視的那一幀並暫停
- `{{ui:settings_game-editor_mcp-reveal-edits}}`：每次AI編輯後，選中並定位它建立或修改的內容

所有設定及其預設值：[[14_editor-settings#AI代理]]

接下來：[[4_not-losing-work]]、[[13_export-and-protection]]
