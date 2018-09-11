# Object 文档

!> 勘误请点击左上角的 **Edit Document**，感谢！

### Blocks 砖块

#### objBlock 普通砖

放在房间的普通砖块，可以使 `player` 在上面行走。

!> 请务必使用 `objBlock` 而不是 `parent` 文件夹中的 `block`，后者会使 `player` 无法行走。

#### blockBullet 挡子弹砖

挡子弹专用砖。save 保护用。

#### blockMove 运动砖

在碰到`player`后会发生移动的砖。

Creation Code 参数：

```gml
spr = sprBlock // 可选，精灵
  h = 4 // 可选，横向速度
  v = 2 // 可选，纵向速度
spd = 3 // 可选，速度
dir = 0 // 可选，方向
```

#### blockInvisible 隐藏砖

碰到 `player` 之后才会显示。

Creation Code 参数：

```gml
spr = sprBlock // 可选，精灵
snd = sndBlockChange // 可选，音效
```

#### blockFake 假砖

碰到 `player` 之后会消失。

Creation Code 参数：

```gml
spr = sprBlock // 可选，精灵
snd = sndBlockChange // 可选，音效
```

#### blockPush 可推动砖

可以推动的砖，能够随着传送带和木板移动。

!> 1.8 版本中仍然有 bug

Creation Code 参数：

```gml
frc = 1 // 可选，摩擦力，默认为 1
wrap = false // 可选，如果设置为 true，纵向掉出房间后会从另一端出现，默认为 false
grav = 0.4 // 可选，重力，默认为 0.4
maxVspeed = 10 // 可选，最大下落速度，默认为 10
```

#### BlockConveyorL 左向传送带

Creation Code 参数：

```gml
spr = sprBlock // 可选，精灵
h = -2 // 可选，传送带速度，默认为 -2
```

#### BlockConveyorR 右向传送带

Creation Code 参数：

```gml
spr = sprBlock // 可选，精灵
h = 2 // 可选，传送带速度，默认为 2
```

#### miniBlock 小砖

与普通砖没啥区别，就是小点。

### Killers 障碍物

#### deliciousFruit

好吃的水果。

除了[默认的 Creation Code ](cc.md)之外，还支持额外的 Creation Code 参数：

```gml
bounce = true // 碰到墙壁是否反弹
wrap = true // 如果为 true，出屏后会从另一端出现
```

#### spikeDown, spikeLeft, spikeUp, spikeRight

#### miniSpikeDown, miniSpikeLeft, miniSpikeUp, miniSpikeRight

普通的障碍物。其中，八种四方向尖刺的精灵可以参考[自动更换刺的精灵](autosprite.md)在脚本 `autoSpikeSprite` 中根据房间来自动更换。

?> 现在可以直接改变这些刺的精灵而不会失效了。当然，强烈建议你使用 `autoSpikeSprite` 脚本进行自动配置。

?> 引擎中任意刺都可以当作触发刺使用啦！详情请见 [新触发系统](trigger.md)

#### borderKiller

用于 player 掉到屏幕外时杀死 `player`。用于在大房间中模拟普通的出房间死亡事件。

1.  使用普通的刺，当玩家碰刺时即死。

    ![normal spike](_images/border1.png)

2.  使用 `borderKiller`，当玩家在视野之外才死。

    ![outside view](_images/border2.png)

### Triggers 触发器

#### objTrigger

触发器。请参考 [新触发系统](trigger.md)

Creation Code 参数：

```gml
trg = 1 // 必填，触发器编号
snd = sndCherry // 可选，触发时音效
xs = 2 // 可选，水平缩放
ys = 2 // 可选，垂直缩放
```

#### objSequenceTrigger

时序触发器。默认可触发 20 次。请参考 [新触发系统](trigger.md)

```gml
// 以下代码中 i >= 1
trg[i] = 1 // 必填，第 i 个触发器编号
time[i] = 50 // 必填，从编号 i 触发到编号 i + 1 触发所用的时间
snd[i] = sndBlockChange // 可选，第 i 个触发器的触发音效
xs = 2 // 可选，水平缩放
ys = 2 // 可选，垂直缩放
```

