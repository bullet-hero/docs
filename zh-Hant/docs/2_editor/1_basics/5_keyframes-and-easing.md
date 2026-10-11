---
title: 關鍵幀與緩動
date: 2026-10-02
tags: [level_author]
---

# 關鍵幀與緩動

關鍵幀是某條軌道在某一幀上的數值，再加上到達這個數值時使用的緩動。關卡中所有會移動、變色或開關的東西，都是一串關鍵幀

基礎概念：[[3_how-the-editor-thinks]]。關鍵幀檢視器的每個欄位：[[5_object-properties]]

## 哪些內容可以做動畫

每條軌道都有自己的關鍵幀，與其他軌道互不影響：

| 所屬 | 軌道 |
|---|---|
| 任意物體 | 位置、旋轉、縮放、尺寸、錨點、軸心 |
| 形狀 | 顏色、UV |
| 文本 | 顏色、字號、文本已寫出的部分、文本被隱藏的部分 |
| 相機 | 位置、旋轉、縮放、軸心、震動 |
| 關卡 | 背景、主題、螢幕限制、12種後期效果中的每一種 |
| 玩家 | 尺寸、速度、可見性、控制、碰撞 |

物體的關鍵幀從它的時段起點開始計算。所以在時間上移動物體，它的整段動畫會跟著一起移動

位置相對於父級設定。關鍵幀儲存的是數值本身，而不是相對於上一個關鍵幀的增量

玩家的可見性、控制和碰撞只有開和關兩種狀態。這些關鍵幀沒有緩動：沒有什麼可以混合

空的玩家軌道上的第一個關鍵幀不會改變畫面：可見性、控制和碰撞為開啟，大小和速度為玩家的常規值。控制關閉或玩家隱藏時無法操控玩家：游標消失，按下也不會被接收。隱藏的玩家仍會被擊中：這隻由碰撞決定

## 幾條建議

- 只給會動的東西設定關鍵幀。沒有關鍵幀的軌道取預設值
- 需要正好落在節拍上的變化，使用`Constant`，例如在drop處切換主題
- 旋轉不會折回：0度的關鍵幀和720度的關鍵幀會讓物體轉兩圈

## 兩個關鍵幀之間

在第一個關鍵幀之前和最後一個關鍵幀之後，數值保持不變。在兩個關鍵幀之間，遊戲取已經過去的時間比例，讓它經過緩動處理，再混合兩個數值

這個比例按時間計算，而不是按繪製的幀計算。所以在30fps和144fps下曲線完全相同

**緩動屬於一對關鍵幀中較晚的那個**。關鍵幀的緩動決定從上一個關鍵幀到達它的這一段。所以軌道上第一個關鍵幀的緩動永遠不會顯現出來。新關鍵幀使用`Linear`

`{{ui:hint_editor_inspector_ease_header}}`欄位會開啟`{{ui:editor_search-title_ease}}`視窗，每種緩動都畫成各自的曲線。你可以選中多個關鍵幀，甚至是不同軌道上的關鍵幀，在一個撤銷步驟內一起修改

## 29種緩動

`Linear`是一條直線。`Constant`保持上一個數值，到關鍵幀時直接跳變

其餘27種分為九個系列，每個系列三種：`In`、`Out`和`InOut`。例如`InSine`、`OutSine`、`InOutSine`

| 系列 | 曲線形態 |
|---|---|
| `Sine` | 最柔和的曲線 |
| `Quad`、`Cubic`、`Quart`、`Quint` | 2、3、4、5次冪 |
| `Expo` | 指數 |
| `Circ` | 四分之一圓 |
| `Back` | 越過範圍後返回 |
| `Elastic` | 在目標值附近振盪 |

`In`開始慢、結束快。`Out`開始快、然後放緩。`InOut`兩端都慢。從`Sine`到`Expo`，每個系列都比前一個更陡

> [!caution] 注意
> `Back`和`Elastic`會超出範圍：`Out`會衝過目標，`In`會先反向越過起點。碰撞體隨物體一起移動。所以一顆本應停在安全區邊緣的子彈，會有幾幀進入安全區

## 隨機數值

關鍵幀中的數值不一定是單個數字：
- 數字：`{{ui:field_common_value}}`、`{{ui:enum_color-type_random-min-max}}`、`{{ui:enum_float-type_random-min-max-step}}`
- 向量（位置、縮放等）：`{{ui:field_common_value}}`、`{{ui:enum_vector-type_random-rect}}`、`{{ui:enum_vector-type_random-rect-step}}`、`{{ui:enum_vector-type_random-circle}}`、`{{ui:enum_color-type_random-lerp}}`、`{{ui:enum_vector-type_random-lerp-step}}`
- 顏色：`{{ui:field_common_value}}`、`{{ui:editor_events-timeline_track_theme}}`、`{{ui:enum_color-type_random-min-max}}`、`{{ui:enum_color-type_random-lerp}}`

`{{ui:enum_vector-type_random-rect}}`對每個軸分別取值。`{{ui:enum_color-type_random-lerp}}`對所有軸取同一個數，所以點會落在A和B之間的連線上。帶步長的變體會把結果向下取整到步長的倍數。步長為0時不使用網格，數值與不帶步長的變體相同。之後，這個關鍵幀和其他關鍵幀一樣進行混合

同一個種子得到同一個關卡。隨機數由種子、關鍵幀所在的幀、圖層、物體的起始幀、軌道和通道計算得出。更多：[[8_determinism]]

接下來：[[2_rhythm-and-structure|節奏與結構]]、[[6_themes|主題]]
