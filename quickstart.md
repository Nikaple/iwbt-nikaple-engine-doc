# 快速起步

I wanna，即 I Wanna be the Guy 的衍生游戏，是一类 ~~抖 M~~ 超好玩的 2D 平台跳跃动作游戏。其中，大部分的 I wanna 衍生游戏制作工具均为 GameMaker（以下简称 GM ）。

使用 I wanna be the Engine Nikaple Edition （以下简称`果引擎`）创作你自己的 I Wanna 游戏之前，你首先需要下载：

* **GameMaker 8.0 或 8.1**（推荐使用 [GameMaker 8.0 超强中文破解版](http://p57vqeilv.bkt.clouddn.com/Super_Gamemaker8_1.4.2_Install.exe?attname=&e=1527862290&token=FZGZGDr0sWKjK7wJ1v0WnkOOgqYfwshN9tFWlp26:leSWs4WGikF9Ev-nLV1oMGim5LE)）
* **引擎本体**（[下载地址](http://www.baidu.com)）

安装好 GM，并使用 GM 打开压缩包中提供的 `I wanna be the Engine Nikaple Edition v2.0.0.gmk` 即可开始 I wanna 游戏的创作！

## 全局配置

在`果引擎`中，主要的游戏相关的全局可配置项均放置在 `Scripts -> functions -> setGlobals` 中。

### global.game_title

游戏标题，显示在游戏窗口标题栏。

### global.first_stage

进入正式游戏的第一个房间（不包括标题、选关等房间）。

### global.enable_production_mode

是否开启生产模式。在生产模式中，不会触发引擎中自定义的错误信息（GM 报错没办法）。

### global.enable_internationalization

是否开启[多语言支持](i18n.md)。

### global.language

默认语言，可选项为 `LANG_CN`, `LANG_EN`, `LANG_JP`。

### global.enable_builtin_drawing

是否使用内置绘图函数。如果关闭，则会统一使用 `FoxWriting` 进行绘制。

### global.enable_lite_mode

轻量化模式（测试专用），当游戏处于开发过程中时，将它设置为 `true` 则会在运行游戏之后直接读取一号存档，直接跳过标题、菜单等界面。

### global.enable_stream_music

是否开启流式播放。开启之后音乐将被一小段一小段地加载至内存中，极大提升运行效率，但缺陷是不能暂停。因此，在玩家死亡或游戏暂停时，背景音乐将不会暂停播放，而仅仅减少音量。

### global.enable_auto_spike_sprite

是否[自动更换刺的精灵](autosprite.md)

### global.enable_jump_cancel

是否允许`JC`。

### global.enable_fullscreen

是否允许按 F4 全屏。

### global.enable_keypad

是否允许小键盘

# 兼容性

果引擎目前仅支持 GM 8.0 以及 GM 8.1。
