---
title: 发布配置
date: 2026-09-24
tags: [developer, level_author]
---

# 发布配置

服务如何声明自己接受哪些关卡，这些规则写成数据文件而不是代码

## 发布配置就是数据

发布配置（`PublishProfile`）描述一个服务接受哪些关卡。它是一个模型，像其他根一样序列化，有自己的代。接入一个新服务意味着写一个文件，而不是修改分析器

关卡可以发往Steam创意工坊、官方服务器、社区服务器、商店版本的目录。每个地方对同样的问题给出不同的答案。答案会随着年份改变，代码不会

发布配置决定的内容：

| 字段 | 含义 |
|---|---|
| `ProfileKey` | 这是哪个服务，在每份报告中重复出现 |
| `AllowedLicenses` | 服务接受的`TypicalLicenseType`值 |
| `AllowedUriTypes` | 允许以哪些方式获取资源。为空表示任何方式 |
| `AllowUnknownLicense`、`AllowPermissionInstead` | 未知许可证或书面许可是否足够 |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution`、`RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 哪些内容必须填写 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | 大小限制，0表示不限 |
| `Sources`、`UnknownSourceTrust` | 网站名单，以及名单外网站的评级 |

哪些许可证可以接受只由发布配置决定。它看起来像许可证的属性，实际上是接收服务的属性

## 四个内置配置

| 工厂方法 | `ProfileKey` | 用途 |
|---|---|---|
| `CreateOpen()` | `local` | 你自己设备上的关卡。什么都不要求 |
| `CreateStandard()` | `standard` | 公共服务器 |
| `CreateWorkshop()` | `workshop` | Steam创意工坊。所有 CC BY 变体都能通过，缺少文件只产生警告 |
| `CreateStrict()` | `strict` | 商店版本，比`standard`更严格 |

| 项目 | `standard` | `strict` |
|---|---|---|
| 许可证 | CC0 1.0、CC BY 4.0和3.0、CC BY-NC 4.0和3.0、SIL OFL 1.1、MIT、Apache 2.0、the Unlicense | 同`standard` |
| 资源来源 | 关卡文件夹、游戏或直接URL | 不允许URL |
| 署名和哈希 | - | 必需 |
| 单个资源上限 | 64 MiB | 32 MiB |
| 单个数据文件上限 | 32 MiB | 16 MiB |
| 单个关卡上限 | 256 MiB | 128 MiB |

> [!tip] 建议
> 不要为自己的服务新增工厂方法。从这四个中选一个，修改需要的字段，然后以JSON文件的形式发布

### 为什么是这些许可证和大小

- `standard`不包含GPL系列许可证。通过App Store再分发GPL作品会与Apple的条款冲突
- 不包含CC BY-SA：ShareAlike会强制改变关卡本身的许可证
- 不包含CC BY-ND：NoDerivatives禁止修改，而游戏正是围绕修改而设计的
- `strict`的大小限制是手机通过移动网络能够下载的量

## 资源从哪里来

许可证字段说明的是作者的声明。`SourceTrust`说明结合资源来源网站，这个声明有多可信：

| 评级 | 结果 | 示例 |
|---|---|---|
| `Approved` | 发布 | Kenney、ccMixter、Incompetech |
| `PartiallyApproved` | 发布，但记录值得看一眼 | Pixabay、SoundImage |
| `RequiresLicenseCheck` | 对照实际页面核对许可证 | OpenGameArt、Free Music Archive、Wikimedia Commons |
| `RequiresResourceCheck` | 先确认作品本身 | Rawpixel、itch.io |
| `NotAllowed` | 拒绝 | YouTube、SoundCloud、Spotify |
| `Unknown` | 没有记录，由`UnknownSourceTrust`决定 | - |

`TrustedSourceCatalog.CreateDefault()`返回25个网站。这只是一份初始名单，每个运营者都应当修改它。所以任何代码都不能假定某个条目一定存在

`Sources`列表为空时，不对来源评级

流媒体平台被列为`NotAllowed`，而不是省略。名单外的网站由`UnknownSourceTrust`评级，而在`standard`和`strict`中，这个评级要求检查而不是拒绝

这份名单与[[ugc-licensing-policy]]描述的是同一件事，两者一起修改

## 如何处理结果

调用的方法是`ValidationFacade.ValidateForPublish`。更多：[[6_validation]]

`PublishReadinessReport`包含：
- `HasErrors`：`Error`组的问题
- `NeedsManualReview`：`Warning`组的问题
- `IsReady`

接下来怎么做不由发布配置决定。客户端遇到错误时阻止上传。服务器则把关卡放进审核队列，而不是直接发布

同一检查在作者一侧的样子：[[5_publish-readiness]]
