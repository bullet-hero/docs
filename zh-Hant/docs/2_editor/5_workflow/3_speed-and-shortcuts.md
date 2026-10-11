---
title: 效率與快捷鍵
date: 2026-10-02
tags: [level_author]
---

# 效率與快捷鍵

最省時間的是命令面板（Ctrl+Shift+P）、內容搜尋（Ctrl+F）、“定位”按鈕和時間軸上的方向鍵。任何按鍵都可以在設定中重新繫結

## 最省時間的四樣東西

- **`{{ui:editor_search-title_command}}`**（`Ctrl+Shift+P`）：編輯器能做的一切，都能按名稱搜尋。比記住某個按鈕在哪個面板上更快
- **`搜尋內容`**（`Ctrl+F`）：按名稱跳轉到物體或音訊軌道，播放頭會跟著一起跳過去
- **`{{ui:cmd_editor_ping}}`**：視口把選中項框入畫面，時間軸和層級同時滾動到它的位置。再按一次會跳到多選中的下一個物體
- **時間軸上的方向鍵**：按方向移動，而不是按列表順序。在相鄰關鍵幀之間切換不需要滑鼠

## 預設快捷鍵

下面的分組和名稱與`{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`中顯示的一致

### 播放

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `Space` | `{{ui:settings_keybindings_editor_play_pause}}` | 播放和暫停 |

### 編輯

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `Ctrl+Z` | `{{ui:cmd_editor_undo}}` | 撤銷 |
| `Ctrl+Y`或`Ctrl+Shift+Z` | `{{ui:cmd_editor_redo}}` | 重做 |
| `Ctrl+S` | `{{ui:settings_keybindings_editor_save}}` | 儲存 |
| `Ctrl+C` | `{{ui:cmd_editor_copy}}` | 複製 |
| `Ctrl+V` | `{{ui:cmd_editor_paste}}` | 貼上 |
| `Ctrl+D` | `{{ui:cmd_editor_duplicate}}` | 建立副本 |
| `Ctrl+G` | `{{ui:cmd_editor_pack-prefab}}` | 從選中項建立預製件 |

### 選中項

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `Del` | `{{ui:settings_keybindings_editor_delete}}` | 刪除選中項 |
| 按住`Ctrl` | `{{ui:settings_keybindings_editor_multi_select}}` | 多選 |
| `Ctrl+Shift+A` | `{{ui:settings_keybindings_editor_deselect}}` | 一次清除所有選中：物體、關鍵幀、音訊和節拍 |
| `Ctrl+Shift+E` | `{{ui:cmd_editor_exit-prefab}}` | 退出預製件模式，回到關卡 |

