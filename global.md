# 全局配置

## 常用全局设定

在果引擎中，主要的游戏相关的全局可配置项均放置在 `Scripts -> functions -> setGlobals` 中。

### 游戏相关设定

#### global.game_title

游戏标题，显示在游戏窗口标题栏。

#### global.first_stage

游戏正式开始时的初始房间（不包括标题、选关等房间）。

#### global.enable_production_mode

是否开启生产模式，默认为 `false`。在生产模式中，不会触发引擎中自定义的错误信息（GM 报错没办法）。

#### global.enable_internationalization

是否开启[多语言支持](i18n.md)，默认为 `true`。

#### global.language

默认语言设定，默认为 `LANG_CN`。可选项为 `LANG_CN`, `LANG_EN`, `LANG_JP`。

#### global.encoding

文字编码，默认为 `gb2312`。该项应与你使用的操作系统文字编码一致，详见[编码表](https://msdn.microsoft.com/en-us/library/windows/desktop/dd317756.aspx)。

#### global.enable_builtin_drawing

是否使用内置绘图函数，默认为 `false`。如果开启，则在语言为 `LANG_EN` 时会使用内置回吐函数；如果关闭，则会统一使用 `FoxWriting` 进行绘制。

#### global.game_room_width

游戏窗口宽度

#### global.game_room_height

游戏窗口高度

#### global.enable_stream_music

是否开启流式播放，默认为 `true`。开启之后音乐将被分段加载至内存中，极大提升运行效率，但缺陷是不能暂停。

?> 流式播放模式下，在玩家死亡或游戏暂停时，背景音乐将不会暂停播放，而仅仅减少音量。

#### global.enable_focus

是否使用键盘模拟聚焦模式。原理是在游戏中不断触发某个不存在的按键，这个按键只能在窗口聚焦时有效。默认开启。

#### global.focus_key_code

使用键盘模拟聚焦的键码。默认为 `1`，即 ``。

#### global.enable_encryption

存档文件是否加密，默认为 `true`。

#### global.key

存档文件加密密钥，为了保证安全，密钥长度应该不小于 64。

### 网络相关设定

#### global.ip_address

服务器 IP 地址。引擎中提供的地址仅供测试，不保证随时可用。推荐发布游戏时部署自己的服务器以增强稳定性。

#### global.tcp_port

服务器 TCP 端口，默认 3738。

#### global.udp_port

服务器 UDP 端口，默认 3738。

#### global.online_mode

联机模式，默认开启。

#### global.max_sync_cycle

同步周期。该值决定了客户端之间同步数据的频率，默认为每 3 帧发送一个同步数据包。

### 调试相关设定

#### global.enable_lite_mode

轻量化模式（快速测试专用）。开启之后，则会在运行游戏编译完成之后直接读取一号存档，跳过标题、菜单等界面。

#### global.debug_host_name

调试用主机用户名（快速登录用）

#### global.debug_host_pass

调试用主机密码（快速登录用）

#### global.debug_guest_name

调试用非主机用户名（快速登录用）

#### global.debug_guest_pass

调试用非主机密码（快速登录用）

## 次要全局设定

一些基本不会改的配置项，位于 `system -> setGlobalsMinor` 中。

#### global.enable_pause_in_boss_room

BOSS 房间内是否允许暂停，默认为 `false`。

#### global.enable_jump_cancel

是否允许跳跃取消（JC），默认为 `false`。

#### global.enable_fullscreen

是否允许按 F4 全屏，默认为 `true`。

#### global.enable_keypad

是否允许使用小键盘，默认为 `true`。

#### global.enable_auto_spike_sprite

是否[自动更换刺的精灵](autosprite.md)，默认为 `true`。

#### global.boss_number

BOSS 数量上限，默认为 `64`。

#### global.item_number

道具数量上限，默认为 `64`。

#### global.data_number

自定义数据数量上限，默认为 `64`。

#### global.saving_directory

存档保存路径，默认为 `Data/Save`。

#### global.music_directory

音乐读取路径，默认为 `Data/Music`。

#### global.plugin_directory

插件读取路径，默认为 `Data/Plugin`。

#### global.option_file_name

配置文件名，默认为 `options.ini`。
