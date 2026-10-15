---
title: 遊玩關卡
date: 2026-10-15
tags: [player]
---

# 遊玩關卡

在關卡列表中選擇關卡，設定這一局的條件，然後開始。別人的關卡就是一個普通的資料夾：把它複製到levels資料夾，再重新整理列表

## 主選單

| 按鈕 | 作用 |
|---|---|
| `{{ui:menu_main_levels-btn}}` | 關卡列表，見下文 |
| `{{ui:menu_main_editor-btn}}` | 關卡編輯器，[[2_editor/1_basics/index]] |
| `{{ui:menu_main_sandbox-btn}}` | 不需要關卡的競技場和教程，[[13_sandbox]] |
| `{{ui:settings_common_title}}` | 所有設定，[[4_settings]] |
| `{{ui:menu_main_story-btn}}` | 暫時還不能用 |
| `{{ui:menu_main_multiplayer-btn}}` | 暫時還不能用 |

## 關卡列表

主選單中的`{{ui:menu_main_levels-btn}}`會開啟關卡列表。關卡有三個來源：

- `{{ui:root_level-source_local}}`：`levels`資料夾，[[1_installation]]
- `{{ui:root_level-source_builtin}}`：遊戲自帶的關卡
- `創意工坊`：僅限Steam版本。這裡顯示你訂閱的關卡。你訂閱的資源合集不是關卡，它們出現在編輯器的庫中，[[16_library-and-collections]]

頂部有搜尋框、`{{ui:root_level-browser_sort}}`、`{{ui:root_level-browser_layout}}`（網格或列表）和`{{ui:root_level-browser_filters}}`。列表預設以網格顯示。可以按`{{ui:root_level-browser_sort-relevance}}`、`{{ui:root_level-browser_sort-title}}`、`{{ui:root_level-browser_sort-duration}}`、`{{ui:root_level-browser_sort-progress}}`和`{{ui:root_level-browser_sort-recent}}`排序。排序按鈕旁的箭頭（`{{ui:root_level-browser_reverse}}`）會把順序反過來。`{{ui:root_level-browser_sort-relevance}}`沒有方向

搜尋先看關卡名稱，再看作者，最後看標籤

`{{ui:root_level-browser_filters}}`會開啟一個包含更多篩選條件的視窗。你一按下，視窗後面的列表就會隨之變化：

- `{{ui:root_level-filters_ai}}`：`{{ui:root_level-filters_ai-yes}}`、`{{ui:root_level-filters_ai-no}}`和`{{ui:root_level-filters_ai-unspecified}}`
- `{{ui:root_level-filters_length}}`：最短和最長的關卡，以及是否顯示時長未知的關卡
- `{{ui:root_level-filters_progress}}`：`{{ui:root_level-filters_progress-unplayed}}`、`{{ui:root_level-filters_progress-started}}`、`{{ui:root_level-filters_progress-cleared}}`、`{{ui:root_level-filters_progress-bot}}`
- `{{ui:root_level-filters_recent}}`：最近 24 小時、7 天或 30 天
- `{{ui:root_level-filters_age}}`：要顯示的最高年齡分級
- `{{ui:root_level-filters_other}}`：隱藏有密碼的關卡，隱藏來自更新版本遊戲的關卡
- `{{ui:root_level-filters_tags}}`：按一次標籤表示必須包含，按兩次表示排除

`{{ui:root_level-filters_progress}}`和`{{ui:root_level-filters_recent}}`只出現在主選單的列表中。編輯器的列表有自己的篩選條件。
按鈕上會顯示開啟了幾個篩選條件，`{{ui:root_level-browser_reset}}`會把它們全部關閉。篩選條件會一直保留，直到你關閉遊戲

把關卡複製進了資料夾？按`{{ui:root_level-browser_refresh}}`，列表就會更新

卡片上有鎖，表示這個關卡受密碼保護

長按或右鍵點選卡片會開啟選單：`{{ui:level_passphrase_open}}`和`{{ui:root_level-browser_delete}}`。對`創意工坊`關卡使用`{{ui:root_level-browser_delete}}`會取消訂閱該物品並刪除其檔案。這需要Steam正在執行，否則Steam會重新下載該關卡。內建關卡無法刪除

## 新增別人的關卡

關卡就是一個普通的資料夾。你可以把它打包後發給朋友

