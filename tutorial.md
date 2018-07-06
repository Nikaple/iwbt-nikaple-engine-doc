# 你的第一个跳刺游戏

## 写在前面

在你做游戏之前，有这么几点一定注意：

1.  确保资源（精灵，脚本，物体等）的命名有相应的前缀，如果资源名称与脚本的变量冲突，GameMaker 会抛出一个 `Variable name expected.` 错误。推荐命名如下：

    1.  精灵命名为 **spr**xxx；
    2.  音效命名为 **snd**xxx；
    3.  背景命名为 **bg**xxx；
    4.  路径命名为 **p**xxx；
    5.  脚本命名为 **scr**xxx；
    6.  字体命名为 **font**xxx；
    7.  时间轴命名为 **tl**xxx；
    8.  物体命名为 **obj**xxx；
    9.  房间命名为 **r**xxx。

2.  rInit 一定要处于所有房间的顶端，不能移动。
3.  如果你觉得引擎自带的脚本、物体太多，看不顺眼，请将它们移动到一个文件夹内。

!> **因删除引擎自带脚本（script）、物体（object）引起的任意问题本人不予解答** 。

## 前期准备

为了制作一个跳刺游戏，你需要准备如下素材：

- 一首好听的 BGM （ogg 格式），其他格式请用 [在线转码网站](https://convertio.co/zh/audio-converter/) 或你常用的格式转换软件将音乐格式转化为 `.ogg`
- 一个你喜欢的刺素材（32 \* 32）
- 按照 [自动贴图](autotile.md) 中的说明准备你想使用的贴图

## 全局配置

首先你需要对游戏进行全局配置，按 `Ctrl + F` 调出搜索框（GM 8.1 使用 `Ctrl + R`），输入 setGlobals ，点击确定找到全局配置脚本。

1.  设置游戏标题：`global.game_title = 'I wanna be the Tutorial'`
2.  设置游戏模式：

    - 单机模式，设置 `global.game_mode = MODE_SINGLE_PLAYER`；
    - 竞技模式，设置 `global.game_mode = MODE_TOURNAMENT` 之后，即允许玩家创建最多容纳 8 人的竞技房间。

3.  设置游戏初始房间（假设你的初始房间名为 rMyStage01）：`global.first_stage = rMyStage01`
4.  如果不需要多语言支持，可以关闭该功能：`global.enable_internationalization = false`

## 第一个房间

由于自带 rTemplate 这个房间，所以可以直接复制 rTemplate 这个房间，接下来就设置背景

1.  首先到上面那个选项栏里面去选择`创建背景图片`
2.  点击`载入背景图片`按钮
3.  选择一张你喜欢的图片当做背景
4.  点击`编辑背景图片`按钮
5.  找到`变换`，点击`拉伸图像`
6.  `宽`和`高`改成 800 和 608，并且选择`完美`选项

插一下话，如果你能够确保你的图片能够平铺下来无缝衔接的话可以选择无视 4-6 步骤

7.  找到你想要设置背景的房间，打开它
8.  点击`背景图片`
9.  点击`房间打开时可见`然后选择背景

OK，你的背景就搞好了，接下来你就可以开始摆东西了，灵活运用贴图与对象，下面我会讲讲贴图和对象是什么以及怎么使用的

## 设置刺的精灵

设置刺精灵的步骤如下：

1.  将准备好的刺素材作为精灵导入 GameMaker ，并将其中心点设置为 (16, 16)，取名为 sprMySpikeM。
2.  将 `Objects -> rooms -> objSpikeSprite` 放入房间，并设置其 Creation Code：
    ```gml
    spr = sprMySpikeM
    ```

## 设置自动贴图

设置自动贴图的步骤如下：

1.  将准备好的贴图素材作为背景导入 GameMaker ，取名为 bgMyTile
2.  将 `Objects -> rooms -> objBlockTile` 放入房间，并设置其 Creation Code：
    ```gml
    tile = bgMyTile
    ```

## 播放音乐

为游戏设置 BGM 的步骤如下：

1.  将准备好的 BGM 命名为 myMusic.ogg 放入音乐文件夹（Data/Music）下。
2.  将 `Objects -> rooms -> objPlayMusic` 放入房间，并设置其 Creation Code：
    ```gml
    bgm = BGM_myMusic
    ```

## 设置存档点

在想设置存档的地方放置 `Objects -> saves -> savePoint` 。在全局配置 `setGlobals` 中，我们可以通过变量 `global.save_mode` 定义存档的默认工作模式。可选值如下：

- `global.save_mode = SAVE_MODE_SHOOT` 射击存档（默认）
- `global.save_mode = SAVE_MODE_TOUCH` 触碰存档
- `global.save_mode = SAVE_MODE_PRESS` 按键存档，默认为 'S'。默认按键可到 `controls_init` 脚本中修改 `global.savebutton`。

## 房间传送

### 使用普通 warp

如果想让 player 从 rMyStage01 传送到 rMyStage02 的 playerStart 位置，你可以在 rMyStage01 中放置传送门（warp），并在 Creation Code 中写入：

```gml
r = rMyStage02
```

### 使用 borderWarp

如果想让 player 从 rMyStage01 的最右侧传送到 rMyStage02 的最左侧，你可以在 rMyStage01 的最右侧放置 borderWarp，并在 Creation Code 中写入：

```gml
r = rMyStage02
ys = 纵向拉伸倍数
```

?> 如果 borderWarp 被放置于房间边缘，它会自动移动到房间外而不需要在 Creation Code 中改变其坐标。

## 游戏结束

当游戏结束时，你可以将 objGameClear 放在通关房间的必经入口上，当 player 碰到 objGameClear 时，游戏会停止计时，并在选关界面显示 Clear!! 字样。

## 游戏测试

在测试之前，你可以在 `setGlobals` 中将 `global.enable_lite_mode` 设置为 `true`，启用之后会在游戏运行时直接读取 **第一个** 存档，大幅提高你的测试效率。

## 发布游戏

在游戏发布之前，你需要进行以下操作：

1.  在 `setGlobals` 中：
    - 将 `global.enable_production_mode` 设置为 `true`，这会关闭引擎中的错误提示（GM 错误提示无法关闭）；
    - 将 `global.key` 更换为长度不小于 40 的随机字符串，以增强存档安全性。
2.  在游戏全局设置（Global Game Settings）中更换游戏图标（可选）；
3.  执行文件 → 创建可执行 exe（File -> Create Executable...）将游戏打包为 exe；
4.  利用防反编译/代码混淆软件保护你的 exe 文件，参考[游戏发布](release.md)
5.  将得到的 exe 文件与 Data 文件夹打包到同一个压缩文件中，发布即可。

## 如果你需要...

### 大房间

假设你需要制作一个 2 \* 2 的大房间，也就是宽 1600 像素，高 1216 像素，步骤如下：

1.  进入房间，在设置选项卡中将宽度设置为 1600 像素，高度设置为 1216 像素；
2.  如果房间中没有 `Objects -> rooms -> objCamera` ，放一个在房间的任意位置；
3.  在大房间中制作你的地图即可。

### 视野跟随

在需要视野跟随时，仅需要将 `Objects -> rooms -> objSmoothView` 放入房间即可。在默认情况下，该 obj 会启用视野平滑效果，如需关闭，可以设置其 Creation Code 参数：

```gml
noSmooth = true
```
