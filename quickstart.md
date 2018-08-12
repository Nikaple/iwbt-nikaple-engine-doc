# 快速起步

I wanna，即 I Wanna be the Guy 的衍生游戏，是一类 ~~抖 M~~ 超好玩的 2D 平台跳跃动作游戏。其中，大部分的 I wanna 衍生游戏制作工具均为 `GameMaker`（以下简称 `GM` ）。

使用 I wanna be the Engine Nikaple Edition （以下简称果引擎）创作你自己的 I Wanna 游戏之前，你首先需要下载：

- **GameMaker 8.0 或 8.1**（推荐使用 [GameMaker 8.0 超强中文破解版](http://p9wc9w6dq.bkt.clouddn.com/Super_Gamemaker8_1.4.2_Install.exe)）
- **引擎本体**（[下载地址](http://p9wc9w6dq.bkt.clouddn.com/iwbte-nikaple-edition-2.0.1.zip)）

安装好 `GM`，并使用 `GM` 打开压缩包中提供的 `.gmk` 文件即可开始 I wanna 游戏的创作！

## 开始前的准备

新版果引擎中加入了联机系统，而调试联机功能则至少需要运行两个客户端程序。为此，你需要进行如下设置：

- 打开 `GM 8.x`，**取消勾选** `文件 -> 偏好设置 -> 一般 -> 在游戏运行的时候隐藏编译器并且进入等待模式` （英文版：`File -> Preference -> General -> Hide the designer and wait while the game is running`）；
- 按工具栏上的红色小三角（以调试模式编译游戏）两次，编译两份游戏并以调试模式启动（记为 `P1`、`P2` ）；
- 在 `P1` 按两下 `Shift`，`P2` 按两下 `Ctrl`，再回到 `P1` 按一次 `Shift`，即可开始测试；
- 为了避免被其他玩家登录相同账号挤下线，可以注册两个账号，并参考[调试功能](/debug?id=快速登录)设置你自己的快速登录方式。

## 必知必看

- [Creation Code 简介](cc.md)

  在老版本中，不同 `object` 的 Creation Code 相差甚远，在使用上造成了相当大的不便。因此，新版中重新设计了一套 Creation Code 规范，使得开发者可以不用看文档也知道要写什么参数。

* [新音乐系统](music.md)

  解决了脚本名称过长的问题，并且能够使用统一的脚本播放音乐与音效。

* [新触发系统](trigger.md)

  提高了 `trg` 系统的效率，普通的坑再也不用蛋疼的写 `sprite_index = xxx` 了

* [调试功能](debug.md)

  随着联机系统的更新，调试功能也有进一步的升级。

## 新特性

- [联机功能](network.md)

加入了完整的联机功能，支持注册、登录、创建/加入/离开房间等操作，最高支持 8 人同时游戏（最大人数可在服务端自行设置）。

- [多语言支持](i18n.md)

加入了一个轻量的多语言系统，这使得你的游戏可以更快速地与国际接轨。

# 手感

与大部分引擎 _基本_ 相同。

# 更新日志

从果引擎 v2.0 版开始，对引擎的任意改动均可在 [此处](https://github.com/Nikaple/iwbt-nikaple-engine/commits/master) 查看。

- [2.0.1](https://github.com/Nikaple/iwbt-nikaple-engine/commit/d3fd736a1222a4212bcf18bc456e8c8ce5cef777): 修正在开启 enable_production_mode 之后还会报错的问题。

# 兼容性

果引擎 目前仅支持 GM 8.0 以及 GM 8.1 。由于 GM 8.1 不能使用 FoxWriting 中文绘制，所以使用之前请把多语言模块关闭！具体操作方法如下：

setGlobals 中：

```gml
global.enable_internationalization = false
```

setGlobalsMinor 中：

```gml
global.enable_builtin_drawing = true
```

# 致谢

感谢 [NIHIL](http://tieba.baidu.com/home/main?un=towanoICIT) 大佬在物理引擎方面的指导，没有他的帮助这个引擎应该就:chicken::chicken::chicken:了

# 已知的 BUG

- 物理引擎可能有 BUG ，还请大佬指出

# 联系作者 & BUG 反馈

加入 Q 群即可，验证信息：I Wanna

![QR Code](_images/group.png)

也可通过 [Github Issues](https://github.com/nikaple/iwbt-nikaple-engine-doc/issues) 或者邮箱： nikaple_at_qq.com 向我反馈。
