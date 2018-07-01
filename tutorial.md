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
3.  如果你觉得引擎自带的脚本、物体太多，看不顺眼，请将它们移动到一个文件夹内。因删除引擎自带脚本、物体引起的任意问题本人不予解答。

## 前期准备

为了制作一个跳刺游戏，你需要准备如下素材：

- 一首好听的 BGM （ogg 格式），其他格式请用 [在线转码网站](https://convertio.co/zh/audio-converter/) 或你常用的格式转换软件将音乐格式转化为 `.ogg`
- 一个你喜欢的刺素材
- 按照 [自动贴图](autotile.md) 中的说明准备你想使用的贴图

## 全局配置

首先你需要对游戏进行全局配置，按 `Ctrl + F` 调出搜索框（GM 8.1 使用 `Ctrl + R`），输入 setGlobals ，点击确定找到全局配置脚本。

1.  设置游戏标题：`global.game_title = 'I wanna be the Tutorial'`
2.  设置游戏模式：

    - 单机模式，设置 `global.game_mode = MODE_SINGLE_PLAYER`；
    - 竞技模式，设置 `global.game_mode = MODE_TOURNAMENT` 之后，即允许玩家创建最多容纳 8 人的竞技房间。

3.  设置游戏初始房间（假设你的初始房间名为 rStage01）：`global.first_stage = rStage01`
4.  如果不需要多语言支持，可以关闭该功能：`global.enable_internationalization = false`

## 第一个房间

## 播放音乐

为了给游戏注入灵魂，
