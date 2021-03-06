# 快速起步

I wanna，即 I Wanna be the Guy 的衍生游戏，是一类 ~~抖 M~~ 超好玩的 2D 平台跳跃动作游戏。其中，大部分的 I wanna 衍生游戏制作工具均为 `GameMaker`（以下简称 `GM` ）。

使用 I wanna be the Engine Nikaple Edition （以下简称果引擎）创作你自己的 I Wanna 游戏之前，你首先需要下载：

- **GameMaker 8.0 或 8.1**（推荐使用 [GameMaker 8.0 超强中文破解版](https://iwbte-nikaple-edition-1255674901.cos.ap-guangzhou.myqcloud.com/engine/Super_Gamemaker8_1.4.2_Install.exe)）
- **引擎本体**（[下载地址](https://iwbte-nikaple-edition-1255674901.cos.ap-guangzhou.myqcloud.com/engine/iwbte-nikaple-edition-2.1.2.zip)）

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

!> 注：在查看过程中，你可能会发现 `&gt;`/`&lt;` 这样的符号，可以用 [HTML 解码网站](http://www.convertstring.com/EncodeDecode/HtmlDecode) 进行处理。

- [2.0.1](https://github.com/Nikaple/iwbt-nikaple-engine/commit/d3fd736a1222a4212bcf18bc456e8c8ce5cef777):
  - 修复在开启 enable_production_mode 之后还会报错的问题。
- [2.0.2](https://github.com/Nikaple/iwbt-nikaple-engine/commit/97d0e617771a5a1f5a9a80bb0100b61d33b7f43d):
  - 修复一次性吃太多+1 跳会报错的问题；
  - 修复 objDebug 不能正确显示 objMultiplePath 的问题。
- [2.0.3](https://github.com/Nikaple/iwbt-nikaple-engine/commit/113906151ea30a3af402aa4cd17a881a814d9d42):
  - 在游戏传输的数据中加入时间戳，扔掉无效的数据以增强游戏的连续性。
- [2.1.0](https://github.com/Nikaple/iwbt-nikaple-engine/commit/2cfd34e401fc1668f86aa316c47376c4eb429265)
  - 这是一次跳崖式升级...由于在之前的更新中，由于提交脚本问题一直没有移除引擎中无用的代码，进而没有移除一些物体/事件，导致本次的提交历史完全是一团乱麻。好在修复之后，版本之间的更新历史会更加清晰，方便查阅。
  - 加入了全新的聊天室功能。由于在打开聊天室时，需要禁用键盘操作（比如移动、按R），本次将引擎中所有用到了 keyboard_check_xxx 以及键盘事件的地方，都改成了 key_check_pressed / key_check_released，以保证在聊天时的正常功能。在需要自定义键盘事件时，请一定注意。
  - 加入了一些防御性代码，修复在网络不佳时可能产生自己残影的 BUG、聊天信息重复发送的 BUG 等。
  - 在禁用 JC 时，直接让右 Shift 无法使用。
  - 默认禁用小键盘。
- [2.1.1](https://github.com/Nikaple/iwbt-nikaple-engine/commit/ff9c28b73944a28ecfa58117de5fe6d276235557)
  - 增加运行前对 `Data\Plugin` 文件夹的检测，使 dll 加载报错更易懂。
  - 将微软雅黑更换为 4.78 M 的版本，大幅减小引擎体积。
  - 修正几个 typo。
- [2.1.2](https://github.com/Nikaple/iwbt-nikaple-engine/commit/33194c8548ed553c252729258ccb7ce513a097e5)
  - 增加运行前对音乐文件夹中音乐命名规范的检测，并在调试模式下为开发者提供友好的错误信息。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/9e9e47cc001cef4a3cbc666a416fe600df34d1d5)
  - 增加运行前对资源名称进行统一检查，避免资源重名、资源名称不合法的问题。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/97c0944b7fe6f86023feece17dad225667f61ce1)
  - 加入对 blockHost/blockGuest 进行自动贴图的支持。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/6764ee1ab37ec11bc23895bc912505ebe523a608)
  - 对自动贴图的具体实现机制进行修改，超大房间也可以较完美地进行贴图了（基本秒开，可以参考引擎中的 rHugeRoom）。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/6764ee1ab37ec11bc23895bc912505ebe523a608)
  - 修复开始游戏后存档不能正确创建的问题。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/249eebc63bbb5f5d60258059cd80415f951dee74)
  - 修复 debug 模式下不能开关显示红蓝砖的问题。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/24ed370bceac18f800016595c4a6a8ddd29da3b7)
  - 现在不推荐使用脚本进行自动贴图，应该统一使用 objBlockTile 放置在房间中处理。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/0e51a5a9bae179c56691f8d25021e9296329dfd4)
  - 将 obj 检查参数的行为从 Create 移入 Alarm 11 事件，以兼容从代码创建 (`instance_create`) 的行为。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/9d8387b8469c101a1c368a5493e5ae9008cbd03a)
  - 修复聊天室标题栏错位的问题。[修改日志](https://github.com/Nikaple/iwbt-nikaple-engine/commit/9e0b4d422ae3be03fd09f72ea7b1dc3776d6e1b9)

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

感谢 [NIHIL](http://tieba.baidu.com/home/main?un=towanoICIT) 大佬在物理引擎方面的指导，没有他的帮助这个引擎应该就 :chicken::chicken::chicken:了

# 已知的 BUG

- 物理引擎可能有 BUG ，还请大佬指出（如果能提出修复方法就更好了:sweat_smile:）

# 联系作者 & BUG 反馈

加入 Q 群即可，验证信息：nikaple

![QR Code](_images/group.png)

也可通过 [Github Issues](https://github.com/nikaple/iwbt-nikaple-engine-doc/issues) 或者邮箱： nikaple_at_qq.com 向我反馈。
