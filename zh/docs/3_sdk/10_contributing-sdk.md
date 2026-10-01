---
title: 参与SDK开发
date: 2026-10-01
tags: [developer]
---

# 参与SDK开发

SDK的问题请在bullet-hero/sdk仓库的issues中报告，代码修改也以拉取请求的形式提交到那里。贡献者规则位于同一个仓库中，就在代码旁边

仓库是[bullet-hero/sdk](https://github.com/bullet-hero/sdk)，默认分支为`master`

## 在哪里报告

| 关于什么 | 报告到哪里 |
|---|---|
| SDK及其代码 | [bullet-hero/sdk/issues](https://github.com/bullet-hero/sdk/issues) |
| 游戏：玩家的错误报告和建议 | [bullet-hero/releases/issues](https://github.com/bullet-hero/releases/issues) |
| 文档文本 | [bullet-hero/docs](https://github.com/bullet-hero/docs) |

## 规则在哪里

贡献者规则位于SDK仓库本身，就在它们所描述的代码旁边：

| 文件 | 内容 |
|---|---|
| [README.md](https://github.com/bullet-hero/sdk/blob/master/README.md) | 依赖、关卡包、构建DLL和包、检查示例 |
| [CLAUDE.md](https://github.com/bullet-hero/sdk/blob/master/CLAUDE.md) | 思维模型、文件夹索引以及整个库的约定 |
| 每个文件夹中的`CLAUDE.md` | 该文件夹的局部规则，例如[Serialization](https://github.com/bullet-hero/sdk/blob/master/Serialization/CLAUDE.md)、[Validations](https://github.com/bullet-hero/sdk/blob/master/Validations/CLAUDE.md)、[Publishing](https://github.com/bullet-hero/sdk/blob/master/Publishing/CLAUDE.md) |
| [Docs/VERSIONING.md](https://github.com/bullet-hero/sdk/blob/master/Docs/VERSIONING.md) | 版本轴、代、迁移和拒绝 |
| [Docs/IDENTIFIERS.md](https://github.com/bullet-hero/sdk/blob/master/Docs/IDENTIFIERS.md) | 模型如何寻址实体：Guid、int、帧、字段路径 |
| [[ugc-licensing-policy]]（在本网站上） | 用户内容的许可政策，与`TrustedSourceCatalog`一起修改 |
| [Versions/README.md](https://github.com/bullet-hero/sdk/blob/master/Versions/README.md) | 如何编写快照和迁移器 |
| [Generators/README.md](https://github.com/bullet-hero/sdk/blob/master/Generators/README.md) | 生成器约定 |
| [Roslyn/README.md](https://github.com/bullet-hero/sdk/blob/master/Roslyn/README.md) | 分析器和模型生成器，以及如何重新构建它们 |
| [UnityIntegration/README.md](https://github.com/bullet-hero/sdk/blob/master/UnityIntegration/README.md) | 双重编译约定 |
| [CHANGELOG.md](https://github.com/bullet-hero/sdk/blob/master/CHANGELOG.md) | 按`sv`版本列出的变更，顶部是`[Unreleased]`部分 |

## 构建和测试

```bash
dotnet build -c Release BH.SDK.csproj
dotnet test Tests/BH.SDK.Tests.csproj
dotnet pack -c Release BH.SDK.csproj
```

- 这里在没有Unity的情况下构建Unity所编译的同一份源码。破坏无引擎约定的文件会让这次构建失败
- 输出到`bin~`和`obj~`
- 打包命令只生成`.nupkg`。仓库不会向nuget.org推送任何东西

> [!caution] 注意
> 分析器和模型生成器以预先构建好的`BH.SDK.Roslyn.dll`形式放在SDK根目录。修改`Roslyn/`中的任何内容后，请重新构建并复制它。否则旧的生成器会继续运行，尽管源码已经不同

```bash
cd Roslyn
dotnet build BH.SDK.Roslyn.csproj -c Release
cp bin~/Release/BH.SDK.Roslyn.dll ../BH.SDK.Roslyn.dll
dotnet test Tests~/BH.SDK.Roslyn.Tests.csproj -c Release
```

在Unity编辑器中，菜单项**Tools > BH.SDK.Roslyn > Build Analyzer**完成同样的操作

## 值得提前了解的不变量

- 核心不引用任何`UnityEngine`类型。需要引擎的代码放到`UnityExtensions/`，或放到`UnityIntegration/`中`#if BHSDK_UNITY`之后，并提供不依赖引擎的分支
- 代码对文件和内存中的数据同样适用，只使用BCL中的异步机制
- `netstandard2.1`和C# 9是Unity项目编译时使用的版本。不会提高它们
- 模型是`[GenerateModel] public sealed partial class`。每个可序列化字段都从`Names.cs`中取得自己的键
- 任何模型变化都是带有快照和迁移器的新一代。更多：[[5_versioning]]
- SDK版本存放在三个地方：`SdkVersion.cs`、`package.json`和`BH.SDK.csproj`中的`<Version>`。只要其中一个单独变动，`SdkVersionAgreementTests`就会失败
