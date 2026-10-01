---
title: 合法资源的两种途径
date: 2026-09-25
tags: [level_author]
---

# 合法资源的两种途径

资源要么有合适的许可证，要么有权利人的许可，才算合格。没有第三种方式

外部资源是关卡自带的一切：音乐、图片、字体、文本和任何文件。每个资源都必须满足**两种方式之一**

## 方式A：开放许可证

资源本身的分发条款已经不比`CC BY-NC`更严格。它保留自己的条款，不会变成`CC BY-NC`

标准配置接受：
- [CC0](https://creativecommons.org/publicdomain/zero/1.0/)：公有领域
- [CC BY](https://creativecommons.org/licenses/by/4.0/)，4.0和3.0版
- [CC BY-NC](https://creativecommons.org/licenses/by-nc/4.0/)，4.0和3.0版
- [MIT](https://choosealicense.com/licenses/mit/)和[Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)：用于文本和代码
- [SIL OFL 1.1](https://openfontlicense.org/open-font-license-official-text/)：用于字体，必须在元数据中注明
- [Unlicense](https://choosealicense.com/licenses/unlicense/)

> [!tip] 建议
> 如果由你来选，就选`CC0`。它是唯一对关卡没有任何要求的许可证

## 配置拒绝什么

- **专有许可**，即“保留所有权利”
- [CC BY-SA](https://creativecommons.org/licenses/by-sa/4.0/)：关卡就得以CC BY-NC-SA发布，而关卡不是以它分发的
- [CC BY-ND](https://creativecommons.org/licenses/by-nd/4.0/)：它禁止修改，这一点游戏不支持
- [CC BY-NC-SA](https://creativecommons.org/licenses/by-nc-sa/4.0/)和[CC BY-NC-ND](https://creativecommons.org/licenses/by-nc-nd/4.0/)：同样是这两个原因

GPL系列不在列表中，尽管它比CC BY-NC更自由。GPL代码无法通过App Store分发而不与Apple的条款冲突。所以凡是会进入iOS版本的内容，都必须保持MIT或Apache的形式

## 配置取决于服务

接受哪些许可证由服务决定，而不是由许可证决定。上面的列表是标准配置。商店版本接受的更少，社区服务器可能接受别的

## 方式B：权利人的许可

私下一句“行，拿去用吧”是不够的。`CC BY-NC`的关卡会被公开分发，许可必须恰好覆盖这一点，而不是你的个人使用

有效的许可同时给出以下三点：
1. 在Bullet Hero关卡中使用该资源的权利
2. 允许第三方通过游戏的服务，自由、非商业地分发这个包含该资源的关卡，并署名
3. 明确限定为仅限非商业用途

如何请求许可：[[6_asking-permission]]

> [!caution] 注意
> 许可不会把拒绝变成通过。如果资源的许可证属于被拒绝的那些，许可会把它送去人工审核，但不会让它变成“允许”

## 许可的范围和期限

没有写明范围或没有证据的许可视为不完整。过期的许可完全不算数

**范围会被记录下来**，而且很重要：
- 针对某一个具体关卡的许可，一旦资源被复制到另一个关卡就失效
- 针对任意关卡的许可，在任何复用中都有效

接下来：[[6_asking-permission]]、[[4_resource-record]]