#### objButton

按钮触发器。当 `player` 射击该按钮后，对应的机关将会被触发。（不支持 `key` 参数）
Creation Code 参数：

```gml
trg = 1 // 必填，触发器编号
spr = sprGreenButtonLeft // 可选，精灵
```

#### trgMultiplePath

多重路径刺。可以按顺序被多个触发器所触发。

Creation Code 参数：

```gml
// 以下代码中 i >= 1
spr = sprSpikeUp // 必填，使用的精灵
trg[i] = 1 // 必填，第 i 个触发器编号
pth[i] = pU1 // 必填，第 i 个路径的名称
spd[i] = 6 // 必填，第 i 个路径中的运动速度
enda[i] = PATH_ACTION_END // 可选，第 i 个路径的路径结束事件
scl[i] = 2 // 可选，第 i 个路径的路径缩放倍数
```

在常量表中可找到[路径结束事件](constant?id=路径结束动作)的可能值

#### trgBlock

可以被触发的砖。

?> 如果 player 触碰到在移动中的 trgBlock 则会判断为死亡。

路径模式下，Creation Code 参数：

```gml
spr = sprBlock // 必填，使用的精灵
trg = 1 // 必填，触发器编号
pth = pD1 // 必填，路径名称
spd = 7 // 必填，运动速度
enda = PATH_ACTION_STOP // 可选，路径结束事件
scl = 1 // 可选，路径缩放倍数
move = true // 可选，是否防止剧透（玩家死亡之后会沿着当前方向移动，不会停止/转弯）
```

更多触发模式请参考 [新触发系统](trigger.md)

#### trgBlockFake

触发式假砖。未被触发时与砖块无异，但触发之后会变成假砖。

Creation Code 参数：

```gml
trg = 1 // 必填，触发器编号
spr = sprBlock // 可选，使用的精灵
```

#### trgBlockInvisible

触发式隐形砖。未被触发时与空气无异，但触发之后会变成隐形砖。

Creation Code 参数：

```gml
trg = 1 // 必填，触发器编号
spr = sprBlock // 可选，使用的精灵
```

### Gimmicks 功能

这个文件夹中包含颠倒重力、水、藤蔓、板子等 obj。

#### objGravUp

颠倒重力。视角会随之旋转。

#### objGravDown

返回正常重力。视角会随之还原。

#### objWater

普通水。跳跃高度为二段跳高度，出水有二段。

Creation Code:

```gml
spd = 2 // 可选，水中最大下落速度
```

#### objWaterNo2ndJump

二段水。跳跃高度为二段跳高度，出水无二段。

Creation Code:

```gml
spd = 2 // 可选，水中最大下落速度
```

#### objWaterNoJump

无跳水。只会降低移动速度，而不恢复跳跃次数。

Creation Code:

```gml
spd = 2 // 可选，水中最大下落速度
```

#### objInfiniteJump

碰到玩家之后使之能够无限跳。

#### objInfiniteJumpDisable

碰到玩家之后使之不能无限跳。

#### objWalljumpR、objWallJumpL

藤蔓

#### objMovingPlatform

普通木板。

Creation Code 参数：

```gml
// 直接赋值，则会直接运动
hspeed = 3 // 横向速度
vspeed = 3 // 纵向速度
// 使用 h、v，则会等玩家站上再运动
h = 3 // 触碰后的横向速度
v = 3 // 触碰后的纵向速度
```

#### objPathPlatform

沿路径运动的木板。

Creation Code 参数：

```gml
// 直接以 spd 速度沿 pth 运动。
path_start(pth, spd, enda, 0);
// 当玩家站上板之后，再开始运动
pth = pD1 // 必填，路径名称
spd = 7 // 必填，运动速度
```

其他可选参数：

```gml
enda = PATH_ACTION_STOP // 路径结束事件
scl = 1 // 路径缩放倍数
move = false // 是否防止剧透（玩家死亡之后会沿着当前方向移动，不会停止/转弯）
draw = false // 是否绘制路径
color = c_black // 绘制路径的颜色
width = 1 // 绘制路径的宽度
```

#### objRoundingCherry