**資料夾**。把關卡資料夾複製到`levels`，然後按`{{ui:root_level-browser_refresh}}`。要複製的是關卡資料夾本身：裡面有`level.json`（或`level.blob`）和`metadata.json`的那個資料夾

**歸檔包**。開啟編輯器，用`{{ui:gen_level_archive}}`生成器建立一個新關卡。然後用`{{ui:editor_create-level_archive-choose}}`按鈕選擇檔案

| 檔案 | 結果 |
|---|---|
| `.zip`、`.tar.gz` | 可以開啟 |
| 自帶密碼的`.zip`、`.zip.gpg`、`.tar.gz.gpg` | 出現`{{ui:editor_create-level_archive-protected}}`後可以開啟 |
| `.7z` | 暫時拒絕。請重新打包為zip |
| 其他任何檔案 | 拒絕，[[5_troubleshooting]] |

改過名字的歸檔包照樣能開啟：遊戲根據檔案的位元組識別格式。舊版本遊戲的歸檔包會在匯入時更新

預設情況下，匯入的關卡會獲得自己的ID。所以它不會覆蓋裝置上已有的關卡

更多：[[6_sharing-by-hand]]

## 關卡介面

關卡介面顯示封面、作者、簡介和音樂作者。介面上還有`{{ui:level_level-view_authors}}`和`{{ui:level_level-view_licenses}}`按鈕

如果關卡後設資料裡寫有連結，點選作者名字和音樂那一行會開啟對應的連結

年齡分級由關卡作者標註，遊戲不做檢查

當作者宣告關卡、其封面或其中某個資源由AI生成時，會顯示“含有AI生成的內容”。這同樣是作者自己的宣告。沒有這一行並不代表“沒有AI”：作者可能只是什麼都沒有標註

開始之前你可以選擇條件：

| 條件 | 可選值 |
|---|---|
| `{{ui:menu_levelview_options-lifes_title}}` | `{{ui:menu_levelview_options-lifes_option-zen}}`（這一局不會結束）、`{{ui:menu_levelview_options-lifes_option-one}}`、`{{ui:menu_levelview_options-lifes_option-three}}`、`{{ui:menu_levelview_options-lifes_option-custom}}`（滑塊，最多16） |
| `{{ui:field_common_speed}}` | `0.5`、`1.0`、`2.0`、`{{ui:menu_levelview_options-lifes_option-custom}}`（滑塊，最多2）。關卡和音樂會一起變速 |
| `檢查點` | 開或關，[[7_damage]] |
| `{{ui:menu_levelview_options-no-collision_title}}` | 開或關。化身會穿過一切，[[7_damage]] |
| `{{ui:menu_levelview_options-bot}}` | `{{ui:enum_bot-kind_none}}`、`{{ui:enum_bot-kind_reflex}}`、`{{ui:enum_bot-kind_warm}}`，[[9_bots]] |
| `{{ui:level_level-view_seed-value}}` | 一個數字、`{{ui:level_level-view_seed-randomize}}`、`{{ui:level_level-view_seed-clear}}`。`0`表示每局使用新的種子，[[8_determinism]] |

按`開始`開始這一局