### 檢視

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `Ctrl+F` | `搜尋內容` | 搜尋內容 |
| `Ctrl+Shift+P` | `{{ui:editor_search-title_command}}` | 執行命令 |
| `Ctrl+Left` | `{{ui:settings_keybindings_editor_panel_left}}` | 顯示或隱藏左側面板 |
| `Ctrl+Right` | `{{ui:settings_keybindings_editor_panel_right}}` | 顯示或隱藏右側面板 |
| `Ctrl+Down` | `{{ui:settings_keybindings_editor_panel_bottom}}` | 顯示或隱藏底部面板 |
| `Ctrl+Up` | `{{ui:settings_keybindings_editor_viewport_tools}}` | 顯示或隱藏視口上方的工具組 |
| 按住`` ` `` | `{{ui:settings_keybindings_editor_preview}}` | 預覽：按住期間隱藏編輯器介面 |

### 時間軸

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `Z` | `{{ui:settings_keybindings_editor_expansion_cycle}}` | 迴圈切換摺疊：全部子樹、僅選定的型別、不折疊 |
| `X` | `{{ui:settings_keybindings_editor_tool_snap}}` | 開啟或關閉吸附 |
| `C` | `{{ui:settings_keybindings_editor_tool_selection}}` | 選擇工具 |
| `V` | `{{ui:settings_keybindings_editor_tool_marquee}}` | 框選工具 |
| `B` | `{{ui:settings_keybindings_editor_tool_scissors}}` | 剪刀工具 |
| `N` | `{{ui:settings_keybindings_editor_tool_edges}}` | 邊緣工具 |
| `Ctrl+E` | `{{ui:settings_keybindings_editor_fold}}` | 在時間軸上摺疊選中的物體 |
| `Q` | `{{ui:settings_keybindings_editor_tab_timeline_level}}` | 開啟關卡時間軸 |
| `W` | `{{ui:settings_keybindings_editor_tab_timeline_local}}` | 開啟區域性時間軸 |
| `E` | `{{ui:settings_keybindings_editor_tab_timeline_audio}}` | 開啟音訊時間軸 |
| `R` | `{{ui:settings_keybindings_editor_tab_timeline_events}}` | 開啟事件時間軸 |
| `T` | `{{ui:settings_keybindings_editor_tab_timeline_prefab}}` | 開啟預製件時間軸 |
| `Shift+T` | `{{ui:settings_keybindings_editor_beat_window}}` | 節拍網格視窗，在這裡敲出速度。`{{ui:settings_keybindings_editor_beat_tap}}`本身預設沒有按鍵，需要的話自己繫結一個 |
| 按住`Ctrl`並滾動滾輪 | `{{ui:settings_keybindings_timeline_pan_modifier}}` | 平移 |
| 按住`Shift`並滾動滾輪 | `{{ui:settings_keybindings_timeline_zoom_modifier}}` | 縮放 |

`Z X C V B N`從左到右對應時間軸工具欄，`Q W E R T`對應標籤頁欄。工具較少的時間軸從右邊開始缺少：區域性時間軸只有`Z X C V`。當前時間軸沒有對應工具的字母鍵不起作用

### 控制柄

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `1` | `{{ui:settings_keybindings_editor_gizmo_none}}` | 選擇 |
| `2` | `{{ui:settings_keybindings_editor_gizmo_position}}` | 位置 |
| `3` | `{{ui:settings_keybindings_editor_gizmo_rotation}}` | 旋轉 |
| `4` | `{{ui:settings_keybindings_editor_gizmo_scale}}` | 縮放 |
| `5` | `{{ui:settings_keybindings_editor_gizmo_size}}` | 尺寸 |
| `6` | `{{ui:settings_keybindings_editor_gizmo_anchors}}` | 錨點 |
| `7` | `{{ui:settings_keybindings_editor_gizmo_pivot}}` | 軸心 |
| `0` | `{{ui:settings_keybindings_editor_gizmo_hidden}}` | 隱藏：選中狀態保留，但不繪製手柄和邊框 |

### 視窗

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `F11` | `{{ui:settings_keybindings_window_toggle_fullscreen}}` | 開啟或關閉全屏。在任何螢幕上都有效，僅限桌面端 |
| `Ctrl+S` | `{{ui:settings_keybindings_window_settings_save}}` | 設定開啟時立即把設定寫入磁碟。在編輯器中`Ctrl+S`儲存關卡 |

### 導航

| 按鍵 | 設定中的名稱 | 作用 |
|---|---|---|
| `Up` | `{{ui:settings_keybindings_nav_up}}` | 在你最後點選進入的區域中向上移動 |
| `Down` | `{{ui:settings_keybindings_nav_down}}` | 在你最後點選進入的區域中向下移動 |
| `Left` | `{{ui:settings_keybindings_nav_left}}` | 在你最後點選進入的區域中向左移動 |
| `Right` | `{{ui:settings_keybindings_nav_right}}` | 在你最後點選進入的區域中向右移動 |

在文本框中輸入時，不帶修飾鍵的單鍵，例如控制柄數字鍵、時間軸字母鍵和`Space`，都不起作用。在幀數輸入框裡輸入`2`不會切換控制柄

## 時間軸上的方向鍵

方向鍵會選中螢幕上該方向最近的專案。無論縮放到什麼程度，同樣的按鍵都會找到同一個專案

- 在多選狀態下，方向鍵從沿按鍵方向最遠的那個專案出發，永遠不會退回到你選中的那一塊裡
- 方向鍵移動總是替換選中項，從不追加
- 時間軸只滾動到剛好能顯示新專案的程度。點選播放頭讀數仍然會讓檢視居中
- 試玩玩家開啟時，方向鍵控制的是它，而不是時間軸。層級和`{{ui:settings_level-settings_raw}}`標籤頁在你點選進入後會保留方向鍵的控制權

## 檢視關卡

**預覽**。按住`` ` ``可以隱藏編輯器介面，只看關卡本身。這是按住生效，不是開關：鬆開按鍵，一切都會恢復。關卡、黑邊（letterbox）、玩家和相機邊界仍然可見。它沒有對應的按鈕或設定。這個按鍵可以在`{{ui:settings_keybindings_editor_preview}}`中重新繫結

**視口網格**通過工具欄上的按鈕或`{{ui:cmd_editor_viewport-grid}}`命令切換，預設關閉。`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_grid-active-default}}`可以改變這一點，而你手動開啟網格這件事不會在會話之間被記住

**控制柄吸附**會把控制柄拖動的內容吸附到網格上。它預設開啟，與控制柄模式無關。用工具欄按鈕或`{{ui:cmd_editor_gizmo-magnet}}`命令切換

**暫停是檢視的常態**。播放暫停時，網格、碰撞體、機器人疊加層、控制柄手柄和選中邊框都會繼續繪製。抓住控制柄手柄時，播放會暫停

## 重新繫結

任何按鍵都可以重新繫結：`{{ui:settings_common_title}}` → `{{ui:settings_keybindings_label}}`

只儲存你改過的按鍵，其餘的都取自預設值。所以如果你沒有動過某個按鍵，它的預設值改進後會直接生效。`{{ui:settings_keybindings_reset}}`只是刪除你的修改，所有按鍵都回到預設值

> [!tip] 提示
> 按鍵標籤沒有寫死在介面裡。重新繫結後，命令面板和所有右鍵選單會立即顯示新的按鍵

## 按下型和按住型按鍵

按下型按鍵只在修飾鍵完全一致時觸發。`Ctrl+Shift+P`不會順帶觸發`Ctrl+P`的功能，按住`Ctrl`時單獨的`T`也不會觸發

按住型按鍵在它的修飾鍵包含在當前按住的修飾鍵中時觸發。它用來細化一個已經在進行中的操作

> [!info] 須知
> 所以兩個按住型按鍵可以故意共用同一個鍵。多選和時間軸平移都在`Ctrl`上，兩者互不衝突

接下來：[[1_order-of-work|工作順序]]、[[2_reuse|複用：預製件、複製、生成器]]
