---
title: 編寫生成器
date: 2026-10-02
tags: [developer]
---

# 編寫生成器

生成器是繼承SDK基類的一個類：BaseLevelGenerator、BaseContentGenerator或BaseModifier。表單、開銷估算和撤銷由宿主根據約定自行構建

生成器根據幾個引數建立關卡內容。作者無需手動擺放每個物體

沒有人為生成器編寫介面，也不需要修改任何列表

內建生成器的作用：[[8_generators]]

## 三種類型

| 型別 | 建立什麼 | 基類 | 入口 |
|---|---|---|---|
| `Level` | 新的`Level`和`LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | 活動範圍內的新物體和資源 | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | 對已有物體的編輯 | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content和Modifier的入口相同。它們的區別在於意圖和`GeneratorRequirements`。修改器預設需要選中項

對於建立物體的生成器，有`BaseSpawnGenerator<TParams>`。它建立每個物體，設定父級並在時間上擺放。具體的類只需負責擺放的數學計算

## 沒有登錄檔

`GeneratorRegistry`在第一次訪問時通過反射找到所有生成器。兩個`NameKey`相同的生成器會當場失敗

只掃描SDK自己的程式集。所以新的生成器放在SDK倉庫中，通過拉取請求提交。更多：[[9_contributing-sdk]]

## 示例

一排物體，基於與內建`RadialGenerator`相同的類構建：

```csharp
using BH.SDK.Generators;
using BH.SDK.Generators.Spawn;
using BH.SDK.Rules;

public class RowGenerator : BaseSpawnGenerator<RowGenerator.Parameters>
{
    public override string NameKey => "gen_geometry_row";

    public override GeneratorHints Hints { get; } = new GeneratorHints.Builder()
        .Section(GeneratorSections.Main, SpawnParameters.MainFields)
        .Section(GeneratorSections.Main, nameof(Parameters.Count), nameof(Parameters.Spacing))
        .Section(GeneratorSections.Additional, SpawnParameters.AdditionalFields)
        .Section(GeneratorSections.Additional, nameof(Parameters.StartX), nameof(Parameters.Y))
        .Range(nameof(Parameters.Count), 1, 256)
        .Range(nameof(Parameters.Spacing), 0f, ValueRules.MaxPos)
        .Range(nameof(Parameters.StartX), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(Parameters.Y), ValueRules.MinPos, ValueRules.MaxPos)
        .Range(nameof(SpawnParameters.Size), ValueRules.MinSca, ValueRules.MaxSca)
        .Build();

    protected override void Generate(GeneratorContext context, Parameters parameters)
    {
        for (var i = 0; i < parameters.Count; i++)
        {
            var obj = Spawn(context, parameters, $"row_{i}", context.Span);
            AddPosition(obj, parameters.StartX + i * parameters.Spacing, parameters.Y, obj.Span.StartFrame);
        }
    }

    // Spawn adds a size key and a color key, AddPosition adds the third
    protected override GeneratorCost EstimateTyped(GeneratorContext context, Parameters parameters)
        => new GeneratorCost(parameters.Count, parameters.Count * 3);

    public class Parameters : SpawnParameters
    {
        public int Count = 8;
        public float Spacing = 2f;
        public float StartX;
        public float Y;
    }
}
```

`NameKey`採用本地化鍵的形式。宿主通過自己的字串表顯示名稱

## 必須遵守的規則

- **只通過`GeneratorContext`修改關卡**（`Create`、`Edit`、`Delete`、`SetValue`等）。它把每次修改記錄到`GeneratorChangeLog`中，整個撤銷功能都依賴於此。直接修改模型能夠編譯，卻會悄無聲息地破壞撤銷
- **每個欄位都列在某個分割槽中，每個數字都有`Range`**。反射得到的欄位順序沒有保證。沒有邊界的數字讓宿主無從鉗制。範圍由測試檢查
- **引數是公開的可變欄位，並有無參建構函式**。表單繫結到它們，預設會序列化它們。不要隱藏繼承來的欄位：一切都按欄位名定址
- **估算與實際執行一致**。宿主在執行前顯示估算。如果執行會超過`LevelRules.MaxObjects`，宿主會拒絕
- **隨機性來自`context.CreateRandom()`**，而不是`System.Random`。同一個種子在任何平臺上都生成同一個關卡
- **把建立的內容掛到`context.Parent`下**。宿主藉此把整次執行收攏為一個物體
- **如果用到`context.Game`或`context.Audio`，請宣告`GeneratorRequirements.LevelScope`**。活動範圍是預製件時，二者都為`null`
- **如果某種引數組合會刪除或改寫作者正在檢視的視窗之外的內容，請重寫`IsDangerousTyped`**。這樣宿主會請求確認

## 外部資料

SDK中沒有音訊解碼器、FFT和圖片載入器。需要這類資料的生成器：
1. 宣告`GeneratorRequirements.ExternalAnalysis`
2. 實現`External/`中的介面：`IWaveformInput`、`IBeatFramesInput`、`IPixelTextureInput`等

宿主在執行前填入資料。如果沒有收到任何資料，生成器必須什麼都不建立

完整的約定：[Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
