---
title: 编写生成器
date: 2026-10-02
tags: [developer]
---

# 编写生成器

生成器是继承SDK基类的一个类：BaseLevelGenerator、BaseContentGenerator或BaseModifier。表单、开销估算和撤销由宿主根据约定自行构建

生成器根据几个参数创建关卡内容。作者无需手动摆放每个物体

没有人为生成器编写界面，也不需要修改任何列表

内置生成器的作用：[[8_generators]]

## 三种类型

| 类型 | 创建什么 | 基类 | 入口 |
|---|---|---|---|
| `Level` | 新的`Level`和`LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | 活动范围内的新物体和资源 | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | 对已有物体的编辑 | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content和Modifier的入口相同。它们的区别在于意图和`GeneratorRequirements`。修改器默认需要选中项

对于创建物体的生成器，有`BaseSpawnGenerator<TParams>`。它创建每个物体，设置父级并在时间上摆放。具体的类只需负责摆放的数学计算

## 没有注册表

`GeneratorRegistry`在第一次访问时通过反射找到所有生成器。两个`NameKey`相同的生成器会当场失败

只扫描SDK自己的程序集。所以新的生成器放在SDK仓库中，通过拉取请求提交。更多：[[9_contributing-sdk]]

## 示例

一排物体，基于与内置`RadialGenerator`相同的类构建：

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

`NameKey`采用本地化键的形式。宿主通过自己的字符串表显示名称

## 必须遵守的规则

- **只通过`GeneratorContext`修改关卡**（`Create`、`Edit`、`Delete`、`SetValue`等）。它把每次修改记录到`GeneratorChangeLog`中，整个撤销功能都依赖于此。直接修改模型能够编译，却会悄无声息地破坏撤销
- **每个字段都列在某个分区中，每个数字都有`Range`**。反射得到的字段顺序没有保证。没有边界的数字让宿主无从钳制。范围由测试检查
- **参数是公开的可变字段，并有无参构造函数**。表单绑定到它们，预设会序列化它们。不要隐藏继承来的字段：一切都按字段名寻址
- **估算与实际运行一致**。宿主在运行前显示估算。如果运行会超过`LevelRules.MaxObjects`，宿主会拒绝
- **随机性来自`context.CreateRandom()`**，而不是`System.Random`。同一个种子在任何平台上都生成同一个关卡
- **把创建的内容挂到`context.Parent`下**。宿主借此把整次运行收拢为一个物体
- **如果用到`context.Game`或`context.Audio`，请声明`GeneratorRequirements.LevelScope`**。活动范围是预制件时，二者都为`null`
- **如果某种参数组合会删除或改写作者正在查看的窗口之外的内容，请重写`IsDangerousTyped`**。这样宿主会请求确认

## 外部数据

SDK中没有音频解码器、FFT和图片加载器。需要这类数据的生成器：
1. 声明`GeneratorRequirements.ExternalAnalysis`
2. 实现`External/`中的接口：`IWaveformInput`、`IBeatFramesInput`、`IPixelTextureInput`等

宿主在运行前填入数据。如果没有收到任何数据，生成器必须什么都不创建

完整的约定：[Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
