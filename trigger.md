# 新触发系统

触发是 I Wanna 中各种坑实现的基础。果引擎 2.0 版重写了触发系统以提高运行时效率，使用起来几乎与原来一致。[查看使用说明](/trigger?id=trg-与-key-一体化)

## 简介

触发系统主要包含两种 `object`：触发器与触发对象，它们通过 `触发事件` 联系到一起。该系统的运作方式可概括为下图：

![trigger system](_images/trigger.png)

- 触发器指一类会响应 `player` 动作的 `object`，它可以在某种条件下发出带有一定标记（`trg`）的 `触发事件`。包括：

  - 隐形的 `trigger`，当 `player` 与之相碰撞时，发出 `触发事件`；
  - 延时的 `trigger`，当 `player` 与之相碰撞之后，过一段时间再发出 `触发事件`；
  - 可见的 `button`，当 `player` 射击击中时，发出 `触发事件`；
  - ...

* 触发对象是一类可以响应 `触发事件` 的 `object`，包括：

  - 在触发后会运动的刺
  - 在触发后会运动的板子
  - 在触发后会被创建的隐形砖
  - 在触发后会做任何动作的任意 `object`

## trg 与 key 一体化

在之前的版本中，`keyTrigger` 经常用于回头坑，因为它在指定 `trg` 的 `freeTrigger` 触发之前不会对 `player` 的任何动作作出反应。而在 2.0 版中，`freeTrigger` 与 `keyTrigger` 合并为了 `objTrigger`。`objTrigger` 的使用方法与 `freeTrigger` 完全一致。并且，当在 `Creation Code` 中指定 `key` 时，即可当做 `keyTrigger` 使用。

普通 objTrigger：

```gml
trg = 1
ys = 6
```

当作 keyTrigger 使用：

```gml
trg = 2
key = 1
ys = 6
```

为了更方便地调试触发机关，在[调试模式](trigger?id=调试模式以及报错)下 `objTrigger` 会有一些额外的处理。

## playerKiller 均可被触发？

这也是果引擎 2.0 版中触发系统最明显的变化。你可以将任意 `playerKiller` 放置在房间中，然后使用 `trg` 使其触发。支持 4 种模式：

- 速度
- 路径
- 缩放
- 旋转

### 速度模式

触发之后会以指定速度运动。有两种触发方式：

- 横向/纵向速度触发：

  Creation Code 参数：

  ```gml
  // 必填，触发器编号
  trg = 1
  // 可选，横向速度
  h = 4
  // 可选，纵向速度
  v = 4
  ```

- 速度/方向触发：

  Creation Code 参数：

  ```gml
  // 必填，触发器编号
  trg = 1
  // 必填，速度
  spd = 6
  // 可选，方向，默认向右
  dir = 45
  ```

### 路径模式

触发之后会沿着给定路径运动。

Creation Code 参数：

```gml
// 必填，触发器编号
trg = 1
// 必填，路径名称
pth = pCircle
// 必填，路径运动速度
spd = 5
// 可选，路径缩放大小
scl = 1
// 可选，路径结束动作
enda = PATH_ACTION_STOP
// 是否防止剧透（玩家死亡之后会沿着当前方向移动，不会停止/转弯）
move = true
```

### 缩放模式

触发之后会参照指定中心进行放大/缩小。公共参数如下：

Creation Code:

```gml
// 必填，触发器编号
trg = 1
// tarx / tary 至少有一个不为空
// 可选，x 方向缩放量
tarx = 3
// 可选，y 方向缩放量
tary = 3
// 可选，使用的精灵
spr = sprSpikeUp
// 可选，快速设置缩放中心（会被 cx/cy 覆盖）
origin = 5
// 可选，缩放中心与精灵中心的横向偏移量
cx = 0
// 可选，缩放中心与精灵中心的纵向偏移量
cy = 0
```

其中，origin 的值为 1 - 9，分别对应精灵的左上角，中上，右上角……见下：

```
1 2 3
4 5 6
7 8 9
```

触发方式有两种：

- 缩放时间触发：

  Creation Code 参数：

  ```gml
  // 必填，缩放到目标缩放量所需要的时间（帧）
  time = 50
  ```

- x, y 缩放速度触发：

  Creation Code 参数：

  ```gml
  // xsp 与 ysp 不能都为空
  xsp = 0.04 // 触发之后 x 方向的缩放速度
  ysp = 0.04 // 触发之后 y 方向的缩放速度
  ```

对于这几个参数的额外说明：

假设你需要将某刺在 1 秒内缩放到原来的 3 倍大小，那么 tarx，tary 的值均为 3。

- 对于缩放时间方式，time = 50；
- 对于缩放速度方式，xsp 与 ysp 的值均为：(3 – 1) / 50 = 0.04。

### 旋转模式

触发之后会沿着指定中心旋转一定角度。

Creation Code 参数：

```gml
// 必填，触发器编号
trg = 7
// 必填，旋转角度
angle = 90
// 必填，旋转时间
time = 20
// 可选，使用的精灵
spr = sprSpikeUp
// 可选，快速设置缩放中心（会被 cx/cy 覆盖）
origin = 5
// 可选，旋转中心与 spr 中心的横向偏移量
cx = 0
// 可选，旋转中心与 spr 中心的纵向偏移量
cy = 0
```

其中，origin 的值为 1 - 9，分别对应精灵的左上角，中上，右上角……见下：

```
1 2 3
4 5 6
7 8 9
```

?> 当 playerKiller 被直接摆放在房间外时，引擎会自动设置 `noDes = true`，确保它能被正确地创建。

## 时序触发器

该 `object` 可以在 `Objects -> triggers -> objSequenceTrigger` 找到。用于触发一些按特定顺序出现的坑。

应用场景举例：

`player` 碰到时直接触发 `trg = 1` 的`触发事件`，1 秒之后触发 `trg = 2`的`触发事件`

```gml
trg[1] = 1
time[1] = 50
trg[2] = 2
```

`player` 碰到时不触发任何事件，1 秒之后触发 `trg = 1` 的触发事件，3 秒之后触发 `trg = 2` 的触发事件：

```gml
trg[1] = 9999
time[1] = 50
trg[2] = 1
time[2] = 100
trg[3] = 2
```

## 调试模式以及报错

当游戏以调试模式运行时，`objTrigger` 会显示当前的 `trg` 以及 `key` 以便观察：

![trigger debug](_images/trigger-debug.jpg)

当 `objTrigger` 等 `object` 的 `Creation Code` 中没有 `trg` ，或者 `trg` 为 `0` 时，引擎会捕捉到这类错误并抛出一个错误，如：

![trigger error](_images/trigger-error.jpg)

此时在位于 `rOnlineSpike` (384, 480) 处的 `objTrigger` 的 `Creation Code` 中补充必要的参数即可。
