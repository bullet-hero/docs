---
title: 运行和扩展公共服务器
date: 2026-09-24
tags: [server_advanced]
---

# 运行和扩展公共服务器

开源SDK中已有哪些可用于Bullet Hero公共服务器的部分，以及哪些尚未确定：协议、API、审核工具

> [!warning] 警告
> 目前还没有服务器代码，也没有协议。下面是服务器将要运行的那部分SDK，它已经可以工作。这里没有服务器本身的端点、消息格式或API，因为它们还不存在

## SDK在服务器上运行

SDK是游戏的开放数据模型：模型、JSON和二进制序列化、校验规则、生成器。Unity编译的同一份源码也能构建为一个普通的`netstandard2.1`库，其中不含引擎。服务器或工具可以引用它：

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

包名为`BulletHero.SDK`。代码位于[github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)，采用MIT许可证

SDK版本通常与游戏版本一致，目前还不承诺API稳定。更多：[[5_versioning]]

**客户端和服务器对同样的模型运行同样的检查**。编辑器认为已就绪的关卡，在服务器上同样就绪。不存在需要保持同步的第二套规则

## ValidateForPublish

一次调用就能回答“这个关卡能否在这里发布”：

```csharp
ValidationFacade.ValidateForPublish(meta, profile, level, now, payload)
```

它一次执行三轮检查：

1. 针对关卡及其元数据的声明式规则
2. 针对关卡的图检查
3. 服务自己在`PublishProfile`中设定的条件

**关卡本身可以不传**。`metadata.json`是单独的文件，这样目录可以在不打开任何关卡的情况下评估成千上万个关卡。这一轮开销很小的检查覆盖了大部分策略

但有两项检查需要`level.json`：完全没有记录的资源，以及资源的获取方式。只针对元数据的报告干净，意思是“已读取的内容中没有问题”。在检查关卡文件之前，`IsReady`始终为`false`

`payload`携带测得的大小：每个资源、`level.json`、`metadata.json`以及整个关卡。没有它，就无法检查配置中的大小限制

检查过程中不会修复任何东西，这是有意为之。内容在发出途中被悄悄修改，是服务最不希望发生的事。更多：[[6_validation]]

## 三种结论

| 分组 | 含义 | 服务器的处理 |
|---|---|---|
| `Error` | 服务拒绝 | 拒绝上传（`HasErrors`） |
| `Warning` | 可以发布，但需要有人查看 | 将关卡放入审核队列（`NeedsManualReview`） |
| `Advice` | 已记录 | 不做处理 |

客户端在上传开始前就会因同样的错误阻止上传。你的服务器会拒绝的关卡，很少能真正送到它那里

## 你自己的PublishProfile

服务的策略是一个文件，即一个序列化的SDK模型。更严格或更宽松的服务器只是换一个文件，而不是分叉代码

**留在玩家设备上的关卡不做任何检查**。配置只在关卡被提交给某个服务的那一刻才起作用。作者如何为这一刻准备关卡：[[5_publish-readiness]]

预设：