生成一个苹果圈。该 obj 需放在苹果圈的圆心处。

Creation Code 参数：

```gml
num = 15 // 必填，苹果总数
rad = 100 // 必填，苹果圈半径
spd = 0.72 // 必填，绕圈速度
ang = 0 // 可选，初始角度（0~360）
spr = sprCherry // 可选，苹果的精灵（默认为普通红色苹果）
mode = 'normal' // 可选，共有两种模式：'normal'/'center'
```

- 改变 `ang` 可以改变各个苹果在苹果圈上的刷新位置
- `spd` 的单位为 度/帧，如果需要在 10 秒内转 360 度，则 spd = 360/(10\*50) = 0.72
- normal 模式为普通苹果圈，center 模式为旋转半径 0~rad 周期性变化的苹果圈

#### objPathSpike

生成一系列均匀分布的按照某个 path 运动刺。该 obj 需放在 path 的起始点。

Creation Code 参数：

```gml
num = 5 // 刺总数（默认为 1，如果用这个 obj 来制作伸缩刺可以省略这个参数）
pth = p9_1 // 运动路径
off = 0 // 初始位置（改变这个值可以改变各个刺在路径上的刷新位置，0~1）
spd = 2 // 各刺沿路径移动的速度
spr = sprSpikeUp // 刺的精灵（可选，默认情况下为朝上的普通刺）
```

#### objJumpRefresher

+1 跳。

Creation Code 参数：

```gml
time = 50 // 刷新时间
```

### Host 主机专用

该文件夹中的 `object` 仅对房主生效。

| object 名称     | 用途   |
| --------------- | ------ |
| blockHost       | 砖     |
| spikeDownHost   | 刺     |
| spikeLeftHost   | 刺     |
| spikeUpHost     | 刺     |
| spikeRightHost  | 刺     |
| warpHost        | 传送点 |
| playerStartHost | 出生点 |
| freeButtonHost  | 按钮   |

### Guest 非主机专用

该文件夹中的 `object` 仅对非房主生效

| object 名称      | 用途   |
| ---------------- | ------ |
| blockGuest       | 砖     |
| spikeDownGuest   | 刺     |
| spikeLeftGuest   | 刺     |
| spikeUpGuest     | 刺     |
| spikeRightGuest  | 刺     |
| warpGuest        | 传送点 |
| playerStartGuest | 出生点 |
| freeButtonGuest  | 按钮   |

### Saves 存档点

引擎中的存档点共有 3 种模式：

- 射击模式：子弹射击存档（默认）
- 触碰模式：玩家触碰存档
  Creation Code 参数：
  ```gml
  mode = 'touch'
  ```
- 按键模式：玩家触碰存档时按键存档
  Creation Code 参数：
  ```gml
  mode = 'press'
  key = 'S' // 可选，默认为按 S 键存档，该参数可为字母（如 'S'）或虚拟键码（如 vk_up）
  ```

4 种状态：

- 红色：默认
- 黄色：说明该存档点需要所有玩家共同射击才能生效。
- 蓝色：说明其他玩家已存档（但是与你无关）
- 绿色：存档成功

#### savePoint

普通单人存档点，有 `红`、`蓝`、`绿` 三种状态。

#### savePointWait

等待存档。所有人射击才能存档成功，存档位置以最后一个人的位置为准。有 `红`、`黄`、`绿` 三种状态。

#### savePointSync

同步存档。当一个人存档之后，其他所有人均可以通过重置游戏传送到该存档。有 `红`、`绿` 两种状态。

### Warps 传送点

在果引擎 2.0 版中，取消了 warpX/warpY 参数，取而代之的是 **有编号的 `objPlayerStart` **。即你可以在 warp 中指定一个编号 `num`，当玩家进入该传送点时，则会被传送到对应房间中编号为 `num` 的 `objPlayerStart` 位置。

#### warp

普通 warp。

Creation Code 参数：

```gml
r = rTraps // 必填，传送到的房间名称。如果是房间内传送，则填 -1。
num = 0 // 可选，传送到 objPlayerStart 的编号
kind = 0 // 可选，使用的房间转场效果
clearSpeed = false // 可选，是否清除玩家速度
screens = 1 // 可选，平移房间的个数
text = "text" // 可选，绘制文字
color = c_red // 可选，文字颜色
```

