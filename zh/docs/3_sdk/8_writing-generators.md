---
title: 编写生成器
date: 2026-09-24
tags: [developer]
---

# 编写生成器

如何用SDK的基类构建生成器，以及它要在编辑器中正常工作必须遵守什么

生成器根据几个参数生成关卡内容。作者不必亲手放置每一个物体

添加生成器就是添加一个类。宿主根据约定构建它的表单、估算和撤销。没有人为它写界面，也不需要编辑任何列表

内置生成器能做什么：[[8_generators]]

## 三种类型

| 类型 | 产出 | 基类 | 入口 |
|---|---|---|---|
| `Level` | 新的`Level`和`LevelMeta` | `BaseLevelGenerator<TParams>` | `Create(parameters)` |
| `Content` | 在当前作用域中新增物体和资源 | `BaseContentGenerator<TParams>` | `Run(context, parameters)` |
| `Modifier` | 修改已存在的物体 | `BaseModifier<TParams>` | `Run(context, parameters)` |

Content和Modifier共用同一个入口。它们的区别在于意图和`GeneratorRequirements`。修改器默认要求有选中项

对于生成物体的生成器，有`BaseSpawnGenerator<TParams>`。它负责创建每个物体、设置父级并放到时间上。具体的类只需要处理摆放的数学计算

## 没有注册表

`GeneratorRegistry`在第一次被访问时通过反射找到所有生成器。两个生成器的`NameKey`相同会当场失败

只扫描SDK自身的程序集。所以新的生成器放在SDK仓库中，以拉取请求的形式加入。更多：[[10_contributing-sdk]]

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

    // Spawn adds a size key and a colour key, AddPosition adds the third
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

`NameKey`的形式是本地化键。宿主通过自己的字符串表显示名称

## 必须遵守的规则

- **只通过`GeneratorContext`修改关卡**（`Create`、`Edit`、`Delete`、`SetValue`等）。它把每次改动记录到`GeneratorChangeLog`中，撤销完全依赖于它。直接操作模型能通过编译，却会悄悄破坏撤销
- **每个字段都列在某个分组中，每个数字都有`Range`**。反射得到的字段顺序没有保证。数字没有边界时，宿主就无法对它钳制。有测试强制检查范围
- **参数是公开的可变字段，并有无参构造函数**。表单绑定到它们，预设序列化它们。不要遮蔽继承的字段：一切都以字段名为键
- **估算与实际运行一致**。宿主在运行前显示估算。如果运行会超出`LevelRules.MaxObjects`，宿主会拒绝运行
- **随机性来自`context.CreateRandom()`**，而不是`System.Random`。同一个种子在任何运行环境上都生成相同的关卡
- **把创建的内容挂到`context.Parent`下**。宿主正是这样把一次运行的全部内容归为一个物体
- 如果访问`context.Game`或`context.Audio`，**声明`GeneratorRequirements.LevelScope`**。当前作用域是预制件时，两者都为`null`
- 当某种参数组合会删除或改写作者当前所看窗口之外的内容时，**重写`IsDangerousTyped`**。宿主随后会请求确认

## 外部数据

SDK没有音频解码器、FFT或图片加载器。需要这类数据的生成器：
1. 声明`GeneratorRequirements.ExternalAnalysis`
2. 实现`External/`中的接口：`IWaveformInput`、`IBeatFramesInput`、`IPixelTextureInput`等

宿主在运行前填好数据。没有拿到任何数据时，生成器必须什么也不生成

完整的约定见[Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md)
