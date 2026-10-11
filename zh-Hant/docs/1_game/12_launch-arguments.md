---
title: 啟動引數
date: 2026-10-12
tags: [advanced_player, developer]
---

# 啟動引數

啟動引數可以直接開啟某個介面、關卡或一次遊玩，開關引數只改變遊戲的這一次啟動。引數寫在執行檔後面：快捷方式、終端或Steam的啟動選項中

不帶引數時，遊戲開啟主選單

透過MCP連線的AI助手可以把同樣的引數傳送給已經在執行的遊戲 - [[7_ai-assistant]]

## 語法

- 每個引數以兩個連字元開頭：`--editor`
- 值用空格或`=`隔開：`--speed 1.5`和`--speed=1.5`是一樣的
- 鍵不區分大小寫：`--Editor`同樣有效
- 無論系統語言是什麼，數字都用小數點：`1.5`，不能寫`1,5`
- 含空格的值放在雙引號中：`--level "D:\My Levels\Volcano"`

**遊戲無法使用的引數永遠不會中止啟動**。它會被丟棄，相關的一行寫入日誌，遊戲開啟平常的介面。日誌的位置：[[11_help#日誌]]

**不認識的引數會被忽略**。遊戲只讀取自己的、帶兩個連字元的引數。Unity自己的單連字元引數，例如`-screen-width`，會原樣通過。解析度和全屏模式用它們來設定

## 介面

| 引數 | 開啟什麼 |
|---|---|
| `--menu` | 主選單，和不帶引數相同 |
| `--editor` | 關卡編輯器 |
| `--game` | `--level`指定的關卡，並立即開始遊玩 |
| `--settings` | 主選單，上面覆蓋設定介面 |

介面引數最多傳一個。兩個不同的介面引數會互相抵消，開啟的是選單，並在日誌中留下警告

`--settings`可以指定標籤頁：`general`、`audio`、`controls`、`keybindings`、`graphics`、`interface`、`game-editor`、`profile`、`other`。不指定名稱時，設定開啟在你上次所在的標籤頁。不認識的名稱會被丟棄，設定照常開啟

每次啟動設定只打開一次。之後回到選單時不會再次開啟。每個標籤頁裡有什麼：[[4_settings]]

## 選擇關卡

`--level`用關卡的識別符號（`LevelId`）或關卡資料夾的路徑來指定關卡。名稱永遠無效：名稱會重複、會被翻譯、會被修改。看起來像識別符號的值總是被當作識別符號

只在遊戲列表中已經顯示的關卡里查詢。不在列表中的資料夾，遊戲找不到

| 搭配 | 結果 |
|---|---|
| 無 | 選單開啟在關卡介面，等待`{{ui:menu_levelview_play-btn}}` |
| `--editor` | 編輯器開啟這個關卡 |
| `--game` | 立即開始遊玩 |

密碼永遠不通過引數傳遞。受保護的關卡會在介面上詢問密碼，回答後開啟

## 遊玩條件

這些條件會填寫關卡介面上的控制元件，遊玩就像你按下了`{{ui:menu_levelview_play-btn}}`一樣開始。它們只在搭配`--game`時生效。沒有它時會被忽略，並在日誌中留下警告

| 引數 | 值 | 關卡介面上的控制元件 |
|---|---|---|
| `--speed` | 大於`0`且不超過`2`，四捨五入到`0.1` | `{{ui:field_common_speed}}` |
| `--lives` | 從`0`到`16`，`0`即`{{ui:menu_levelview_options-lifes_option-zen}}` | `{{ui:menu_levelview_options-lifes_title}}` |
| `--seed` | `0`或正整數，`0`表示每次遊玩使用新種子 | `{{ui:level_level-view_seed-value}}` |
| `--bot` | `none`、`reflex`、`warm` | `{{ui:menu_levelview_options-bot}}` |
| `--checkpoints`、`--no-checkpoints` | 無 | `{{ui:menu_levelview_options-checkpoints_title}}` |
| `--no-collision` | 無 | `{{ui:menu_levelview_options-no-collision_title}}` |

省略的條件取預設值：3條生命，速度`1.0`，檢查點開啟，無機器人，種子`0`，碰撞開啟

這樣啟動的遊玩就是普通的遊玩。它和其他遊玩一樣計入統計，[[10_statistics]]

## 作用於整次啟動的開關

這三個引數適用於任何介面，永遠不會修改已儲存的設定：

| 引數 | 作用 |
|---|---|
| `--autosave on`、`--autosave off` | 在這次啟動中開啟或關閉編輯器的自動儲存。設定的`{{ui:settings_game-editor_title}}`標籤頁顯示強制的值，並且不允許修改 |
| `--suppress-game-saves` | 整次啟動使用匿名模式。無法在遊戲中關閉，[[4_settings#匿名模式]] |
| `--frame-stats` | 向日志寫入幀時間彙總，包括GPU和CPU時間。用於效能測量 |

`--frame-stats`每30秒為每個介面寫一行，介面上方的視窗每次變化時也會寫一行。介面的前3秒不計入

## 組合

| 命令 | 結果 |
|---|---|
| 無或`--menu` | 選單 |
| `--editor` | 未開啟關卡的編輯器 |
| `--settings` | 選單，設定開啟在你上次所在的標籤頁 |
| `--settings graphics` | 同上，開啟在`{{ui:settings_graphics_title}}`標籤頁 |
| `--level X` | 選單顯示關卡X的介面，等待`{{ui:menu_levelview_play-btn}}` |
| `--level X --game` | 關卡X，正在遊玩 |
| `--level X --editor` | 打開了關卡X的編輯器 |
| `--game`但沒有`--level` | 選單和警告 |
| `--menu --editor` | 選單和警告 |
| `--speed 2`但沒有`--game` | 條件被忽略，並有警告 |
| `--editor --autosave off` | 編輯器，自動儲存僅在這次啟動中關閉 |
| `--autosave maybe` | 被忽略並有警告，由你的設定決定 |
| `--suppress-game-saves` | 選單。這次啟動中游戲自己的存檔都不會寫入磁碟 |
| `--level X --game --suppress-game-saves` | 關卡X，正在遊玩，結束後不留下統計 |
| `--editor --suppress-game-saves` | 編輯器。關卡存檔、自動儲存和備份照常寫入，設定和統計不寫入 |

## 示例

在Windows上，從終端或快捷方式：

```bash
"Bullet Hero.exe" --editor
"Bullet Hero.exe" --level 5f2b0e6a-1c3d-4b5e-8a9f-0d1e2f3a4b5c --game --lives 1 --speed 1.5
"Bullet Hero.exe" --level "C:\Users\<you>\AppData\LocalLow\vertoker\Bullet Hero\levels\Volcano" --editor
```

在Steam中，遊戲的啟動選項只寫引數，不寫執行檔：`--editor --autosave off`

## Android

Android沒有命令列。引數通過啟動遊戲的intent中的字串附加資料`bh`傳遞，拆分方式和手動輸入的命令列完全相同。從電腦上通過`adb`來完成：

```bash
adb shell "am start -S -n com.vertoker.BulletHero/com.unity3d.player.UnityPlayerGameActivity -e bh '--frame-stats --editor'"
```

- **引號很重要**。整個`am start`放在雙引號中，`bh`的值放在單引號中。否則裝置的shell會拆開這一行：`bh`只收到第一個引數，其餘的會作為`am`自己的引數交給它
- **`-S`會先停止正在執行的遊戲**。引數只在啟動時讀取一次。傳送給已經在執行的遊戲不會有任何變化

iOS完全沒有啟動引數