关于 `screens` 参数的说明：

![warp](_images/warp.png)

如图所示，假设你想从 room1 中的 (800, 912) 处传送到 room2 中的 (0, 304) 处，不仅得将 x 坐标设为 0，还需要将 y 坐标向上平移一个屏幕的距离（608 像素）。这样可以使 `player` 的纵坐标在屏幕上看起来没有变化，增强游戏的连续性。

在这种情况下，将 `screens` 设置为 -1 即可。

?> 关于房间转场效果，可以参考[转场效果](transition.md)

#### warpSync

传送后会将其他玩家一并传送（包括死亡的）。

#### warpWait

所有玩家一起进入才会生效的传送点。

#### warpWaitingBG

在玩家进入 warpWait 后显示的等待画面。

#### borderWarp

#### borderWarpSync

#### borderWarpWait

隐形 warp。如果将 `warp` 放在房间外，你往往需要对其进行拉伸。而由于 `warp` 的形状不规则，拉伸之后会导致在某些角度下传送失败。因此，在房间边缘需要传送到另一个房间时，请使用 `borderWarp*`。

Creation Code 参数：

```gml
r = rTraps // 必填，传送到的房间名称。
kind = 0 // 可选，使用的房间转场效果
width = 1 // 可选，目标房间的宽度与视野宽度的比值，通常情况下可以用 room_width / 800 代替
height = 1 // 可选，目标房间的高度与视野高度的比值，通常情况下可以用 room_height / 800 代替
screens = 1 // 可选，平移房间的个数
```

?> 关于 screens 参数，可以参考[这里](objectref?id=warp)

!> 使用该 obj 时，默认将 player 传到目标房间的房间边缘。如果想要 player 传送到目标房间的 objPlayerStart 位置，可以设置 `mode = 'normal'`。

#### warpStart

用于选关界面的 warp。

Creation Code 中：

- dif 表示游戏难度（-1 – Load，0 – Medium，1 – Hard，2 – Very Hard，3 - Impossible）
- text 表示在 warp 上方需要绘制的文字。

#### bossWarp

拿到特定的 `bossItem` 才会出现的 `warp`，Creation Code 参考普通的 `warp` 即可，该 `object` 默认不可见。因此，你需要在同房间 boss 的 destroy 事件中写入：

```gml
bossWarp.visible = true
```

#### bossWarpSync

拿到特定的 `bossItem` 才会出现的 `warpSync`，Creation Code 参考普通的 `warpSync` 即可，该 `object` 默认不可见。因此，你需要在同房间 boss 的 destroy 事件中写入：

```gml
bossWarpSync.visible = true
```

#### warpCount

拿到特定数量的 bossItem 或 secretItem 才会开启的 warp。

在普通 warp 的 Creation Code 的基础上，还需增加：

```gml
countBoss = true // 是否统计 bossItem 数量
countItem = false // 是否统计 secretItem 数量
total = 8 // 指定数量
```

### Items 道具

这个文件夹中包含了各种在游戏中能获得的道具以及相关 obj。

#### bossItem

boss 被击败时所创建的 item，player 拿到之后则会记录指定编号的 boss 已被击败。

Creation Code 参数：

```gml
num = 1 // 必填，道具编号
spr = sprBossIcon1 // 可选，精灵
```

该 obj 默认不可见。因此，你需要在同房间 boss 的 destroy 事件中写入：

```gml
bossItem.visible = true
```

#### bossItemViewer

用于在房间中显示某 boss 是否被击败。

Creation Code 参数：

```gml
num = 1 // 必填，boss编号
spr = sprBossIcon1 // 可选，使用精灵
```

#### bossBlock

当拿到对应 boss 的 item 的时候，会自动摧毁的 block。

Creation Code 参数：

```gml
num = 1 // 必填，boss编号
spr = sprBlock // 可选，使用精灵
```

#### secretItem

隐藏道具。

Creation Code 参数：

```gml
num = 1 // 必填，隐藏道具编号
spr = sprItemIcon1 // 可选，使用精灵
```