| 预设 | 键 | 适用于 |
|---|---|---|
| `CreateOpen()` | `local` | 设备上的关卡，没有任何要求 |
| `CreateStandard()` | `standard` | 公共服务器，策略见[[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | 商店版，不允许直接URL，每个资源都要有哈希 |

主要字段：

| 字段 | 决定什么 |
|---|---|
| `AllowedLicenses` | 接受哪些常见许可证，为空则全部接受 |
| `AllowedUriTypes` | 资源可以如何获取，为空则全部允许 |
| `AllowUnknownLicense` | 资源是否可以不说明其使用条件 |
| `AllowPermissionInstead` | 权利人的许可能否替代被拒绝的许可证（总是送去审核） |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution` | 每条资源记录必须包含什么 |
| `RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 关卡必须声明什么 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | 大小限制，0表示不限 |
| `Sources`、`UnknownSourceTrust` | 可信网站名单，以及不在名单中的网站如何评级 |

两个公共预设：

| | `standard` | `strict` |
|---|---|---|
| 资源使用直接URL | 允许 | 禁止 |
| 每个资源都有署名 | 不要求 | 要求 |
| 每条记录都有内容哈希 | 不要求 | 要求 |
| 单个资源上限 | 64 MB | 32 MB |
| `level.json`或`metadata.json`上限 | 32 MB | 16 MB |
| 关卡上限 | 256 MB | 128 MB |
| 不在名单中的网站 | `RequiresLicenseCheck` | `RequiresResourceCheck` |

所有预设和字段：[[7_publish-profiles]]

### 为什么standard中没有GPL

`standard`中有意不包含GPL系列许可证。通过App Store再分发GPL作品会与Apple的条款冲突。允许这类许可证的目录，以后就无法提供给iOS

> [!info] 须知
> SDK自带的可信网站名单只是一个起点。网站会更改条款，因此每个运营者都应在自己的配置中覆盖它。任何东西都不能假定某个特定网站在名单中

## 审核

官方服务器计划在检查之上增加的内容。公共服务器很可能也需要这些：

- **审核队列**。由`Warning`类问题填充
- **举报和封禁**关卡与用户。Google Play和App Store的规则要求，凡是展示给其他人的内容都必须具备这两项
- **按哈希下架**。资源记录可以以`sha256:<hex>`的形式携带其文件的内容哈希。投诉会指明一部作品，有了哈希，就能通过查找而不是凭名称猜测找到所有带有它的关卡。编辑器在导入资源时会记录哈希
- **服务条款**。它们涵盖许可证不涵盖的内容：作者声明自己拥有权利、运营者删除关卡的权利、在列表中展示关卡名称和封面的权利

**Steam创意工坊的运作方式不同**。文件由Valve托管。官方只能在发布后对其评级，并决定游戏加载哪些内容

## 归档格式

关卡是一个装有文件的文件夹，归档包让它便于携带。SDK能读写的格式：

| 格式 | 读取 | 写入 | 说明 |
|---|---|---|---|
| `.tar.gz` | 是 | 是 | 默认格式 |
| `.zip` | 是 | 是 | 可以用AES-256逐项加密 |
| `.tar.gz.gpg`、`.zip.gpg` | 是 | 是 | 用口令保护的OpenPGP消息，是`.tar.gz`唯一能用的保护方式 |
| `level.json.gpg` | 是 | 是 | 单个受保护的关卡文件 |
| `.7z` | 否 | 否 | 能够识别，以便按名称明确拒绝 |

格式根据文件的开头字节判断，从不根据扩展名。文件名是任何人都能修改的部分

`tar -xzf`、`gpg -d`和任何zip解压工具都能打开所有可写入的格式。解包关卡不需要游戏。更多：[[4_archives]]

## 尚未确定的事

- 游戏与服务器之间的协议，以及OWS和NOWS是否使用同一个协议
- 服务器API：上传、目录、搜索、账号
- 如何让游戏指向某个社区服务器
- 服务器本身如何扩展，用什么语言
- 在服务器上一起游玩：传输、权威方、关卡同步和大厅

关于一起游玩，只确定了一件事：玩家的化身如何根据网络消息出现和消失

向任何服务发布关卡的功能，最早也要在`gv 1.0.0`之后的更新中才会推出。检查所依赖的数据必须在关卡发布前就记录在关卡中

## 关卡许可证与任何服务器

关卡默认以*CC BY-NC*授权，作者可以在关卡元数据中选择其他许可证。分享关卡的许可由作者直接授予每一位接收者。因此任何服务器，无论官方还是社区，都不得以商业方式托管*CC BY-NC*关卡

服务器即使采用不同许可证下的不同代码，也不会改变内容的任何权利。面向作者的完整规则：[[ugc-licensing-policy]]
