---
title: 安装
date: 2026-10-02
tags: [developer, level_author]
---

# 安装

SDK就是nuget.org上的BulletHero.SDK包，也可以从源码构建。在Unity中以git submodule接入，ConsoleSmoke示例用来确认你的关卡能被读取

SDK的代码位于[github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)。许可证为MIT

## .NET

`BulletHero.SDK`包已发布到nuget.org：`dotnet add package BulletHero.SDK`。三个依赖会随它一起到位。如需从源码构建：

```bash
git clone https://github.com/bullet-hero/sdk.git
cd sdk
dotnet build -c Release BH.SDK.csproj   # bin~/Release/BH.SDK.dll and BH.SDK.xml
dotnet pack  -c Release BH.SDK.csproj   # bin~/Release/BulletHero.SDK.<version>.nupkg
```

然后二选一接入：
- 从本地文件夹引用`.nupkg`：`dotnet add package BulletHero.SDK --source <folder>`。三个依赖会随它一起到位
- 直接引用`BH.SDK.dll`。这时下面三个包需要自己添加：对DLL的引用不会带上它的依赖

依赖全部来自NuGet：

| 包 | 版本 | 用途 |
|---|---|---|
| `Newtonsoft.Json` | 13.0.3 | JSON |
| `BouncyCastle.Cryptography` | 2.7.0 | 为带密码的关卡提供OpenPGP |
| `SharpZipLib` | 1.4.2 | tar和zip（gzip来自BCL） |

### 构建细节

- 程序集名为`BH.SDK.dll`，旁边附有XML文档
- 目标框架是`netstandard2.1`，语言是C# 9。这与Unity项目的版本相同，所以同一份源码既能在Unity中构建，也能脱离Unity构建
- 输出文件夹是`bin~`和`obj~`。需要波浪号，是因为Unity不导入名称以波浪号结尾的文件夹

## Unity

游戏以git submodule的方式接入SDK：

```bash
git submodule init
git submodule add -f https://github.com/bullet-hero/sdk.git Assets/Plugins/BH.SDK
```

移除用`git rm -r -f Assets/Plugins/BH.SDK`

Unity项目需要自己提供：
- `Newtonsoft.Json`，通过`com.unity.nuget.newtonsoft-json`包
- 来自NuGet的`BouncyCastle.Cryptography`和`SharpZipLib`（游戏用NuGetForUnity安装它们）
- Player Settings中的脚本宏`BHSDK_UNITY`。没有它，`UnityIntegration`会选择不依赖引擎的分支
- 位于SDK根目录的`BH.SDK.Roslyn.dll`。Unity只把分析器应用到它所在文件夹的程序集以及引用该程序集的程序集。挪到别处后，它什么也不分析

仓库根目录有一个`package.json`，名称为`com.vertoker.bullet-hero-sdk`，最低Unity版本为`6000.0`。因此Package Manager也能通过git URL添加SDK。这种方式没有使用，这里也不介绍

## 检查：ConsoleSmoke示例

`Samples~/ConsoleSmoke`是一个`net8.0`控制台应用。它引用构建好的`BH.SDK.dll`，和第三方工具的做法完全一样。该应用读取一个关卡文件夹，输出名称、物体数量和代。然后让关卡经JSON和`.blob`各往返一次

```bash
dotnet build -c Release Samples~/ConsoleSmoke/ConsoleSmoke.csproj
dotnet Samples~/ConsoleSmoke/bin~/Release/net8.0/ConsoleSmoke.dll <level folder>
```

| 退出码 | 含义 |
|---|---|
| 0 | 全部一致 |
| 1 | 参数错误 |
| 2 | 找不到`level.*`或`metadata.*` |
| 3 | 往返结果不一致 |
| 4 | 文件比当前SDK新 |

在游戏内置关卡`new-zero-demo`上的输出（用`sv 1.0.0`录制）：

```
BH.SDK 1.0.0, model generation 1
name:       New zero demo
objects:    782
generation: 1 (Blob)
round trip Json: equal (1505078 bytes)
round trip Blob: equal (680706 bytes)
exit 0
```

下一步：[[2_level-format]]

## SDK的组成

| 部分 | 是什么 | 是否需要Unity |
|---|---|---|
| `BH.SDK` | 核心：模型、序列化、版本、规则、校验、归档包、发布、生成器、与Afterbeat互通 | 否 |
| `UnityIntegration` | 一个薄层，其中每个文件在有无Unity时都能编译（`#if BHSDK_UNITY`），例如`Cat`日志器 | 否：在Unity之外它直接编译进核心 |
| `UnityExtensions` | 到Unity类型的转换、2D变换、化身移动 | 是，始终需要 |
| `BH.SDK.Roslyn` | 分析器和源码生成器。它为每个带有`[GenerateModel]`的模型编写`Equals`、复制、JSON与`.blob`编解码器以及校验遍历 | 在编译期运行 |

模型文件只包含它的字段和构造函数。所有重复的部分都由生成器编写。所以不会在七个生成的方法体中的某一个里漏掉字段

## 为什么是独立的库

- **关卡比游戏活得久**。关卡是一个由开放格式文件组成的文件夹（JSON、tar.gz、zip、OpenPGP）。读取它们的代码也是开源的。即使写出关卡的游戏不在了，关卡依然可读
- **与其他节奏游戏互通**。与*Afterbeat*（原名*Project Arrhythmia*）之间的双向转换已经在SDK中。更多：[[9_afterbeat-interop]]
- **修复更快**。格式的缺陷从外部就能看到。任何读代码的人都能报告它或提交修复
- **第三方工具**。转换器、校验器、关卡生成器或模组使用与游戏相同的模型。不需要从文件中还原它们
- **服务器**。核心不依赖Unity，以`netstandard2.1`构建。所以服务器能在同样的模型上执行与客户端相同的检查