#### secretItemViewer

用于在房间中显示某隐藏道具是否已获取。

Creation Code 参数：

```gml
num = 1 // 必填，隐藏道具编号
spr = sprItemIcon1 // 可选，使用精灵
```

### Room 房间杂物

#### objPlayerStart

默认出生点。

Creation Code 参数：

```gml
autoSave = false // 是否自动存档
wrap = false // 设置为 true 时，出房间后会从另一端出现而不是死亡
infJump = false // 是否开启无限跳
forceSync = false // 是否强制同步 player
```

#### objPlayMusic

音乐播放，使用该 obj 会覆盖 `music_config` 中设置的 BGM。

Creation Code 参数：

```gml
// 当前房间的 BGM
bgm = BGM_Rock
```

#### objSpikeSprite

用于给房间中的刺更换精灵。

Creation Code 参数：

```gml
// 当前房间中刺的精灵，32 * 32，原点位于 (16, 16)
spr = sprSpikeM
// 可选，当前房间中小刺的精灵
miniSpr = sprMiniSpikeM
// 可选，当前房间中刺的精灵播放速度（image_speed）
ispd = 0
// 更换主机专用刺，例如 spikeDownHost
sprH = ...
miniSprH = ...
ispdH = ...
// 更换非主机专用刺，例如 spikeDownGuest
sprG = ...
miniSprG = ...
ispdG = ...
```

#### objBlockTile

用于给房间中的砖更换贴图。素材准备请参考 [自动贴图](autotile.md)，贴图模式会自动设置。

Creation Code 参数：

```gml
// 当前房间中砖使用的贴图
tile = bgLine
// 当前房间中主机专用砖使用的贴图
tileH = bgGrass
// 当前房间中非主机专用砖使用的贴图
tileG = bgCastle
```

#### objCamera

在大房间中使用，使得游戏的视角能根据玩家切换房间而移动。

#### objSmoothView

平滑视角，通常放在大房间中使用。在默认情况下，该 obj 会启用视野平滑效果。

Creation Code 参数：

```gml
noSmooth = true // 是否关闭视野平滑效果
```

!> 该 `object` 会覆盖 `objCamera` 的效果。

#### objResetSync

联机模式下，某一玩家重置游戏后会使得其他玩家自动重置游戏。

#### objResetWait

联机模式下，当所有人选择重置游戏时，游戏才会重置。

?> BOSS 房间中强烈推荐

#### objGameClear

玩家碰到之后即将 `global.clear` 设置为 `true`，停止游戏时间的计算。

### Visual 视觉效果

这个文件夹中包含了一些常见的游戏效果。

#### objShake

通过脚本 screenShake 调用，请参考脚本 [screenShake](scriptref?id=screenshaketime-shakex-shakey)。

#### objScreenFlash

通过脚本 screenFlash 调用，请参考脚本 [screenFlash](scriptref?id=screenflashtime)。

#### objShadow

通过脚本 createShadow 调用，请参考脚本 [createShadow](scriptref?id=createshadowalpha_speed-scale_speed)。

#### objViewFlipper

翻转视角。

Creation Code 参数：

```gml
angle = 180 // 可选，旋转度数，默认 180
time = 15 // 可选，旋转时间，默认 15
```

### Parent 父对象

| 名称              | 用途                             |
| ----------------- | -------------------------------- |
| platform          | 板子父对象                       |
| block             | 砖块父对象（不要直接放在房间中） |
| blockConveyor     | 传送带父对象                     |
| objTriggerable    | 所有能被触发的 `object` 的父对象 |
| playerKiller      | 障碍物父对象                     |
| playerKillerHost  | 仅对房主生效的障碍物父对象       |
| playerKillerGuest | 仅对非房主生效的障碍物父对象     |
| roomChanger       | 传送点父对象                     |
| roomChangerSync   | 同步传送点父对象                 |
| roomChangerWait   | 等待传送点父对象                 |
| bulletParent      | 子弹父对象                       |
| objWaterParent    | 水父对象                         |

### Bosses BOSS

#### miku

这个文件夹中包含了与 miku 耐久有关的各种 obj。

