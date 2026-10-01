---
title: 发布配置
date: 2026-10-01
tags: [developer, level_author]
---

# 发布配置

服务用PublishProfile文件描述自己接受哪些关卡：许可证、资源来源、必填字段、大小限制。新增一个服务就是写一个文件，而不是修改分析器

## 配置就是数据

发布配置（`PublishProfile`）是一个模型，与其他任何根一样序列化，有自己的代

关卡可以进入Steam创意工坊、官方服务器、社区服务器、商店版的目录。每个地方对同样的问题都有自己的回答。这些回答会随着年份变化，而代码不会

配置决定的内容：

| 字段 | 含义 |
|---|---|
| `ProfileKey` | 这是哪个服务，在每份报告中重复出现 |
| `AllowedLicenses` | 服务接受的`TypicalLicenseType`值 |
| `AllowedUriTypes` | 资源可以通过哪些方式获取。空列表表示任何方式 |
| `AllowUnknownLicense`、`AllowPermissionInstead` | 未知许可证或书面许可是否足够 |
| `RequireResourceMeta`、`RequireResourceUrl`、`RequireAttribution`、`RequireAgeRating`、`RequireLevelAuthors`、`RequireHashes` | 哪些内容必须填写 |
| `MaxResourceBytes`、`MaxDataFileBytes`、`MaxTotalBytes` | 大小限制，0表示不限制 |
| `Sources`、`UnknownSourceTrust` | 网站列表，以及对列表之外网站的评级 |

哪些许可证可以接受，只由配置决定。这看起来像许可证的属性，实际上是接收方服务的属性

## 四个内置配置

| 工厂方法 | `ProfileKey` | 用途 |
|---|---|---|
| `CreateOpen()` | `local` | 你设备上的关卡。没有任何要求 |
| `CreateStandard()` | `standard` | 公共服务器 |
| `CreateWorkshop()` | `workshop` | Steam创意工坊。任何CC BY变体都能通过，缺少文档只会给出警告 |
| `CreateStrict()` | `strict` | 商店版，比`standard`更严格 |

| 项目 | `standard` | `strict` |
|---|---|---|
| 许可证 | CC0 1.0、CC BY 4.0和3.0、CC BY-NC 4.0和3.0、SIL OFL 1.1、MIT、Apache 2.0、the Unlicense | 同`standard` |
| 资源来源 | 关卡文件夹、游戏内或直接链接 | 不允许链接 |
| 署名和哈希 | - | 必需 |
| 每个资源的限制 | 64MiB | 32MiB |
| 每个数据文件的限制 | 32MiB | 16MiB |
| 每个关卡的限制 | 256MiB | 128MiB |

> [!tip] 建议
> 不要为你的服务添加工厂方法。取四个配置之一，修改需要的字段，然后以JSON文件的形式提供

### 为什么是这些许可证和大小

- GPL系列许可证不在`standard`中。通过App Store分发的GPL作品与Apple的条款冲突
- 排除CC BY-SA：ShareAlike会迫使关卡本身更换许可证
- 排除CC BY-ND：NoDerivatives禁止编辑，而游戏正是建立在编辑之上的
- 严格的大小限制就是手机通过移动网络能下载的量

## 资源从哪里来

许可证字段说明作者声称了什么。`SourceTrust`说明结合资源来源网站来看，这个声明有多可信：

| 评级 | 结果 | 示例 |
|---|---|---|
| `Approved` | 发布 | Kenney、ccMixter、Incompetech |
| `PartiallyApproved` | 发布，但值得看一下这条记录 | Pixabay、SoundImage |
| `RequiresLicenseCheck` | 对照真实页面核对许可证 | OpenGameArt、Free Music Archive、Wikimedia Commons |
| `RequiresResourceCheck` | 先确认作品本身 | Rawpixel、itch.io |
| `NotAllowed` | 拒绝 | YouTube、SoundCloud、Spotify |
| `Unknown` | 没有记录，由`UnknownSourceTrust`决定 | - |

`TrustedSourceCatalog.CreateDefault()`返回25个网站。这是一份起始列表。预计每个运营者都会修改它。所以任何东西都不能依赖某条记录一定存在

`Sources`列表为空时关闭来源评级

流媒体平台被明确列为`NotAllowed`，而不是省略。缺失的网站通过`UnknownSourceTrust`评级，在`standard`和`strict`中这个评级要求检查，而不是拒绝

目录和[[ugc-licensing-policy]]描述的是同一件事，需要一起修改

## 如何处理结果

调用的是`ValidationFacade.ValidateForPublish`。更多：[[6_validation]]

`PublishReadinessReport`包含：
- `HasErrors`：`Error`组的问题
- `NeedsManualReview`：`Warning`组的问题
- `IsReady`

接下来怎么做，配置不决定。客户端在有错误时阻止上传。服务器把关卡放入审核队列，而不是直接发布

作者一侧的同一项检查：[[5_publish-readiness]]
