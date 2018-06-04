## 全局配置

在`果引擎`中，主要的游戏相关的全局可配置项均放置在 `Scripts -> functions -> setGlobals` 中。

* global.game_title

游戏标题，显示在游戏窗口标题栏。

* global.first_stage

进入正式游戏的第一个房间（不包括标题、选关等房间）。

* global.enable_production_mode

是否开启生产模式。在生产模式中，不会触发引擎中自定义的错误信息（GM 报错没办法）。

* global.enable_internationalization

是否开启[多语言支持](i18n.md)。

* global.language

默认语言，可选项为 `LANG_CN`, `LANG_EN`, `LANG_JP`。

* global.enable_builtin_drawing

是否使用内置绘图函数。如果关闭，则会统一使用 `FoxWriting` 进行绘制。

* global.enable_lite_mode

轻量化模式（测试专用），当游戏处于开发过程中时，将它设置为 `true` 则会在运行游戏之后直接读取一号存档，直接跳过标题、菜单等界面。

* global.enable_stream_music

是否开启流式播放。开启之后音乐将被一小段一小段地加载至内存中，极大提升运行效率，但缺陷是不能暂停。因此，在玩家死亡或游戏暂停时，背景音乐将不会暂停播放，而仅仅减少音量。

* global.enable_auto_spike_sprite

是否[自动更换刺的精灵](autosprite.md)

* global.enable_jump_cancel

是否允许`JC`。

* global.enable_fullscreen

是否允许按 F4 全屏。

* global.enable_keypad

是否允许小键盘
