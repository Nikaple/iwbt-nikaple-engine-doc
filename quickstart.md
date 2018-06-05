# 快速起步

I wanna，即 I Wanna be the Guy 的衍生游戏，是一类 ~~抖 M~~ 超好玩的 2D 平台跳跃动作游戏。其中，大部分的 I wanna 衍生游戏制作工具均为 `GameMaker`（以下简称 `GM` ）。

使用 I wanna be the Engine Nikaple Edition （以下简称`果引擎`）创作你自己的 I Wanna 游戏之前，你首先需要下载：

* **GameMaker 8.0 或 8.1**（推荐使用 [GameMaker 8.0 超强中文破解版](http://p57vqeilv.bkt.clouddn.com/Super_Gamemaker8_1.4.2_Install.exe?attname=&e=1527862290&token=FZGZGDr0sWKjK7wJ1v0WnkOOgqYfwshN9tFWlp26:leSWs4WGikF9Ev-nLV1oMGim5LE)）
* **引擎本体**（[下载地址](http://www.baidu.com)）

安装好 `GM`，并使用 `GM` 打开压缩包中提供的 **I wanna be the Engine Nikaple Edition v2.0.0.gmk** 即可开始 I wanna 游戏的创作！

## 开始前的准备

新版 `果引擎` 中加入了联机系统，而调试联机功能则至少需要运行两个客户端程序。为此，我们需要进行如下设置：

* 打开 `GM 8.x`，**取消勾选** `文件 -> 偏好设置 -> 一般 -> 在游戏运行的时候隐藏编译器并且进入等待模式` （英文版：`File -> Preference -> General -> Hide the designer and wait while the game is running`）；
* 按工具栏上的红色小三角（以调试模式编译游戏）两次，编译两份游戏并以调试模式启动（记为 `P1`、`P2` ）；
* 在 `P1` 按两下 `Shift`，`P2` 按两下 `Ctrl`，再回到 `P1` 按一次 `Shift`，即可开始测试；
* 为了避免被其他玩家登录相同账号挤下线，可以注册两个账号，并参考[调试功能](/debug?id=快速登录)设置你自己的快速登录方式。

## 必知必看

* [Creation Code 简介](cc.md)

  在老版本中，不同 `object` 的 `Creation Code` 相差甚远，在使用上造成了相当大的不便。因此，新版中重新设计了一套 `Creation Code` 规范，使得开发者可以不用看文档也知道要写什么参数。

- [新音乐系统](music.md)

  解决了脚本名称过长的问题，并且能够使用统一的脚本播放音乐与音效。

- [新触发系统](trigger.md)

  提高了 `trg` 系统的效率，普通的坑再也不同蛋疼的写 `sprite_index = xxx` 了

- [调试功能](debug.md)

  随着联机系统的更新，调试功能也有进一步的升级。

## 新特性

* [联机功能](network.md)

加入了完整的联机功能，支持注册、登录、创建/加入/离开房间等操作，最高支持 8 人同时游戏。

* [多语言支持](i18n.md)

加入了一个轻量的多语言系统，这使得你的游戏可以更快速地与国际接轨。

# 联系作者 & BUG 反馈

加入 Q 群即可，验证信息：I Wanna

![QR Code](_images/group.png)

也可通过 [Github Issues](https://github.com/nikaple/iwbt-nikaple-engine-doc/issues) 或[电子邮件](mailto:nikaple@nikaple.com)向我反馈。

# 兼容性

`果引擎` 目前仅支持 GM 8.0 以及 GM 8.1。
