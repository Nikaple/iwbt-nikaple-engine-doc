# Object 文档

关于 GameMaker 基本操作，可以参考[新手教程](http://tieba.baidu.com/p/2885308275)。

## Object 详情

1.

### Blocks 砖块

#### objBlock 普通砖

放在房间的普通砖块，可以使 `player` 在上面行走。

!> 请务必使用 `objBlock` 而不是 `parent` 文件夹中的 `block`，后者会使 `player` 无法行走。

#### blockBullet 挡子弹砖

挡子弹专用砖。save 保护用。

#### blockPush 可推动砖

可以推动的砖，能够随着传送带和木板移动。

Creation Code 参数：

```gml
frc = 1 // 可选，摩擦力，默认为 1
wrap = true // 可选，如果设置为 true，纵向掉出房间后会从另一端出现，默认为 false
grav = 0.4 // 可选，重力，默认为 0.4
maxVspeed = 10 // 可选，最大下落速度，默认为 10
```

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
```

#### blockFake 假砖

碰到 `player` 之后会消失。

Creation Code 参数：

```gml
spr = sprBlock // 可选，精灵
```

#### BlockConveyorL 左向传送带

Creation Code 参数：

```gml
h = -2 // 可选，传送带速度，默认为 -2
```

#### BlockConveyorR 右向传送带

Creation Code 参数：

```gml
h = 2 // 可选，传送带速度，默认为 2
```

#### miniBlock 小砖

与普通砖没啥区别，就是小点。

### Killers 障碍物

#### spikeDown, spikeLeft, spikeUp, spikeRight

普通的障碍物。其中，四方向尖刺的精灵可以在脚本`autoSpikeSprite`中根据房间来自动更换。

?> 现在可以直接改变这些刺的精灵而不会失效了。当然，强烈建议你使用`autoSpikeSprite`脚本进行自动配置。

?> 引擎中任意刺都可以当作触发刺使用啦！速度模式以及路径模式均能支持！

#### deliciousFruit

#### miniSpike

这个文件夹中包含了 4 种小刺。

#### borderKiller

用于 player 掉到屏幕外时杀死 player。在普通的 800*608 房间中，player 并不是一碰到屏幕边缘就死，而是会再往外移动一小段距离。而当房间大小较大，例如 800*1216 时，普通的杀死玩家的方法是在屏幕外放上 spikeDown / playerKiller / damageBlock 之类的 obj：（在 player 碰到刺的同时死亡）这样则会在 player 碰到屏幕边缘的同时就判定 player 死亡，这与普通掉出房间的判定不同。这时我们需要利用 borderKiller，使 player 在掉出屏幕之后再判定死亡：（在 player 掉出屏幕之后才死亡）

### Triggers 触发器

#### objTrigger

#### objSequenceTrigger

请参考 [新触发系统](trigger.md)

#### objButton

按钮触发器。当 `player` 射击该按钮后，对应的机关将会被触发。（不支持 `key` 参数）
`Creation Code` 参数：

```gml
spr = sprGreenButtonLeft
trg = 1
```

#### trgMultiplePath

多重路径刺。可以按顺序被多个触发器所触发，最大触发次数由 create 中的 maxTraps 变量决定。

`Creation Code` 参数：

```gml
// 使用的精灵
spr = sprSpikeUp
// 第 i 个触发器编号 （从 i=1 开始，按顺序触发 i=2，i=3，…的 trg）
trg[i] = 1
// 第 i 个路径的名称
pth[i] = pU1
// 第 i 个路径中的运动速度
spd[i] = 6
// 第 i 个路径的路径结束事件（0：停止运动；1：从头开始；2：从当前位置继续运动；3：反转路径）
enda[i] = 0
// 第 i 个路径的路径缩放倍数（默认为 1，例如将 pU1 放大两倍则为向上移动两格）
scl[i] = 2
```

#### trgScale

缩放刺。当触发之后会放大/缩小。两种触发方式：缩放时间 / x, y 缩放分速度。

缩放时间触发，Creation Code 参数：

```gml
// 使用的精灵
spr = sprSpikeUp
// 触发器编号
trg = 1
// 触发之后 x 方向的目标缩放量
tarx = 2
// 触发之后 y 方向的目标缩放量
tary = 2
// 缩放到目标缩放量所需要的时间（帧）
time = 50
// 缩放中心位置
origin = 5
```

x, y 缩放速度触发。Creation Code 参数：

```gml
// 使用的精灵
sprite_index = sprSpikeUp
// 触发器编号
trg = 1
// 触发之后 x 方向的目标缩放量
tarx = 2
// 触发之后 x 方向的缩放速度
xsp = 0.04
// 触发之后 y 方向的目标缩放量
tary = 2
// 触发之后 y 方向的缩放速度
ysp = 0.04
// 缩放中心位置
origin = 5
```

其中，origin 的值为 1 - 9，分别对应精灵的左上角，中上，右上角......见下：

```
1 2 3
4 5 6
7 8 9
```

对于这几个参数的额外说明：

假设我们需要将某刺在 1 秒内缩放到原来的 3 倍大小，那么 tarx，tary 的值就为 3；

* 对于缩放时间方式，time = 50；

* 对于缩放速度方式，xsp 与 ysp 的值均为：(3 – 1) / 50 = 0.04。

#### trgRotate

旋转刺。在触发之后会相对于某一点旋转一定的读数。

Creation Code 参数：

```gml
// 使用的精灵
spr = sprSpikeUp
// 触发器编号
trg = 1
// 旋转中心离 spr 原点的横向距离
cx = 16
// 旋转中心离 spr 原点的纵向距离
cy = 16
// 旋转总度数// 旋转到目标度数所需要的时间（帧）
angle = 90

time = 50
```

#### trgPathBlock

路径砖。触发后会按照指定路径移动，如果 player 触碰到在移动中的 pathFreeBlock 则会判断死亡。

Creation Code 参数：

```gml
// 使用的精灵
spr = sprBlock
// 触发器编号
trg = 1
// 路径名称
pth = pD1
// 运动速度
spd = 7
// 路径结束事件（0：停止运动；1：从头开始；2：从当前位置继续运动；3：反转路径）
enda = 0
// 路径缩放倍数（默认为 1，例如将 pU1 放大两倍则为向上移动两格）
scl = 1
move = true // 是否防止剧透（如果为 true，当玩家死亡之后砖会沿着当前方向移动，不会停止/转弯）
```

#### trgBlockFake

触发式假砖。未被触发时与砖块无异，但触发之后会变成假砖。

Creation Code 参数：

```gml
sprite_index = sprBlock // 使用的精灵
trg = 1 // 触发器编号
```

#### trgBlockInvisible

触发式隐形砖。未被触发时与空气无异，但触发之后会变成隐形砖。

Creation Code 参数：

```gml
sprite_index = sprBlock // 使用的精灵
trg = 1 // 触发器编号
```

### Gimmicks 功能

这个文件夹中包含颠倒重力、水、藤蔓、板子等 obj。

#### objGravUp

颠倒重力。视角会随之旋转。

#### objGravDown

返回正常重力。视角会随之还原。

#### objWater

普通水。跳跃高度为二段跳高度，出水无二段。

#### objWater2

二段水。跳跃高度为二段跳高度，出水有二段。

#### movingPlatform

普通木板。两种使用方式：直接运动与触碰运动（player 碰到板子的时候才会动）。

普通模式，Creation Code 参数：

```gml
hspeed = 3 // 横向速度
vspeed = 3 // 纵向速度
```

触碰模式，Creation Code 参数：

```gml
touch = true;
h = 3 // 触碰后的横向速度
v = 3 // 触碰后的纵向速度
```

#### pathPlatform

沿路径运动的木板。

两种使用方式：直接运动与触碰运动（player 碰到板子的时候才会动）。

如果需要使用防剧透功能，Creation Code 中补充：move = true;

普通模式，Creation Code 中直接添加代码：

```gml
path_start(pth, spd, enda, 0);
```

其中：

* pth 为路径名称
* spd 为运动速度
* enda 为路径结束事件（0：停止运动；1：从头开始；2：从当前位置继续运动；3：反转路径）

触碰模式，Creation Code 参数：

```gml
touch = true;
pth = pU1 // 路径名称
spd = 2.0001 // 运动速度
enda = 0 // 路径结束事件（0：停止运动；1：从头开始；2：从当前位置继续运动；3：反转路径）。
```

!> 注意，当 spd 取值为 2 并且沿竖直方向运动时，会有奇怪的 bug。将速度设为 2.0001 即可解决。

#### roundingCherry

生成一个苹果圈。该 obj 需放在苹果圈的圆心处。

Creation Code 参数：

```gml
num = 15 // 苹果总数
rad = 100 // 苹果圈半径
ang = 0 // 初始角度（改变这个值可以改变各个苹果在圆上的刷新位置，0~360）
spd = 0.72 // 绕圈速度（度/步，如果需要在 10 秒内转一周，那么 spd = 360/(10*50) = 0.72）
spr = sprCherry // 苹果的精灵（可选，默认情况下为普通红色苹果）
```

#### pathSpike

生成一系列均匀分布的按照某个 path 运动刺。path **必须封闭**，该 obj 需放在 path 的起始点。

Creation Code 参数：

```gml
num = 5 // 刺总数（默认为 1，如果用这个 obj 来制作伸缩刺可以省略这个参数）
pth = p9_1 // 运动路径
off = 0 // 初始位置（改变这个值可以改变各个刺在路径上的刷新位置，0~1）
spd = 2 // 各刺沿路径移动的速度
spr = sprSpikeUp // 刺的精灵（可选，默认情况下为朝上的普通刺）
```

### Host

该文件夹中的 `object` 仅对房主生效

### Guest

该文件夹中的 `object` 仅对非房主生效

### Saves 存档点

#### savePoint

存档点。一共有四种状态：

1.  红色：默认
2.  黄色：说明该存档点需要所有玩家共同射击才能生效。
3.  蓝色：说明其他玩家已存档（但是与你无关）
4.  绿色：存档成功

### Warps 传送点

这个文件夹中包含了各种 warp（传送点）

#### warp

普通 warp。

如果不需移动到某房间的指定位置而只是初始位置（playerStart） Creation Code 参数：

```gml
roomTo = rTraps // 传送到的房间名称
kind = 0 // 使用的房间转场效果
```

如果需要移动到指定房间的指定位置，Creation Code 中使用：

```gml
roomTo = rTraps // 传送到的房间名称
kind = 0 // 使用的房间转场效果
warpX = 400 // 指定传送的 x 坐标
warpY = 304 // 指定传送的 y 坐标
```

> 关于房间转场效果，可以参考[转场效果](transition.md)

#### invisibleWarp

隐形 warp。在房间边缘需要传送到另一个房间时，请使用这个`obj`。

如果不需移动到某房间的指定位置而只是初始位置（`playerStart`所在坐标），Creation Code 参数：

```gml
roomTo = rTraps // 传送到的房间名称
kind = 0 // 使用的房间转场效果
```

需要移动到指定房间的指定位置，Creation Code 中使用：

```gml
roomTo = rTraps // 传送到的房间名称
kind = 0 // 使用的房间转场效果
warpX = 400 // 指定传送的 x 坐标
warpY = 304 // 指定传送的 y 坐标
screens = x/y 方向坐标偏移程度
```

> 关于房间转场效果，可以参考[转场效果](transition.md)

关于 screens 参数的说明：

假设我们处于 800\*1216 一个大房间 room1 中，并且处于房间右下角( 784, 1168 )的位置，在我们的右边有一个 warp，它会将我们传送到另一个 800\*608 房间 room2 的左下角 （16, 560） 。为了使 player 在房间之间传送得更自然，我们想让 player 的纵坐标在传送前后看上去没有发生改变。这时候，我们需要将 player 的纵坐标向上平移 1 个屏幕的距离（也就是 608），也就是这里的 screens = -1。经过反复测试，warp 的距离以距离房间边缘 12 像素最佳，例如在以上情况下，便可以在 warp 的 Creation Code 中写入：

```
roomTo = room2;
warpX = 12;
screens = -1;
```

当省略 `warpX`/`warpY` 中的某一个值时，表示所省略值代表的坐标不会直接改变，而是移动 screens 个屏幕的距离。

#### warpStart

用于选关界面的 warp。

Creation Code 中：

* dif 表示游戏难度（0 – Medium，1 – Hard , 2 – Very Hard , 3 - Impossible）
* difName 表示在 warp 上方需要绘制的文字。

#### bossWarp

拿到特定的 bossItem 才会出现的 warp，一般会在 boss 的摧毁事件中创建。例如，在 myBoss 的摧毁事件中：

```gml
a = instance_create(400, 416, bossWarp);
a.roomTo = room2;
```

#### warpText

能够绘制文字的普通 warp。

在普通 warp 的 Creation Code 的基础上，增加一行：

```gml
text = "文字";
```

这里的文字只能是英文或者数字，并不支持中文绘制。简单的中文绘制用图片/背景表示即可，如确实有绘制中文的需求，可以使用 [FoxWriting](https://www.noisyfox.io/fox-writing-gamemaker.html) 扩展。

#### warpCount

拿到特定数量的 bossItem 或 secretItem 才会开启的 warp。

在普通 warp 的 Creation Code 的基础上，还需增加：

```gml
countBoss = true // 是否统计 bossItem 数量（true 表示统计 bossItem 数量）
countItem = false // 是否统计 secretItem 数量（true 表示统计 secretItem 数量）
total = 8 // 指定数量
```

### Slopes 斜坡

!> 这个文件夹中的 object 暂时处于报废状态

### Items 道具

这个文件夹中包含了各种在游戏中能获得的道具以及相关 obj。

#### bossItem

boss 被击败时所创建的 item，player 拿到之后则会记录指定编号的 boss 已被击败。

这个 obj 经常用于 boss 的摧毁事件中。在创建的同时需指定精灵与 boss 编号。例如，在 myBoss 的 destroy 事件中写入：

```gml
a = instance_create(688,544,bossItem);
a.num = 1;
a.sprite_index = bossicon1;
```

这段代码在 myBoss 被摧毁之时，在 (688, 544) 创建一个精灵为 `bossicon1` 的 `bossItem`，当 `player` 拿到这个 `bossItem` 时，系统会记录编号为 `num` 的 boss 已被击败，也就是 `global.boss[1]=1`。

#### bossItemViewer

用于在房间中显示某 boss 是否被击败。Creation Code 参数：

```gml
sprite_index = 使用精灵
num = boss编号
```

#### bossBlock

当拿到对应 boss 的 item 的时候，会自动摧毁的 block Creation Code 参数：

```gml
sprite_index = 使用精灵
num = boss编号
```

#### secretItem

隐藏道具。

Creation Code 参数：

```gml
sprite_index = itemicon1 // 使用精灵
num = 1 // 隐藏道具编号
```

#### secretItemViewer

用于在房间中显示某隐藏道具是否已获取。Creation Code 参数：

```gml
sprite_index = itemicon1 // 使用精灵
num = 1 // 隐藏道具编号
```

### Room 房间杂物

### Visual 视觉效果

这个文件夹中包含了一些常见的游戏效果。

#### objHPBar

用来绘制 boss 血条。这仅仅是一个如何使用 `drawLife` 脚本的范例

#### objShake

通过脚本 `screenShake` 调用，请参考脚本 `screenShake`。

#### objScreenFlash

通过脚本 `screenFlash` 调用，请参考脚本 `screenFlash`。

#### objShadow

通过脚本 `createShadow` 调用，请参考脚本 `createShadow`。

#### objSmoothView

用于在视野跟随的房间中使用更平滑的视野。使用了@波导 Lucario 的代码。

使用方法：将这个 obj 放到房间中的任意位置，然后到房间的 views （视野） 选项栏的 Object following（视野跟随）中，选择 objSmoothView，并将 Hbor 设置为 400，Vbor 设置为 304。Hsp 与 Vsp 可以不设置。

### Parent 父对象

这个文件夹中包含了 `platform`、`playerKiller`、`roomChanger` 这几个父对象。

### Bosses

#### miku

这个文件夹中包含了与 miku 耐久有关的各种 obj。

> 引擎重置了耐久的时间轴。原版 yuuutu 引擎的自带耐久中有四个时间轴，总共几百个时间轴事件；在本引擎中，仅有 1 个时间轴与 16 个时间轴事件，相信这比原来的会更容易看懂。

如果想学习如何制作耐久，可以先参考一下[耐久制作基础教程](avoidance.md)。

这个文件夹中包含了两个范例 boss（强化版的 boss 有二形态），objBossBullet 是 boss 中发射的弹幕 obj。这个 boss 与之前的教程中的 boss 范例差不多，只是放出一些攻击方式的代码供大家参考，仅供学习交流用，还请不要将这些傻蛋攻击方式仅仅是直接抄到你自己的高端大气的 boss 战中(´・ω・｀)

### System 系统

这个文件夹中包含了 `player` 以及有关游戏系统的 obj。这里介绍本引擎与 yuuutu 引擎中不同的地方。

#### world

* 计时方式为精确到毫秒
* 在 draw 事件中可以修改暂停界面。其中 pauseback 为暂停前游戏画面的截图

!> gm8.1 中生成截图的函数 `background_create_from_screen`有一定概率会出现 bug。

#### player

!> 移除原有变量：frozen, djump

新增：

* `global.reverse`: 设置为 true 时，颠倒重力
* `global.frozen`: 设置为 true 时，玩家无法操作 kid
* `global.frozen2`: 设置为 true 时，kid 无法移动（上下左右均不可）
* `infJump`: 设置为 true 时，kid 可以无限跳
* `jump[i]`: kid 第 i 段跳跃的速度
* `maxJumps`: 最大跳跃次数（3 或者 3 以上时，需额外指定跳跃高度）
* `curJumps`: 当前处于的跳跃编号
* `grav`: 重力大小

有关 player 的脚本：

* `playerMove` 控制 player 左右移动的脚本
* `playerWallJump` 控制 player 爬墙时动作的脚本
* `playerJump` 控制 player 跳跃的脚本
* `playerShoot` 控制 player 射击的脚本
* `playerSlope` 控制 player 在斜面上移动的脚本
* `playerReverse` 控制 player 翻转重力的脚本
* `playerMisc` 控制 player 的杂项脚本，包括死亡判定、调试功能等新增功能（仅在调试模式（F6）中有效）：
  * 使用鼠标左键同屏传送(´・ω・｀)
  * 使用 S 键即时存档(´・ω・｀)
  * 使用 G 键开启上帝模式(´・ω・｀)

#### bloodEmitter

更换为粒子效果，减少了死亡之后的 obj 数量

#### titleButton

增加了轻量化模式下，直接读取 SaveData1 的功能。

#### menuSelect / menuSelect2

均用于在 `rMenu` 中绘制死亡次数、时间、boss 图标等。

* menuSelect 为跳刺选难度，menuSelect2 为直接选难度
* 在 create 中可以指定各个 boss 图标

通过在 draw 事件中简单的改动，也可以绘制隐藏道具的图标。

首先，我们在 create 中利用脚本 `loadIcons` 获取了用于 draw 事件的存档信息：

```
  menu_difficulty[i]: 第 i 个存档的难度
  menu_clear[i]: 第 i 个存档是否通关
  menu_boss[i,j]: 第 i 个存档的第 j 个 boss 是否被击败
  menu_item[i,j]: 第 i 个存档的第 j 个 item 是否被拿到
```

只用在 `Draw` 事件中根据 `menu_item[i, j]` 来判断图标并绘制即可
