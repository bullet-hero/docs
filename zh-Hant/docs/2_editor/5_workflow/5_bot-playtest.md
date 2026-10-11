---
title: 機器人如何遊玩你的關卡
date: 2026-10-02
tags: [level_author]
---

# 機器人如何遊玩你的關卡

機器人用和你相同的操作遊玩關卡，檢查的是可讀性而不是難度。它不保證能通關

它觀察飛來的東西，尋找空閒的空間，操控的也是和你一樣的角色。它會移動、衝刺、受到傷害，也會死亡

機器人在關卡開始前選擇，就在生命和速度旁邊

## 編輯器中的機器人

在編輯器中，機器人操控預覽玩家：
1. 開啟`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_player_title}}`
2. 勾選`{{ui:settings_game-editor-player_bot}}`
3. 在工具欄中開啟預覽玩家

預覽玩家不能選擇機器人，始終是`{{ui:enum_bot-kind_reflex}}`。只有這個機器人不需要提前準備任何東西。你編輯關卡時它會繼續工作，任何播放速度都可以，包括倒放

剛拖動播放頭之後，機器人會短暫地玩得差一些：它在重新瞭解前方有什麼

當你拖動控制柄手柄或在文本框中輸入時，預覽玩家不響應你的操作

同一組設定中的`{{ui:settings_game-editor-player_bot-debug}}`會在關卡上方繪製資訊。它預設關閉，而它的三個部分預設開啟，所以開啟它就能立刻看到完整的畫面：
- `{{ui:settings_game-editor-player_bot-debug-grid}}`：機器人認為螢幕每個區域有多少空閒空間。紅色是它預計會被擊中的位置，空間越大顏色越淡。它認為自己安全的地方不繪製任何東西
- `{{ui:settings_game-editor-player_bot-debug-target}}`：它正在前往的點。目標不動表示機器人滿意了，而不是卡住了
- `{{ui:settings_game-editor-player_bot-debug-reach}}`：它預計自己能到達多遠，內圈是走路，外圈是衝刺。它從不選擇圈外的目標

只繪製`{{ui:enum_bot-kind_reflex}}`的資訊。在暫停時開啟它，畫面是靜止的

**用任意機器人完整遊玩**。關卡設定的`{{ui:settings_level-settings_play}}`標籤頁中有一個`{{ui:settings_level-settings_bot}}`列表，與選單中關卡介面上的相同：`{{ui:enum_bot-kind_none}}`、`{{ui:enum_bot-kind_reflex}}`、`{{ui:enum_bot-kind_warm}}`。這會啟動一次真正的關卡遊玩，而不是預覽玩家

## 解讀結果

機器人檢查的是可讀性，而不是難度：
- 機器人從容通過了你覺得很難的一段。說明這一段是可讀的，只是你練習不夠
- 機器人在同一個地方一次又一次被擊中。去看看那個地方：通常是一個不留逃生空間的危險物。人類玩家也不會讀得更好

## 機器人保證什麼、不保證什麼

**機器人不保證能通關**。它是一個不會累的玩家，而不是一個不會輸的玩家。如果某一段要求提前一秒就以正確的方式進入彈幕組合，機器人會被擊中。這不是錯誤

> [!info] 須知
> 機器人無法作弊，這是它的設計。它的操作和玩家相同，沒有任何額外能力：同樣的速度、同樣的衝刺、同樣的判定框、同樣的傷害。玩家過不去的地方，機器人也過不去

**機器人會加重裝置負擔**。它每一幀都在尋找空閒空間。在效能較弱的裝置上會掉幀。在複雜的關卡上，最初幾秒會最嚴重

## 打敗了機器人的關卡

機器人只有在還沒見過的關卡上才會進步。機器人已經能通關的關卡對它沒有任何幫助

你的關卡打敗了機器人？把它發過來：
1. 在[bullet-hero/releases](https://github.com/bullet-hero/releases/issues)中提交一個issue
2. 寫明是哪個機器人在哪裡輸了
3. 附上關卡資料夾

接下來：[[1_readability-and-fairness|可讀性與公平性]]、[[3_difficulty-curve|難度]]
