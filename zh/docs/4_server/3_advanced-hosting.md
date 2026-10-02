---
title: 公共服务器及其扩展
date: 2026-10-02
tags: [server_advanced]
---

# 公共服务器及其扩展

公共服务器已经可以使用开源SDK：与客户端相同的模型和检查可以脱离Unity构建。协议、服务器API和审核工具目前尚未确定

> [!warning] 警告
> 目前还没有服务器代码和协议。下面介绍的是服务器将要依托的那部分SDK，它已经可以工作。这里没有地址、消息格式和服务器本身的API，因为它们还不存在

## SDK可以在服务器上运行

SDK是游戏的开源数据模型：模型、序列化为JSON和二进制格式、校验规则、生成器。Unity编译的同一份源码可以脱离引擎构建为普通的`netstandard2.1`库。服务器或工具程序可以引用它：

```bash
dotnet build -c Release BH.SDK.csproj
dotnet pack  -c Release BH.SDK.csproj
```

包名为`BulletHero.SDK`。代码位于[github.com/bullet-hero/sdk](https://github.com/bullet-hero/sdk)，采用MIT许可证

SDK的版本通常与游戏版本一致，目前还不承诺API稳定。更多：[[5_versioning]]

**客户端和服务器在同样的模型上执行同样的检查**。编辑器认为已就绪的关卡，对服务器来说也已就绪。不存在需要保持一致的第二套规则

## ValidateForPublish

一次调用回答“这个关卡能否在这里发布”：

```csharp
new ValidationFacade().ValidateForPublish(meta, profile, level, now, payload)
```

它一次执行三遍检查：

1. 针对关卡及其元数据的声明式规则
2. 关卡图的检查
3. 服务在自己的`PublishProfile`中设定的条件

**关卡本身可以不传入**。`metadata.json`是单独的文件，这样目录无需打开任何一个关卡就能评估成千上万个关卡。这一遍低成本的检查覆盖了大部分策略

但有两项检查需要`level.json`：完全没有记录的资源，以及资源的获取方式。只根据元数据得到的干净报告意味着“已读取的部分没有错误”。在关卡文件检查之前，`IsReady`保持为`false`

`payload`携带测得的大小：每个资源、`level.json`、`metadata.json`以及整个关卡的大小。没有它，就无法检查配置的大小限制

检查期间不修复任何东西，这是有意为之。在输出端悄悄修改内容，是服务最不需要的。更多：[[6_validation]]

## 三种结论

| 组 | 含义 | 服务器做什么 |
|---|---|---|
| `Error` | 服务拒绝 | 拒绝上传（`HasErrors`） |
| `Warning` | 可以发布，但需要人工查看 | 把关卡放入审核队列（`NeedsManualReview`） |
| `Advice` | 已记录 | 不做任何事 |

客户端在上传开始之前就会因同样的错误阻止上传。会被你的服务器拒绝的关卡很少能到达服务器

## 自己的PublishProfile

服务的策略是一个文件，即序列化的SDK模型。更严格或更宽松的服务器只是另一个文件，而不是代码的分支

**留在玩家设备上的关卡完全不检查**。配置只在关卡提交给服务的那一刻才起作用。作者如何为这一刻准备关卡：[[5_publish-readiness]]

预设：

| 预设 | 键 | 用途 |
|---|---|---|
| `CreateOpen()` | `local` | 设备上的关卡，没有任何要求 |
| `CreateStandard()` | `standard` | 公共服务器，策略来自[[ugc-licensing-policy]] |
| `CreateStrict()` | `strict` | 商店版，不允许直接链接，每个资源都要有哈希 |

主要字段：

| 字段 | 决定什么 |
|---|---|
| `AllowedLicenses` | 接受哪些典型许可证，空列表表示全部接受 |
| `AllowedUriTypes` | 资源可以通过哪些方式获取，空列表表示允许所有方式 |
| `AllowUnknownLicense` | 资源能否对自己的条款什么都不说明 |
| `AllowPermissionInstead` | 权利人的许可能否代替被拒绝的许可证（总是送去审核） |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution` | 每个资源的记录必须包含什么 |
| `RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 关卡必须声明什么 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | 大小限制，零表示不限制 |
| `Sources`、`UnknownSourceTrust` | 可信网站列表，以及如何评级列表之外的网站 |

两个公共预设：

| | `standard` | `strict` |
|---|---|---|
| 资源的直接链接 | 允许 | 禁止 |
| 每个资源注明作者 | 不要求 | 要求 |
| 每条记录中的内容哈希 | 不要求 | 要求 |
| 最大的资源 | {{v:publish.standard.max-resource-mb}}MB | {{v:publish.strict.max-resource-mb}}MB |
| 最大的`level.json`或`metadata.json` | {{v:publish.standard.max-data-file-mb}}MB | {{v:publish.strict.max-data-file-mb}}MB |
| 最大的关卡 | {{v:publish.standard.max-level-mb}}MB | {{v:publish.strict.max-level-mb}}MB |
| 列表之外的网站 | `RequiresLicenseCheck` | `RequiresResourceCheck` |

全部预设和字段：[[7_publish-profiles]]

### 为什么standard中没有GPL

`standard`中特意不包含GPL系列许可证。通过App Store分发的GPL作品与Apple的条款冲突。允许它们的目录以后就无法在iOS上提供

> [!info] 须知
> SDK自带的可信网站列表只是一个起点。网站会改变自己的条款，所以每个服务器所有者都应当在自己的配置中覆盖它。任何东西都不能指望某个特定网站一定在列表中

## 审核

官方服务器计划在检查之上增加的内容。公共服务器很可能也需要这些：

- **审核队列**。由`Warning`组的问题填充
- **举报和封禁**关卡与用户。Google Play和App Store的规则对任何其他人能看到的内容都要求这两项
- **按哈希删除**。资源记录可以以`sha256:<hex>`的形式保存其文件的内容哈希。举报会指明某件作品，有了哈希，包含它的每个关卡都能通过搜索找到，而不是靠名称猜测。编辑器在导入资源时记录哈希
- **使用条款**。它们涵盖许可证没有涵盖的内容：作者声明自己拥有权利，服务器所有者删除关卡的权利，在列表中显示关卡名称和封面的权利

**Steam创意工坊的方式不同**。文件由Valve存储，Bullet Hero一侧没有审核队列。游戏在上传前检查关卡或合集，出现错误就阻止上传：[[17_publishing]]。发布之后，游戏只决定从中下载哪些内容

## 归档包格式

关卡是一个装有文件的文件夹，归档包让它便于携带。SDK读取和写入的格式：

| 格式 | 读取 | 写入 | 说明 |
|---|---|---|---|
| `.tar.gz` | 是 | 是 | 默认 |
| `.zip` | 是 | 是 | 可以按条目用AES-256加密 |
| `.tar.gz.gpg`、`.zip.gpg` | 是 | 是 | 带密码的OpenPGP消息，是`.tar.gz`唯一可用的保护方式 |
| `level.json.gpg` | 是 | 是 | 单个受保护的关卡文件 |
| `.7z` | 否 | 否 | 识别它是为了用清楚的名称拒绝 |

格式根据文件开头的字节判断，而不是根据扩展名。名称是文件中唯一任何人都能修改的部分

`tar -xzf`、`gpg -d`和任何zip压缩工具都能打开所有写入的格式。解压关卡不需要游戏。更多：[[4_archives]]

## 尚未确定的事

- 游戏与服务器之间的协议，以及OWS和NOWS是否使用同一个协议
- 服务器API：上传、目录、搜索、账号
- 如何让游戏指向社区服务器
- 服务器本身如何扩展，用什么语言扩展
- 在服务器上一起游玩：传输、权威、关卡同步和大厅

关于一起游玩，只想清楚了一件事：玩家的化身如何根据网络消息出现和消失

向任何服务发布关卡的功能最早也要在`gv 1.0.0`之后的更新中出现。检查所依赖的数据必须在关卡发布之前就进入关卡

## 关卡许可证与任何服务器

关卡默认以*CC BY-NC*发布，作者可以在关卡元数据中选择其他许可证。分享关卡的许可直接从作者授予每位接收者。所以任何服务器，无论官方还是社区，都不能以商业方式托管*CC BY-NC*下的关卡

采用不同代码和不同许可证的服务器，不会改变内容的任何权利。面向作者的完整规则：[[ugc-licensing-policy]]
