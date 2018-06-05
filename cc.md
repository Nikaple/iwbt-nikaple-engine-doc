# Creation Code 简介

## 如何使用 Creation Code

在引擎中，大量存在着通用 `object`，它们通过放置在房间之后的 `Creation Code` 来实现差异化功能。具体使用方法为：

1.  打开房间编辑器，将 `object` 摆放到房间中

2.  根据 GameMaker 版本的不同，添加 `Creation Code` 的方式也不同

    * GameMaker 8.0：`Ctrl + 右键 -> Creation Code...`
    * GameMaker 8.1：`右键 -> Creation Code...`

## 果引擎中的 Creation Code 规范

`Creation Code`中，存在着许多通用代码，记住它们将能帮助你更快更好地使用引擎，归类如下：

```gml
--------------- 通用 ---------------
     spr = 需要更换的精灵
     trg = 触发器编号
       h = 横向速度
       v = 纵向速度
     spd = 速度
     dir = 方向
    time = 时间（以帧为单位）
     num = 编号（boss编号，道具编号等，不常用）
   noDes = 出房间后是否不销毁（默认为出房间后直接销毁）
     dis = 出房间后销毁前移动的距离（默认为 0，不常用）

------------- 路径相关 -------------
     pth = 路径编号
     spd = 速度
    enda = 路径结束事件（0：停止运动；1：从头开始；2：从当前位置继续运动；3：反转路径）
     scl = 路径放大倍数

------------- 传送相关 -------------
  roomTo = 目标房间
    kind = 转场效果（可选）
   waprX = 传送 X 坐标（可选）
   warpY = 传送 Y 坐标（可选）
    text = warp 上方文字（可选）
   color = warp 上方文字颜色（可选）

--------------- 其他 -------------
setScale(横向缩放倍数, 纵向缩放倍数)
```
