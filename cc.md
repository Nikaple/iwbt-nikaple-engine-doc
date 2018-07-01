# Creation Code 简介

## 如何使用 Creation Code

在引擎中，大量存在着通用 `object`，它们通过放置在房间之后的 Creation Code 来实现差异化功能。具体使用方法为：

1.  打开房间编辑器，将 `object` 摆放到房间中

2.  根据 GameMaker 版本的不同，添加 Creation Code 的方式也不同

    - GameMaker 8.0：`Ctrl + 右键 -> Creation Code...`
    - GameMaker 8.1：`右键 -> Creation Code...`

## 果引擎中的 Creation Code 规范

Creation Code中，存在着许多通用代码，记住它们将能帮助你更快更好地使用引擎，归类如下：

```gml
--------------- 通用 ---------------
     spr = 需要更换的精灵（sprite_index）
     ind = 精灵编号（image_index）
    ispd = 精灵播放速度（image_speed）
      xs = 水平缩放（image_xscale）
      ys = 竖直缩放（image_yscale）
     trg = 触发器编号
       h = 触发横向速度
       v = 触发纵向速度
     spd = 触发速度
     dir = 触发方向
  origin = 旋转/缩放中心
    time = 时间（以帧为单位）
     num = 编号（boss编号，道具编号等）
   noDes = 出房间后是否不销毁（默认为出房间后直接销毁）
  noSync = 是否不同步（默认同步）
     dis = 出房间后销毁前移动的距离（默认为 0）

------------- 路径相关 -------------
     pth = 路径编号
     spd = 速度
    enda = 路径结束事件（参考常量表）
     scl = 路径放大倍数
    move = 是否防止剧透（玩家死亡之后会沿着当前方向移动，不会停止/转弯）

------------- 传送相关 -------------
  roomTo = 目标房间
    kind = 转场效果（可选）
     num = 目标 playerStart 的编号（可选）
    mode = warp 模式（'normal'/'border'，默认为'normal'）
    text = warp 上方文字（可选）
   color = warp 上方文字颜色（可选）
```
