# Chinese term base

The terms `zh.yaml` (Simplified Chinese) is translated with. Every value in `zh.yaml` follows this table: a thing is
named the same way on every screen, in every hint, in every tooltip.

- **`strict`** rows are checked by the game's tests: whenever the English value of a key contains the `en` term (a
  whole word, any case, tags ignored, a plural `s`/`es` included), its Chinese value must contain the `zh` term.
- **`loose`** rows are guidance: a common word whose best translation depends on the sentence around it. Follow them
  unless the sentence reads wrong, and never use a `loose` row's `zh` for a different concept.
- A row whose `zh` is the same Latin text as `en` means "keep it in Latin" - product names, formats, keys.

The canonical meanings are the [glossary](../en/docs/2_editor/7_reference/1_glossary.md). To propose a change, open an
issue or a pull request that edits this table and every `zh.yaml` value that uses the term, in one change.

Punctuation, labels and the rest of the house style for Chinese: `Assets/Addressables/TEXT-STYLE.md`, section 8, in
the game's repository.

| en | zh | kind | note |
|---|---|---|---|
| Level | 关卡 | strict | 一次游玩的全部内容：物体、音频、事件和它自己的资源 |
| Object | 物体 | strict | 时间轴上的一个作者创建的东西，有生命周期、变换和父级。Unity 中文社区常用"物体" |
| Rect | 空物体 | loose | 不绘制任何内容的物体：只有变换、生命周期和子物体。ru 也拆成两个词：作为物体类型是"空物体"，作为形状（矩形）是"矩形" |
| Shape | 形状 | loose | 物体绘制的真实几何体，不是图片。游戏生成约 500 种 |
| Collider | 碰撞体 | strict | 物体被击中的范围，可以与绘制的内容不一致。Unity 中文版用词 |
| Prefab | 预制件 | strict | 可复用的物体模板，可在关卡中放置任意次。Unity 中文版用词 |
| Prefab Mode | 预制件模式 | strict | 编辑模板本身的内容，而不是周围的关卡 |
| Effect | 特效 | loose | 生成器式的物体：每帧根据几个参数生成自己的物体。后期处理的 Bloom、Vignette 等是"后期效果"，不是"特效" |
| Inframe Object | 帧内物体 | loose | 特效生成的物体，由引擎管理，不能选中或编辑 |
| Theme | 主题 | strict | 关卡按索引引用的调色板，重新配色只需改一处 |
| Frame | 帧 | strict | 关卡时间的单位。帧是一个格子，时间是两个格子之间的边界 |
| Keyframe | 关键帧 | strict | 某一帧上的一个作者设定的值，两个关键帧之间的值会插值 |
| Key | 关键帧 | loose | 作为"关键帧"的简称时译"关键帧"；键盘按键译"按键"，本地化键译"键" |
| Track | 轨道 | strict | 一个可动画属性自己的一行关键帧：位置、旋转、音量。Audio Track 译"音频轨道" |
| Timeline | 时间轴 | strict | 编辑关卡所用的帧轴，每类内容一个标签页 |
| Span | 时段 | loose | 物体存在的时间：起始帧和长度，而非结束帧。英文动词 span（"跨越"）不译为"时段" |
| Playhead | 播放头 | strict | 当前正在显示的帧 |
| Ease | 缓动 | strict | 数值从上一个关键帧移动到这一个的方式 |
| Marker | 标记 | strict | 关卡标尺上的命名点，用于再次找到某个位置 |
| Checkpoint | 检查点 | strict | 死亡后玩家被送回的位置 |
| Anchor | 锚点 | strict | 跟随父级边缘的边，父级缩小时子物体随之移动 |
| Layer | 图层 | strict | 绘制顺序，相对于父级：子物体的图层加上父级的图层 |
| Pivot | 轴心 | loose | 物体旋转和缩放所围绕的点，在它自己的框内。Unity 中文版用词。ru 拆成两个词（"Опора"/"Пивот"），中文统一用"轴心"，相机的 Pivot 同样 |
| Gizmo | 控制柄 | strict | 视口中选中物体上绘制的拖拽手柄 |
| Snapping | 吸附 | strict | 把拖拽拉到某个东西上：磁铁下的其他内容，节拍开关下的音乐 |
| Snap | 吸附 | strict | 同 Snapping |
| Beat | 节拍 | strict | 音乐自己的网格，由关卡设定，播放时不读取 |
| Beat Segment | 节拍段 | strict | 一段恒定速度，有自己的速度、相位和小节长度 |
| BPM | BPM | strict | 每分钟节拍数，保留拉丁字母，中文节奏游戏社区通用 |
| Tap | 敲击 | loose | 敲出速度时的一次按下，足够多次即可描述一个节拍段。触屏上的"点击"译"点按" |
| Generator | 生成器 | strict | 创作自动化：根据几个参数生成关卡内容 |
| Modifier | 修改器 | strict | 编辑或删除已有内容而不是添加的生成器 |
| Seed | 种子 | strict | 关卡中所有随机值的来源数字，同一种子重放相同 |
| Raw Data | 原始数据 | strict | 整个保存模型作为一棵可编辑的树，故意不做校验 |
| Recommendation | 建议 | strict | 五个标签之一，写作 `<b>建议：</b>` |
| Tip | 提示 | strict | 五个标签之一，写作 `<b>提示：</b>` |
| Worth knowing | 须知 | strict | 五个标签之一，写作 `<b>须知：</b>` |
| Warning | 警告 | strict | 五个标签之一，写作 `<b>警告：</b>` |
| Caution | 注意 | strict | 五个标签之一，写作 `<b>注意：</b>` |
| More | 更多 | loose | 窗口提示最后一行 `More:` 写作 `更多：`，链接保留 `/en/` |
| Bullet Hero | Bullet Hero | strict | 产品名，不翻译 |
| Afterbeat | Afterbeat | strict | 产品名，不翻译 |
| Project Arrhythmia | Project Arrhythmia | strict | 产品名，不翻译 |
| Steam | Steam | loose | 产品名，不翻译 |
| JSON | JSON | strict | 格式名，不翻译 |
| MSAA | MSAA | strict | 技术缩写，不翻译 |
| FXAA | FXAA | strict | 技术缩写，不翻译 |
| HDR | HDR | loose | 技术缩写，不翻译 |
| VFX | VFX | loose | 技术缩写，不翻译 |
| URL | URL | loose | 不翻译 |
| Ctrl | Ctrl | loose | 键盘按键名一律保留拉丁字母：Ctrl、Shift、Alt、Enter、Esc、Space、Tab |
| Shift | Shift | loose | 键名；作为动词 shift（"移动"）不保留 |
| Enter | Enter | loose | 键名；作为动词 enter（"进入"、"输入"）按语境翻译 |
| Hierarchy | 层级 | strict | 编辑器面板，按父子关系列出物体。Unity 中文版"层级"窗口 |
| Inspector | 检视器 | strict | 编辑器面板，显示选中内容的属性。Unity 中文版"检视器" |
| Viewport | 视口 | strict | 编辑器中显示关卡画面的区域 |
| Command Palette | 命令面板 | strict | 按名称搜索并执行命令的窗口，VS Code 中文版用词 |
| Command | 命令 | loose | |
| Selection | 选中项 | loose | 名词"选择的内容"；动词 select 译"选择"或"选中" |
| Select | 选择 | loose | 选中物体时也可译"选中" |
| Marquee | 框选 | strict | 拖出矩形进行选择 |
| Apply | 应用 | loose | |
| Reset | 重置 | loose | |
| Cancel | 取消 | loose | |
| Confirm | 确认 | loose | |
| OK | 确定 | loose | |
| Save | 保存 | loose | |
| Load | 加载 | loose | |
| Open | 打开 | loose | |
| Close | 关闭 | loose | |
| Exit | 退出 | loose | 退出预制件模式也用"退出" |
| Create | 创建 | loose | |
| Add | 添加 | loose | |
| Remove | 移除 | loose | 从列表或父级中拿掉，不删除文件 |
| Delete | 删除 | loose | 真正删除，与 Remove 区分 |
| Duplicate | 创建副本 | loose | 与 Copy 区分：Copy 是"复制"到剪贴板，Duplicate 是就地"创建副本" |
| Copy | 复制 | loose | 到剪贴板 |
| Paste | 粘贴 | loose | |
| Cut | 剪切 | loose | |
| Undo | 撤销 | loose | |
| Redo | 重做 | loose | |
| History | 历史 | loose | 撤销/重做的历史记录标签页 |
| Edit | 编辑 | loose | |
| Rename | 重命名 | loose | |
| Move | 移动 | loose | |
| Import | 导入 | loose | |
| Export | 导出 | loose | |
| Archive | 归档包 | loose | 关卡打包成的单个文件 |
| Folder | 文件夹 | loose | |
| File | 文件 | loose | |
| Search | 搜索 | loose | |
| Filter | 筛选 | loose | |
| Refresh | 刷新 | loose | |
| Toggle | 切换 | loose | 开关按钮的动作；"Toggle Left Panel"译"显示/隐藏左侧面板" |
| Show | 显示 | loose | |
| Hide | 隐藏 | loose | |
| Hidden | 已隐藏 | loose | |
| Visible | 可见 | loose | |
| Enabled | 已启用 | loose | |
| Disabled | 已禁用 | loose | |
| On | 开 | loose | 开关状态 |
| Off | 关 | loose | 开关状态 |
| None | 无 | loose | |
| Auto | 自动 | loose | |
| Custom | 自定义 | loose | |
| Default | 默认 | loose | |
| All | 全部 | loose | |
| Nothing | 无 | loose | 空状态文字如"Nothing to…"译"没有可…的内容" |
| Current | 当前 | loose | |
| Active | 活动 | loose | 物体在当前帧是否存在；开关状态时可译"启用" |
| Global | 全局 | loose | 与 Local 相对 |
| Local | 局部 | loose | Local timeline 译"局部时间轴" |
| Parent | 父级 | loose | Unity 中文版用词 |
| Child | 子物体 | loose | 指物体时；泛指时译"子级" |
| Root | 根 | loose | |
| Fold | 折叠 | loose | |
| Unfold | 展开 | loose | |
| Flatten | 展平 | loose | 把预制件放置展开为普通物体 |
| Transform | 变换 | loose | |
| Position | 位置 | loose | |
| Rotation | 旋转 | loose | |
| Scale | 缩放 | loose | |
| Size | 尺寸 | loose | |
| Offset | 偏移 | loose | |
| Angle | 角度 | loose | |
| Radius | 半径 | loose | |
| Width | 宽度 | loose | |
| Height | 高度 | loose | |
| Min | 最小 | loose | 字段标签中可缩写为"最小"/"最大" |
| Max | 最大 | loose | |
| Step | 步长 | loose | 随机值或数值字段的步长 |
| Random | 随机 | loose | |
| Rnd | 随机 | loose | Random 的缩写，中文不需缩写 |
| From | 起点 | loose | 线段两端的 From/To 译"起点"/"终点"，句中按语境译"从" |
| To | 终点 | loose | 同上 |
| Value | 数值 | loose | |
| Type | 类型 | loose | |
| Name | 名称 | loose | |
| Mode | 模式 | loose | |
| Count | 数量 | loose | |
| Speed | 速度 | loose | 物体或玩家的移动速度 |
| Velocity | 速度 | loose | 粒子的矢量速度；与 Speed 同时出现时译"初速度"/"速度矢量"区分 |
| Gravity | 重力 | loose | |
| Particle | 粒子 | loose | |
| Orbital | 环绕 | loose | 粒子的环绕运动 |
| Lifetime | 寿命 | loose | 粒子寿命；物体的存在时间用"时段" |
| Color | 颜色 | loose | |
| Alpha | 不透明度 | loose | ru 拆成两个词（透明度/Альфа）：UI 标签译"不透明度"，通道名可保留"Alpha" |
| Opacity | 不透明度 | loose | |
| Opaque | 不透明 | loose | |
| Transparent | 透明 | loose | |
| Gradient | 渐变 | loose | |
| Texture | 纹理 | loose | Unity 中文版用词 |
| Font | 字体 | loose | |
| Text | 文本 | loose | |
| Localized Text | 本地化文本 | loose | |
| Language | 语言 | loose | |
| Audio | 音频 | loose | |
| Audio Track | 音频轨道 | loose | |
| Volume | 音量 | loose | |
| Music | 音乐 | loose | |
| Sound | 音效 | loose | 界面音效 |
| Resource | 资源 | loose | 关卡自带的纹理、音频、字体等 |
| Resources | 资源 | loose | |
| Metadata | 元数据 | loose | |
| Meta | 元 | loose | Meta Level 译"元关卡" |
| License | 许可证 | loose | |
| Author | 作者 | loose | 关卡作者 |
| Artist | 艺术家 | loose | 音乐作者 |
| Settings | 设置 | loose | |
| Editor | 编辑器 | loose | |
| Game | 游戏 | loose | |
| Player | 玩家 | loose | 游玩的人及其化身 |
| Avatar | 化身 | loose | 玩家控制的形象 |
| Dash | 冲刺 | loose | 化身的冲刺动作 |
| Hitbox | 判定框 | loose | 中文动作/弹幕游戏通用 |
| Damage | 伤害 | loose | |
| Health | 生命值 | loose | |
| Death | 死亡 | loose | |
| Camera | 相机 | loose | Unity 中文版用词 |
| Zoom | 缩放 | loose | 相机或视图的缩放；与 Scale 同时出现时译"变焦" |
| Pan | 平移 | loose | |
| Shake | 震动 | loose | 相机震动 |
| Grid | 网格 | loose | |
| Ruler | 标尺 | loose | |
| Loop | 循环 | loose | |
| Play | 播放 | loose | 编辑器中播放；主菜单的 Play 译"开始游戏" |
| Pause | 暂停 | loose | |
| Stop | 停止 | loose | |
| Preview | 预览 | loose | |
| Render | 渲染 | loose | |
| Post-processing | 后期处理 | loose | Unity 中文版用词 |
| Post | 后期 | loose | Post-processing 的缩写 |
| Bloom | 泛光 | loose | Unity 中文版用词 |
| Vignette | 暗角 | loose | |
| Chromatic Aberration | 色差 | loose | |
| Lens Distortion | 镜头畸变 | loose | |
| Film Grain | 胶片颗粒 | loose | |
| Grain | 颗粒 | loose | |
| Motion Blur | 运动模糊 | loose | |
| Blur | 模糊 | loose | |
| Color Curves | 颜色曲线 | loose | |
| Curve | 曲线 | loose | |
| Lift Gamma Gain | 提升/伽马/增益 | loose | |
| Shadows Midtones Highlights | 阴影/中间调/高光 | loose | |
| White Balance | 白平衡 | loose | |
| Analog Glitch | 模拟故障 | loose | |
| Digital Glitch | 数字故障 | loose | |
| Glitch | 故障 | loose | |
| Gamma | 伽马 | loose | |
| Background | 背景 | loose | |
| Framerate | 帧率 | loose | ru 拆成两个词：显示帧率译"帧率"，Fixed Framerate（模拟更新频率）译"模拟更新频率" |
| Fixed Framerate | 模拟更新频率 | loose | 见 Framerate |
| Collision | 碰撞 | loose | |
| Screen Limit | 屏幕限制 | loose | |
| Cursor | 光标 | loose | |
| Control | 控制 | loose | |
| Controls | 操作 | loose | 设置中的操作方式 |
| Keybinding | 快捷键 | loose | |
| Shortcut | 快捷键 | loose | |
| Button | 按钮 | loose | 手柄按键译"按键" |
| Interface | 界面 | loose | |
| Screen | 屏幕 | loose | |
| Window | 窗口 | loose | |
| Panel | 面板 | loose | |
| Tab | 标签页 | loose | 键名 Tab 保留拉丁字母 |
| Menu | 菜单 | loose | |
| Tool | 工具 | loose | |
| Library | 库 | loose | 关卡库 |
| Bot | 机器人 | loose | 自动游玩关卡的程序 |
| Tutorial | 教程 | loose | |
| Sandbox | 沙盒 | loose | |
| Hint | 提示 | loose | 编辑器中的帮助窗口；注意与标签 `提示：` 区分语境 |
| Glossary | 术语表 | loose | |
| Validation | 校验 | loose | |
| Rules | 规则 | loose | |
| Format | 格式 | loose | |
| Version | 版本 | loose | |
| Desktop | 桌面 | loose | |
| Mobile | 移动端 | loose | |
| Alignment | 对齐 | loose | |
| Align | 对齐 | loose | |
| Center | 居中 | loose | 对齐方式；名词"中心"按语境 |
| Left | 左 | loose | |
| Right | 右 | loose | |
| Top | 上 | loose | |
| Bottom | 下 | loose | |
| Horizontal | 水平 | loose | |
| Vertical | 垂直 | loose | |
| Linear | 线性 | loose | |
| Appearing | 出现 | loose | 物体出现的动画 |
| Scissors | 剪刀 | loose | 在播放头处切分的工具 |
| Edges | 边缘 | loose | |
| Point | 点 | loose | |
| Continue | 继续 | loose | |
| Next | 下一步 | loose | |
| Back | 返回 | loose | |
| Loading | 加载中 | loose | |
| Progress | 进度 | loose | |
| Statistics | 统计 | loose | |
| Preset | 预设 | loose | |
| Clipboard | 剪贴板 | loose | |
| Console | 控制台 | loose | 编辑器的日志面板；平台类型"游戏主机"译"主机" |
| Ping | 定位 | loose | 在层级和视口中显示所选内容，同 Unity 的 Ping |
| Override | 覆盖 | loose | 预制件放置对模板的修改（Modification/Override），Unity 中文版用词 |
| Placement | 放置 | loose | 预制件在关卡中的一次放置 |
| Template | 模板 | loose | 预制件模板 |
| Clip | 片段 | loose | 时间轴上的一段，物体的时段所画出的条 |
| Slip | 滑移 | loose | 视频剪辑用语：移动片段的内容而不移动片段本身 |
| Slot | 槽位 | loose | 主题中的颜色槽位 |
| Beat Grid | 节拍网格 | loose | |
| Bar | 小节 | loose | 音乐的小节 |
| Tempo | 速度 | loose | 音乐速度（BPM 所描述的） |
| Tap Tempo | 敲击测速 | loose | |
| Stereo Pan | 声像 | loose | 音频用语，不译"平移" |
| Font Size | 字号 | loose | |
| Word Wrap | 自动换行 | loose | |
| Backup | 备份 | loose | |
| Branch | 分支 | loose | 历史记录中的分支 |
| Fit | 适配 | loose | Fit Track / Fit Level |
| Finding | 问题 | loose | 规则检查发现的问题 |
| Fix | 修复 | loose | |
| Group | 编组 | loose | 把选中物体编组 |
| Id | ID | loose | 保留拉丁字母 |
| Mipmap | Mipmap | loose | 保留拉丁字母；设置标签可写"Mip贴图" |
| Sampling | 采样 | loose | 纹理采样 |
| Tiling | 平铺 | loose | Unity 中文版用词 |
| Wrapping | 环绕 | loose | 纹理环绕模式 |
| Pixel art | 像素画 | loose | 纹理类型 |
| Drawing | 绘图 | loose | 纹理类型 |
| Emission Shape | 发射形状 | loose | 特效的发射形状，与物体绘制的"形状"区分 |
| Over Lifetime | 随寿命变化 | loose | 粒子属性，Unity 中文版风格 |
| Forces | 力 | loose | 粒子受力 |
| Scatter | 散布 | loose | 与 Spread 区分 |
| Spread | 扩散 | loose | 与 Scatter 区分 |
| Tangent | 切线 | loose | 曲线切线 |
| Clamp | 钳制 | loose | Unity 中文版环绕模式用词 |
| Ping Pong | 往返 | loose | |
| Temperature | 色温 | loose | 白平衡 |
| Tint | 色调 | loose | 白平衡 |
| Modifier Key | 修饰键 | loose | 键盘上按住的 Ctrl/Shift/Alt，与"修改器"（Modifier）不同 |
| Dead Zone | 死区 | loose | 输入设置 |
| Sensitivity | 灵敏度 | loose | |
| Stick | 摇杆 | loose | 手柄或触屏摇杆 |
| Shoulder | 肩键 | loose | 手柄肩键 |
| Gamepad | 手柄 | loose | |
| Touchscreen | 触屏 | loose | |
| Motion Sensor | 体感 | loose | 陀螺仪操作设备 |
| Handedness | 惯用手 | loose | |
| Double Tap | 双击 | loose | 鼠标和触屏都用"双击" |
| Workshop | 创意工坊 | loose | Steam 中文版用词 |
| Story | 剧情 | loose | 主菜单的剧情模式 |
| Wave | 波次 | loose | 沙盒中的攻击波次 |
| Immortal | 无敌 | loose | |
| Dodge | 闪避 | loose | |
| Zen | 禅 | loose | 生命选项中的禅模式 |
| Clears | 通关次数 | loose | 统计 |
| Hits | 受击次数 | loose | 统计 |
| Profile | 档案 | loose | 设备档案（设置中的 Profile 标签页） |
| Frame Hierarchy | 帧层级 | loose | 时间轴标签页：当前帧存在的物体，按父级嵌套 |
| Stop Frame | 停止帧 | loose | |
| Runtime Seed | 运行种子 | loose | |
| Level Logo | 关卡封面 | loose | ru 用"Обложка" |
| Post-processing effect | 后期效果 | loose | Bloom、Vignette 等；"特效"只指 Effect 物体。Comfort 预设中的 screen effects 译"画面效果" |
| Audio effect | 音频效果 | loose | Chorus、Reverb 等，不用"特效" |
| Chorus | 合唱 | loose | 音频效果名 |
| Compressor | 压缩器 | loose | 音频效果名 |
| Distortion | 失真 | loose | 音频效果名 |
| Echo | 回声 | loose | 音频效果名 |
| Flange | 镶边 | loose | 音频效果名，Unity 中文版用词 |
| Highpass | 高通 | loose | 音频效果名 |
| Lowpass | 低通 | loose | 音频效果名 |
| Normalize | 标准化 | loose | 音频效果名 |
| Param EQ | 参数均衡 | loose | 音频效果名 |
| Pitch Shifter | 变调 | loose | 音频效果名 |
| Reverb | 混响 | loose | 音频效果名 |
| Emitter | 发射器 | loose | 粒子发射器 |
| Variant | 变体 | loose | 角度、颜色、缩放的类型选项 |
| Fader | 推子 | loose | 调音台用语 |
| Signal level | 电平 | loose | 音频效果中的 level（Dry Level 等），不是"关卡" |
| Swatch | 色块 | loose | 主题颜色色块 |
| Device library | 本设备的共享库 | loose | 在关卡之间共享特效、预制件、主题的库 |
| Anti-aliasing | 抗锯齿 | loose | |
| Overlay | 叠加层 | loose | |
| Scrub | 拖动试听 | loose | 拖动播放头时的音频试听；特效组中的 scrub 译"拖动" |
| Gradient stop | 色标 | loose | 渐变编辑器中的颜色/Alpha 键 |
| Link to a docs page | 页面标题 | loose | `更多：`链接文字用页面标题的译文，同一页面处处相同；en 用简称时 zh 也用简称 |
