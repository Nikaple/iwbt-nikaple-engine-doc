# 自动贴图

## 使用方法

自动贴图是提高游戏制作效率的绝佳工具，它使得你可以在脚本 `autoBlockTile` 中对所有房间的自动贴图做统一处理。自动贴图的默认深度为 2000000，这使得你可以轻易地对不满意处进行覆盖与修改（要做坑什么的）。果引擎目前支持三种自动贴图模式：

- 纵向
- 四向
- 八向

你可以在脚本 `autoBlockTile` 中，仿照示例添加自动贴图的代码：

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

## 纵向贴图

效果图：
![example2](_images/autotile/example2.png)

使用纵向贴图之前你需要准备如下贴图素材一张：

![dir2](_images/autotile/tile2_32.png)

- 大小为 32 \* 64 像素；
- 上半部分为顶部贴图，下半部分为其他贴图。

?> 在房间顶部的贴图会以底部贴图显示。

调用方法：

```gml
autotile(2, bg)
```

## 四向贴图

效果图：
![example4](_images/autotile/example4.png)

!> 使用四向贴图时应让贴图的边线尽可能小，因为四向贴图对内角不会做任何处理。

支持两种模式：

- 16 \* 16
- 32 \* 32

### 使用 16 \* 16 素材

使用 16 \* 16 素材意味着每块砖（32 \* 32）的贴图都由 4 块 16 \* 16 的贴图构成，你只需要准备如下贴图一张：

![dir4_16](_images/autotile/tile4_16.png)

- 大小为 48 \* 48 像素；
- 周围 8 块为边界贴图，中间为内部贴图。

?> 如果想用这种方式，强烈建议使用[八向贴图](autotile?id=八向贴图)

调用方法：

```gml
autotile(4, bg)
```

### 使用 32 \* 32 素材

使用 32 \* 32 素材意味着你对每块贴图能有更细粒度的控制，使游戏看起来更加丰富，你需要准备如下贴图一张：

![dir4_32](_images/autotile/tile4_32.png)

看不清？看下图

![dir4_explanation](_images/autotile/explanation4_32.png)

这样你可以对不同位置的贴图进行一些随机的装饰，使地图看起来更加自然。

调用方法：

```gml
autotile(4, bg, 32)
```

## 八向贴图

效果图：
![example4](_images/autotile/example8.png)

支持两种模式：

- 16 \* 16
- 32 \* 32

### 使用 16 \* 16 素材

使用 16 \* 16 素材意味着每块砖（32 \* 32）的贴图都由 4 块 16 \* 16 的贴图构成，你只需要准备如下贴图一张：

![dir4_16](_images/autotile/tile8_16.png)

- 大小为 48 \* 80 像素；
- 上面 48 \* 48 部分与四向贴图的一致（周围 8 块为边界贴图，中间为内部贴图。），下面的 32 \* 32 部分为四个内角贴图。

调用方法：

```gml
autotile(8, bg)
```

### 使用 32 \* 32 素材

使用 32 \* 32 素材意味着你对每块贴图能有更细粒度的控制，使游戏看起来更加丰富，你需要准备如下贴图一张：

![dir4_32](_images/autotile/tile8_32.png)

!> 贴图的左上角为 0 号贴图！每行贴图个数以及贴图间距均可以设置，但顺序必须一致！

看不清？看下图

![dir8](_images/autotile/explanation8.png)
![dir8_explanation](_images/autotile/explanation8_32.png)

这样你可以对不同位置的贴图进行一些随机的装饰，使地图看起来更加自然。

调用方法：

```gml
autotile(8, bg, 32)
```
