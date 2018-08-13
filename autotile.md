# 自动贴图

## 简介

自动贴图是提高游戏制作效率的绝佳工具，它可以免去你给房间中砖块一个个贴图的烦恼。自动贴图的默认深度为 2000000，这使得你可以轻易地对不满意处进行覆盖与修改（要做坑什么的）。果引擎目前支持三种自动贴图模式：

- 纵向
- 四向
- 八向

## 使用方法

以下两种方法任选其一，同时使用时分房间设置（新手推荐）的贴图会覆盖集中设置的贴图。

### 分房间设置（新手推荐）

在房间中放入 `objBlockTile` （位于 rooms 文件夹下），并设置 Creation Code：

```gml
tile = bgGrass
```

使用该方法自动贴图时，背景图中的第一块贴图必须位于背景图的左上角，并且必须按照[贴图准备](autotile?id=贴图准备)中的说明准备贴图。

### 集中设置

考虑到执行效率问题，集中设置时不会自动设置贴图的方向（纵向/四向/八向）以及背景贴图间距，你需要自行计算。在脚本 `autoBlockTile` 中，仿照示例添加自动贴图的代码：

```gml
case rTraps:
    // 使用纵向贴图
    autotile(2, bgGrass)
    break
case rOnlineWarpSync:
    // 使用四向贴图，每块贴图大小为 32 像素
    autotile(4, bgMetal, 32)
    break
case rOnlineTriggerAndButton:
    // 使用四向贴图，每块贴图大小为 16 像素
    autotile(4, bgLine)
    break
case rOnlineSpike:
    // 使用八向贴图，每块贴图大小为 32 像素
    autotile(8, bgIsland, 32)
    break
case rOnlineBossSample:
    // 使用八向贴图，每块贴图大小为 16 像素
    autotile(8, bgVVVVVV)
    break
```

`autotile` 脚本可以接收 6 个参数：

- 贴图的方向类型（必填）
- 使用贴图的名称（必填）
- 使用贴图的模式（可选，32 \* 32 则需填 32，16 \* 16 可以不填）
- 贴图的深度（可选，默认 2000000）
- 提供的背景图中，每块贴图之间的间距（可选，默认为 0 ）
- 提供的背景图中，每行贴图的个数（可选，仅在四/八向贴图的 32 \* 32 像素模式中有效，默认为 4（四向）/ 8（八向））

## 贴图准备

### 纵向贴图

效果图：
![example2](_images/autotile/example2.png)

使用纵向贴图之前你需要准备如下贴图素材一张：

![dir2](_images/autotile/tile2_32.png)

- 大小为 32 \* 64 像素（无间距时）；
- 上半部分为顶部贴图，下半部分为其他贴图；
- 上半部分与下半部分之间可以有间距。

?> 在房间顶部的贴图会以底部贴图显示。

调用方法：

```gml
autotile(2, bg)
```

### 四向贴图

效果图：
![example4](_images/autotile/example4.png)

!> 使用四向贴图时应让贴图的边线尽可能小，因为四向贴图对内角不会做任何处理。

支持两种模式：

- 16 \* 16
- 32 \* 32

#### 使用 16 \* 16 素材

使用 16 \* 16 素材意味着每块砖（32 \* 32）的贴图都由 4 块 16 \* 16 的贴图构成，你只需要准备如下贴图一张：

![dir4_16](_images/autotile/tile4_16.png)

- 大小为 48 \* 48 像素（无间距时）；
- 周围 8 块为边界贴图，中间为内部贴图；
- 贴图大小为 16 \* 16 ，贴图之间可以有间距。

?> 如果想用这种方式，强烈建议使用[八向贴图](autotile?id=八向贴图)

调用方法：

```gml
autotile(4, bg)
```

#### 使用 32 \* 32 素材

使用 32 \* 32 素材意味着你对每块贴图能有更细粒度的控制，使游戏看起来更加丰富，你需要准备如下贴图一张：

![dir4_32](_images/autotile/tile4_32.png)

- 大小为 128 \* 128 像素（无间距时）；
- 贴图大小为 32 \* 32 ，贴图之间可以有间距。

看不清？看下图

![dir4_explanation](_images/autotile/explanation4_32.png)

这样你可以对不同位置的贴图进行一些随机的装饰，使地图看起来更加自然。

调用方法：

```gml
autotile(4, bg, 32)
```

### 八向贴图

效果图：
![example4](_images/autotile/example8.png)

支持两种模式：

- 16 \* 16
- 32 \* 32

#### 使用 16 \* 16 素材

使用 16 \* 16 素材意味着每块砖（32 \* 32）的贴图都由 4 块 16 \* 16 的贴图构成，你只需要准备如下贴图一张：

![dir4_16](_images/autotile/tile8_16.png)

- 大小为 48 \* 80 像素（无间距时）；
- 上面 48 \* 48 部分与四向贴图的一致（周围 8 块为边界贴图，中间为内部贴图），下面的 32 \* 32 部分为四个内角贴图；
- 贴图大小为 16 \* 16 ，贴图之间可以有间距。

调用方法：

```gml
autotile(8, bg)
```

#### 使用 32 \* 32 素材

使用 32 \* 32 素材意味着你对每块贴图能有更细粒度的控制，使游戏看起来更加丰富，你需要准备如下贴图一张：

![dir4_32](_images/autotile/tile8_32.png)

- 大小为 256 \* 192 像素（无间距时）；
- 贴图大小为 32 \* 32 ，贴图之间可以有间距。

!> 贴图的左上角为 0 号贴图！每行贴图个数以及贴图间距均可以设置，但顺序必须一致！

看不清？看下图

![dir8](_images/autotile/explanation8.png)
![dir8_explanation](_images/autotile/explanation8_32.png)

这样你可以对不同位置的贴图进行一些随机的装饰，使地图看起来更加自然。

调用方法：

```gml
autotile(8, bg, 32)
```

### 最上面的一排贴图不对！

有时，房间最上方的贴图会与你期望的不一样。此时可以参考 `rOnlineWarpWait` ，在房间中任意位置放置一个 objBlock，然后在其 Creation Code 中写入如下代码：

```gml
// 在房间上端放置一个长条 objBlock 以改变最上面的贴图状态
x = 0
y = -32
xs = room_width / 32
```

### 自定义不参与自动贴图的 obj

在默认情况下，以 objBlock/objVisibleTile 为父对象的 obj 均会参与到自动贴图中，如果你不希望你的自定义 obj 参与或影响自动贴图，可以前往 autotile_exclude 脚本设置：

```gml
// ...
switch (ind) {
    case blockPush:
    case blockConveyor:
    case blockConveyorL:
    case blockConveyorR:
    case myObject: // 不参与自动贴图
        return true
    default:
        return false
}
```
