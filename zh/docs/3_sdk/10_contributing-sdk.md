---
title: 参与SDK开发
date: 2026-09-24
tags: [developer]
---

# 参与SDK开发

在哪里报告问题，SDK给贡献者的规则写在哪里，以及如何构建、测试和打包

SDK是一个独立的仓库：[bullet-hero/sdk](https://github.com/bullet-hero/sdk)，默认分支为`master`。对SDK代码的修改以拉取请求的形式提交到那里

## 在哪里报告

| 关于 | 去哪里 |
|---|---|
| SDK及其代码 | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| 游戏：玩家的错误报告和需求 | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| 文档文本 | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## 规则写在哪里

给贡献者的规则就放在SDK仓库里，紧挨着它们所描述的代码：

| 文件 | 内容 |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | 依赖、关卡包、构建DLL和包、冒烟测试示例 |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | 整个库的心智模型、文件夹索引和约定 |
| 每个文件夹中的`CLAUDE.md` | 该文件夹的局部规则，例如[Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md)、[Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md)、[Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | 版本维度、代、迁移和拒绝读取 |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | 模型如何定位事物：Guid、int、帧、字段路径 |
| [[ugc-licensing-policy]]（本站） | 用户内容的许可政策，与`TrustedSourceCatalog`一起修改 |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | 如何编写快照和迁移器 |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | 生成器约定 |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | 分析器和模型生成器，以及如何重新构建它们 |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | 双重编译约定 |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | 按`sv`版本列出的变更，顶部有`[Unreleased]`部分 |

## 构建和测试

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- Unity编译的同一份源码在这里不依赖Unity即可构建。破坏无引擎约定的文件会让这次构建失败
- 输出到`bin~`和`obj~`
- 打包命令只生成`.nupkg`。仓库不会向nuget.org推送任何东西

> [!caution] 注意
> 分析器和模型生成器以预先构建好的`BH.SDK.Roslyn.dll`放在SDK根目录中。修改`Roslyn/`下的任何内容后，都要重新构建并复制它。否则旧的生成器会继续运行，与源码所写的不一致

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

在Unity编辑器中，菜单项**Tools > BH.SDK.Roslyn > Build Analyzer**完成同样的操作

## 值得先了解的不变量

- 核心不引用任何`UnityEngine`类型。需要引擎的代码放到`UnityExtensions/`，或放到`UnityIntegration/`中`#if BHSDK_UNITY`之后，并提供不依赖引擎的分支
- 代码对文件和内存数据同样适用，并且只使用BCL的异步
- `netstandard2.1`和C# 9是Unity项目编译时使用的版本，不会提高
- 模型是`[GenerateModel] public sealed partial class`。每个序列化成员的键都取自`Names.cs`
- 对模型的任何修改都是新的一代，并配有快照和迁移器。更多：[[5_versioning]]
- SDK版本存放在三个地方：`SdkVersion.cs`、`package.json`和`BH.SDK.csproj`中的`<Version>`。只改动其中一处时，`SdkVersionAgreementTests`会失败
