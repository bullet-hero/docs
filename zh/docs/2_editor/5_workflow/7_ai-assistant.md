---
title: AI助手
date: 2026-10-12
tags: [level_author]
---

# AI助手

支持MCP的AI客户端可以在你眼前编辑编辑器中打开的关卡。每个AI批量操作都是一个撤销步骤，AI不能发布、删除文件，也不能覆盖其他关卡

为此，Windows、Linux和Mac上的游戏自带一个MCP服务器。AI用和你相同的操作进行编辑，所以每处改动都会立刻出现在视口中，并像你自己的操作一样进入历史记录

任何支持MCP的客户端都可以，比如聊天应用或编程助手。游戏中没有任何东西绑定在某一个AI上

## 连接客户端

1. 打开`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`
2. 勾选`{{ui:settings_game-editor_mcp-enabled}}`。设置下方的状态行会显示编辑器监听的端口
3. 按下`{{ui:settings_game-editor_mcp-copy-config}}`。剪贴板中就有了已填好两个路径的客户端配置
4. 把它粘贴到你的客户端的MCP服务器设置中
5. 在编辑器中打开一个关卡，或者让AI自己打开编辑器或关卡

复制的配置是这样的：

```json
{ "mcpServers": { "bullet-hero": { "command": "<path to Bullet Hero MCP>", "args": ["--endpoint", "<path to endpoint.json>"] } } }
```

服务器文件`Bullet Hero MCP`位于游戏旁边：

| 系统 | 服务器文件 |
|---|---|
| Windows | `<游戏文件夹>/Bullet Hero MCP.exe` |
| Linux | `<游戏文件夹>/Bullet Hero MCP` |
| Mac | `<game>.app/Contents/Resources/mcp/osx-arm64/Bullet Hero MCP`，Intel上用`osx-x64`代替`osx-arm64` |

只有本机可以连接，并且同一时间只能连接一个客户端。手机和平板上没有MCP部分：助手只在电脑上可用

## AI能做什么，不能做什么

你能做的事，AI几乎都能做：
- 读取关卡：层级、物体、关键帧、事件和资源
- 创建、修改和删除物体、关键帧、标记、检查点、音频轨道和节拍网格
- 运行生成器，打包和放置预制件，在预制件模式中工作
- 把纹理、字体或音频文件导入关卡
- 撤销和重做，保存打开的关卡，打开其他关卡，创建新关卡
- 用与启动时相同的参数把游戏切换到其他界面，例如编辑器、某个关卡或设置 - [[12_launch-arguments]]
- 在游戏未运行时启动游戏，前提是服务器位于已安装的游戏旁边且MCP已经开启

这样开始的游玩和其他游玩一样计入你的统计，所以AI只在你要求时才会开始游玩

它不能：
- 发布到Steam创意工坊
- 删除关卡或任何文件
- 覆盖其他关卡或其他文件。文件名已被占用的导入会被拒绝
- 打开只读关卡，或者本次会话中你还没输入过密码的受保护关卡
- 在打开的关卡有未保存的修改时打开其他关卡