> 引擎重置了耐久的时间轴。原版 yuuutu 引擎的自带耐久中有四个时间轴，总共几百个时间轴事件；在本引擎中，仅有 1 个时间轴与 16 个时间轴事件，相信这比原来的会更容易看懂。

如果想学习如何制作耐久，可以先参考一下[耐久制作基础教程](avoidance.md)。

#### objHPBar

用来绘制 boss 血条。这仅仅是一个如何使用 `drawLife` 脚本的范例

#### objBossSample

BOSS 示例。

#### objBossSampleBuffed

强化 BOSS 示例。

#### objBossSampleOnline

联机 BOSS 示例。

#### objBossBullet

BOSS 发射的弹幕 obj。

### System 系统

#### options

| 名称            | 用途           |
| --------------- | -------------- |
| objOptionButton | 设置房间的按钮 |
| objConfigBar    | 设置调整滑块   |
| objMusic        | 音乐图标显示   |
| objSound        | 音效图标显示   |

#### title

| 名称                | 用途                           |
| ------------------- | ------------------------------ |
| objTitleController  | rTitle 控制器                  |
| objLanguageSwitch   | 语言切换按钮                   |
| objControllerButton | 登录/注册/加入房间等操作的按钮 |

#### lobby

| 名称               | 用途          |
| ------------------ | ------------- |
| objLobbyController | rLobby 控制器 |
| objLobbyRoomDrawer | 房间列表绘制  |

#### room

| 名称              | 用途         |
| ----------------- | ------------ |
| objRoomController | rRoom 控制器 |
| objRoomProfile    | 玩家信息绘制 |

#### player

##### player

初始化参数参考 [playerInit](scriptref?id=player)

其他可能有用的变量如下：

```gml
onBlock = 是否站在砖块上
onPlatform = 是否站在板子上
onConveyor = 是否站在传送带上
onIvy = 是否在藤蔓上
inWater = 是否在水中
isRunning = 是否移动
isJumping = 是否跳跃
curJumps = 当前跳跃数
shouldDieWhenOutsideRoom = 出房间时是否死亡
shouldWrapWhenOutsideRoom = 出房间时是否应从房间另一侧出现

// 例如：
if (player.isJumping && player.curJumps == 2) {
  // 在二段跳时触发...
}
if (player.isJumping && player.inWater) {
  // 在水中跳跃时触发...
}
```

##### bloodEmitter

血液喷泉生成器。

##### objBlood

血迹。

##### bullet

玩家发射的子弹。

#### online

#### menu

##### objMenuSelect / objMenuSelect2

均用于在 `rMenu` 中绘制死亡次数、时间、boss 图标等。

- menuSelect 为跳刺选难度，menuSelect2 为直接选难度
- 在 create 中可以指定各个 boss 图标

通过在 draw 事件中简单的改动，也可以绘制隐藏道具的图标。

首先，在 create 中利用脚本 `loadIcons` 获取了用于 draw 事件的存档信息：

```
  menu_difficulty[i]: 第 i 个存档的难度
  menu_clear[i]: 第 i 个存档是否通关
  menu_boss[i,j]: 第 i 个存档的第 j 个 boss 是否被击败
  menu_item[i,j]: 第 i 个存档的第 j 个 item 是否被拿到
```

只用在 `Draw` 事件中根据 `menu_item[i, j]` 来判断图标并绘制即可

#### 杂项

| obj 名称        | 用途                  | 备注                                                                  |
| --------------- | --------------------- | --------------------------------------------------------------------- |
| objInit         | 在 rInit 中初始化游戏 |                                                                       |
| objLoad         | 在 rLoad 中读取存档   |                                                                       |
| world           | 游戏的全局控制器      | 参考 [World](scriptref?id=world)                                      |
| objEffectParent | 全局效果控制器        | 控制 [flashObject](scriptref?id=flashobjectflash_time-flash_count) 等 |
| objGameover     | GAMEOVER！            |                                                                       |
| objDeathSound   | 死亡时音效控制        |                                                                       |
| objNothing      | 啥都不干              |                                                                       |
| objDebug        | 调试控制台            | 参考 [调试功能](debug.md)                                             |