暫停時有`{{ui:game_pause-window_continue-btn}}`、`{{ui:game_pause-window_restart-btn}}`、`{{ui:game_game-result_restart-checkpoint}}`（到達檢查點之後）、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-options}}`和`{{ui:game_game-result_back-to-menu}}`。`{{ui:game_game-result_back-to-options}}`會回到關卡介面，並保留這一局開始時的條件。如果這一局是從編輯器開始的，則回到編輯器的`遊玩`標籤頁

## 結果視窗

視窗顯示`通過`或`{{ui:game_game-result_lose}}`，以及三個部分：`進度`、`{{ui:game_game-result_section-damage}}`和`{{ui:game_game-result_section-conditions}}`

- 各行：`完成度`、`{{ui:game_game-result_checkpoint}}`、`{{ui:field_common_time}}`、`{{ui:game_game-result_length}}`、`{{ui:game_game-result_hits}}`、`{{ui:game_game-result_lives-left}}`、`{{ui:game_game-result_streak}}`
- 本局條件：`{{ui:field_common_speed}}`、`{{ui:menu_levelview_options-lifes_title}}`、`{{ui:menu_levelview_options-bot}}`、`{{ui:game_game-result_seed}}`、`檢查點`。開啟`{{ui:menu_levelview_options-no-collision_title}}`的一局會在`{{ui:menu_levelview_options-lifes_title}}`後面加上`· 無碰撞`
- 按鈕：`{{ui:game_pause-window_restart-btn}}`、`{{ui:game_game-result_restart-checkpoint}}`、`{{ui:settings_common_title}}`、`{{ui:game_game-result_back-to-options}}`、`{{ui:game_game-result_back-to-menu}}`

預設情況下，失敗時不會開啟這個視窗，而是把這一局倒回到上一個檢查點。要改變這一點：`{{ui:settings_common_title}}`→`{{ui:settings_interface_label}}`→`{{ui:settings_interface_open-menu-on-lose}}`

## 紀錄

關卡介面上有一個紀錄區：`{{ui:menu_levelview_record-best}}`、`{{ui:menu_levelview_record-attempts}}`和`{{ui:menu_levelview_record-clears}}`（或`{{ui:menu_levelview_record-none}}`）

每一組條件都有自己的紀錄：生命、速度、檢查點、碰撞和機器人。紀錄區顯示當前所選條件下的紀錄。嘗試次數和通關次數對任何一局都會統計

紀錄是怎麼選出來的：[[10_statistics]]

## 難度

在列表中，關卡的難度是名稱下方那一行開頭的圖示，位於時長之前。關卡介面在年齡分級旁邊顯示圖示和等級名稱

等級由關卡作者設定，重新發布關卡的稽核員可以修改它。沒有等級的關卡不顯示圖示，它屬於`{{ui:enum_difficulty-tier_undefined}}`

| 圖示 | 等級 |
|---|---|
| ![[difficulty-auto.svg]] | `{{ui:enum_difficulty-tier_auto}}`：關卡自己完成，不需要任何操作 |
| ![[difficulty-drizzle.svg]] | `{{ui:enum_difficulty-tier_drizzle}}` |
| ![[difficulty-rain.svg]] | `{{ui:enum_difficulty-tier_rain}}` |
| ![[difficulty-downpour.svg]] | `{{ui:enum_difficulty-tier_downpour}}` |
| ![[difficulty-hail.svg]] | `{{ui:enum_difficulty-tier_hail}}` |
| ![[difficulty-barrage.svg]] | `{{ui:enum_difficulty-tier_barrage}}` |
| ![[difficulty-onslaught.svg]] | `{{ui:enum_difficulty-tier_onslaught}}` |
| ![[difficulty-deluge.svg]] | `{{ui:enum_difficulty-tier_deluge}}` |
| ![[difficulty-inferno.svg]] | `{{ui:enum_difficulty-tier_inferno}}` |
| ![[difficulty-singularity.svg]] | `{{ui:enum_difficulty-tier_singularity}}` |

等級從最簡單排到最難。目前難度到`{{ui:enum_difficulty-tier_singularity}}`為止，更難的等級以後會根據大家實際製作的關卡加入

## 卡片標記

| 標記 | 含義 |
|---|---|
| `{{ui:root_level-entry_not-listed}}` | 硬碟上有這個創意工坊資料夾，但你沒有訂閱它。只有開啟`{{ui:settings_common_title}}`→`{{ui:settings_general_title}}`→`{{ui:settings_general_show-all-found-content}}`時才可見 |
| `{{ui:root_level-entry_unverified}}` | 關卡來源沒有響應 |
| `{{ui:root_level-entry_newer-version}}`、`{{ui:root_level-entry_newer-file}}` | 這個版本的遊戲無法開啟該關卡，[[5_troubleshooting]] |
| `{{ui:root_level-entry_level-missing-badge}}` | 資料夾中沒有`level.json`，無法開始關卡，[[4_level-folder-and-backups]] |
| `{{ui:root_level-entry_meta-missing-badge}}` | 資料夾中沒有可讀取的`metadata.json`。卡片顯示資料夾名稱，關卡可以遊玩，[[4_level-folder-and-backups]] |

## 刪除關卡

長按或右鍵點選卡片→`{{ui:root_level-browser_delete}}`。遊戲會先要求確認

你可以同時刪除關卡的統計資料（`{{ui:root_level-delete_statistics}}`）和備份（`{{ui:root_level-delete_backups}}`）

刪除受保護的關卡不需要密碼