**一个AI批量操作就是历史记录中的一步**。它在`{{ui:settings_level-settings_history}}`标签页中显示为`{{ui:op_group_ai-batch}}`，并带有AI自己写的说明。按一次`Ctrl+Z`就会撤销整个批量操作。关于历史记录的更多内容：[[10_level-settings#历史]]

第一个修改关卡的AI批量操作会把关卡的`{{ui:settings_level-settings_metadata-level-ai-generated}}`设为`{{ui:enum_ai-generation_yes}}`，而且是在同一步中。撤销这个批量操作也会把它还原。更多：[[2_metadata-and-sharing#AI生成]]

## 你优先

AI从不和你争夺编辑器：
- 你拖动控制柄手柄或拖动时间轴时，AI的编辑会被拒绝，它会等待并重试
- AI只在你空闲时才使用播放头：没有在游玩、拖动、输入或保存
- AI查看某一帧时你动了编辑器，AI会立刻停下。播放头留在你放的位置
- 历史记录跳转进行期间，AI也无法编辑

客户端连接期间，视口工具栏上会显示一个标记：`{{ui:editor_agent-badge_connected}}`，AI工作时则显示它正在做的事的说明。标记上的`{{ui:editor_agent-badge_stop}}`会断开客户端，并在你按下`{{ui:editor_agent-badge_allow}}`之前拒绝它连接。在那之前，标记上显示`{{ui:editor_agent-badge_stopped}}`

停止状态不会保存。关闭`{{ui:settings_game-editor_mcp-enabled}}`或重启游戏都会解除它

## AI看到什么

AI用两种方式观察关卡：
- **示意图**。任意一帧的图片，在屏幕外计算出来。它不移动播放头。上面有形状和判定框，但没有文本和特效
- **截图**。真实的像素，和关卡绘制的完全一样，通过你的播放头拍下。播放头会短暂跳到那一帧，编辑器的叠加层会隐藏。然后播放头回到你离开时的位置，除非开启了`{{ui:settings_game-editor_mcp-follow-ai}}`。画面由关卡摄像机取景，而不是编辑器摄像机

跳转之后的特效截图接近连续播放时的样子，但不一定完全相同

AI听不到音乐。它把音轨变成数字：速度、节拍、小节、段落、每个频段的响度。这只是带置信度的估计，可能出错，比如速度差一半或一倍。你在关卡中设置的节拍网格比AI的估计更可信

所以在时机很重要时，AI可能会请你听一下。它在编辑器中播放最长{{v:mcp.max-play-seconds}}秒的一段，这也会移动播放头。你一动编辑器，播放就停在当前位置

## ai文件夹

AI把关于关卡的记忆保存在关卡文件夹内的`ai`文件夹中。下一次会话，无论用哪个客户端，都会先读它，从上一次停下的地方继续

里面有：
- `CONTEXT.md`：任务、音乐、段落计划、决定、你的意见和未解决的问题
- AI决定保留的其他文件，只能是`.md`或`.json`
- `manifest.json`：文件夹是否随关卡一起传送。AI无法修改它

只有当AI第一次有东西要写时，这个文件夹才会出现。一个文件最多{{v:mcp.ai-file-max-kb}}KB，整个文件夹最多{{v:mcp.ai-folder-max-mb}}MB。这些都是普通的文本文件：你可以自己阅读、编辑或删除

> [!warning] 警告
> `ai`文件夹不属于关卡的历史记录。`Ctrl+Z`不会撤销AI写进去的内容

**默认情况下，文件夹会随关卡一起传送**：进入导出的归档包和Steam创意工坊上传内容。想把它留在本地，就在关卡设置的`{{ui:settings_level-settings_metadata}}`标签页中取消勾选`{{ui:settings_level-settings_metadata-level-ai-share}}`。文件夹存在后这个复选框才会出现。它会立即保存到文件，所以`Ctrl+Z`也不会还原它

带密码的导出模式从不包含这个文件夹，无论复选框怎么设置。更多：[[13_export-and-protection#导出关卡]]

在本设备上复制关卡时，文件夹会一起复制，因为复制不是分享

## 设置

所有设置都在`{{ui:settings_common_title}}` → `{{ui:hint_settings_game-editor_header}}` → `{{ui:settings_game-editor_mcp_title}}`中，只保存在本设备上：
- `{{ui:settings_game-editor_mcp-enabled}}`：客户端到底能不能连接。默认关闭
- `{{ui:settings_game-editor_mcp-port}}`：编辑器监听的端口。`0`表示每次启动自动选一个空闲端口
- `{{ui:settings_game-editor_mcp-follow-ai}}`：开启时，截图之后播放头停在AI查看的那一帧并暂停
- `{{ui:settings_game-editor_mcp-reveal-edits}}`：每次AI编辑后，选中并定位它创建或修改的内容

所有设置及其默认值：[[14_editor-settings#AI代理]]

接下来：[[4_not-losing-work]]、[[13_export-and-protection]]
