# 联机简介

为了自定义游戏中的联机效果，我们首先需要对联机游戏的运行机制有一个基本的概念。

# 服务器

服务器是客户端与客户端之间沟通的媒介，离开了服务器的支持，利用果引擎制作出的游戏只能单机运行。果引擎配套的服务器端代码 [iw-nikaple-server](https://github.com/Nikaple/iw-nikaple-server) 使用 [Node.js](https://nodejs.org) 编写，基于 [Patchwire](https://www.npmjs.com/package/patchwire) 魔改而来，在没有特殊需求的情况下，一般不需要修改。

果引擎为开发者提供了一个默认的 IP 地址（139.\*.\*.59，请在引擎的`ns_init`脚本中查看），仅供测试使用。在公开发布游戏时最好将 IP 地址改为你自己服务器的 IP，以增加游戏服务器的稳定性。

# 客户端

客户端的基础引擎部分基于 [I wanna be the Engine Yuuutu Edition](https://www.delicious-fruit.com/ratings/game_details.php?id=10483)（~~其实已经差不多全部重写了~~），网络通讯部分为高度定制化的 Patchwire 配套 [GM:S 引擎](https://github.com/gm-core/patchwire-gm)，使用的 Dll 插件包括：

* [Http Dll 2.3](http://www.maartenbaert.be/game-maker-dlls/http-dll-2/) 用于网络通信
* [Super Sound System](http://gmc.yoyogames.com/index.php?showtopic=120034) 用于音乐播放
* [FoxWriting](https://www.noisyfox.io/fox-writing-gamemaker.html) 用于多语言支持
* [CleanMem](http://gmc.yoyogames.com/index.php?showtopic=438215) 用于释放多余内存

# 通讯协议

服务器与客户端的通信协议主要分为两种，TCP 以及 UDP，它们的特点如下：

* TCP：稳定，但相对来说效率较低
* UDP：不稳定，丢包率相对较大，但效率高

基于以上特性，我们需要对不同数据选择不同协议来进行传输：

* 用户登录，创建房间，射击存档，重置游戏等功能，由于其数据量较小（一般只发送一次数据即可），为了保证其稳定性使用 TCP 协议传输。
* 玩家位置同步，可推动的箱子的位置同步等功能，由于数据量大（几乎每帧都会传送数据），但对稳定性要求不高（后面的数据会自然覆盖前面的，所以就算丢包也会很快恢复正常），使用 UDP 协议传输。

# 使用 TCP 协议传输数据

在引擎中，一共有三种预设的 TCP 传输模式，可以满足大部分的需求。它们分别是：

* [Instance 实例模式](/network?id=instance-实例模式)，用于同步静态放置在房间中，具有相同 `id` 的实例。

* [Event 事件模式](/network?id=event-事件模式)，用于同步任意时间点，在任意实例中的任意信息。

* [Wait 等待模式](/network?id=wait-等待模式)，用于同步一些需要所有客户端同时触发才能进行的事件。

  ?> 注意，由于引擎的限制，同步脚本 `ns_send_*` 只能写在 **除 Create, Begin Step, End Step, Draw 以外** 其他的事件中。如果实在需要在这些事件中调用同步脚本，请在需要同步的地方设定 alarm[i] = 1，并在 Alarm i （i = 0 ~11）事件中发送同步请求。

在这三种模式中，均可通过在同步信息（键值对）中指定 `scope` 参数来控制消息接收者的范围。

`scope` 的值可以是：

* `SCOPE_DEFAULT` 默认范围，发送给同房间的其他玩家（不填就是它）
* `SCOPE_OTHERS` 发送给其他玩家（无论在不在同一房间）
* `SCOPE_ALL` 发送给所有人（包括你自己）

例如：

```gml
// 向所有其他玩家均发送一个 `hello` 事件，包含一个熟悉的名字
ns_send_event(
    'hello', 1,
    'name', 'crazy_tiger',
    'scope', SCOPE_OTHERS
)
```

## Instance 实例模式

该模式使用脚本 `ns_send_instance` 声明，用于同步具有相同 `id` 的 `object` 。

脚本接收任意个数的参数，但需满足以下条件：

* 第一个参数为需要同步信息（键值对）的数量 n；
* 紧接着的 2n 个参数为形如 key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub> 的键值对，代表需要同步的信息。

注意，该脚本只能用于同步直接摆放在房间内，固定 `id` 的 `object` 。（使用 `instance_create` 创建的 `object` 无效，会报错）

?> 当不需要同步任何数据时，可以不填参数。

下面以 `blockMove` 为例，具体说明 Instance 实例模式的应用。

当 `player` 站上 `blockMove` 时，`blockMove` 会朝着设定好的方向开始运动。其中，横向速度为 `h` ，纵向速度为 `v` 。因此，在判定到 `player` 站上的那一瞬间，我们需要将砖块的状态同步到其他客户端上。

`Create Event`:

```gml
// 设置数据同步状态为未同步
sent = false
```

`Step Event`:

```gml
// 检测玩家是否站上了砖块，略
isPlayerOnBlock = ...
// 仅当玩家站在砖块上并且同步状态为未同步时才发送数据，
// 如果不使用 sent 变量，则每帧都会发送数据，造成较大网络开销
if (isPlayerOnBlock && !sent) {
    // 设置横向速度
    hspeed = h
    // 设置纵向速度
    vspeed = v
    // 同步 2 个属性，
    // 第一个属性名为'h'，值为当前横向速度，
    // 第二个属性名为'v'，值为当前纵向速度
    ns_send_instance(
        2,
        'h', hspeed,
        'v', vspeed
    )
    // 设置数据同步状态为已同步
    sent = true
}
```

随后，该信息会被直接同步到其他客户端的 `Other -> User defined -> User 15` 事件中。我们只需在其中处理得到的数据即可：

`User Defined 15`:

```gml
// 此时，h, v 已被分别设置为需要同步的横向与纵向速度，
// 我们需要利用它们对当前实例进行处理。
hspeed = h
vspeed = v
```

这样便完成了该实例的速度在不同客户端中的同步，这种模式也是应用得最广的一种模式。

## Event 事件模式

该模式使用脚本 `ns_send_event` 声明，用于在任意时间点，任意 `object` 中同步任意信息。

脚本接收任意个数的参数，但需满足以下条件：

* 第一个参数为事件的名称（后面会用到）；
* 第二个参数为该事件中需要同步信息（键值对）的数量 n；
* 紧接着的 2n 个参数为形如 key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub> 的键值对，代表需要同步的信息。

以 `savePointSync` 为例，当某个客户端的 `player` 利用该存档保存之后，其他所有玩家均可以通过重置游戏（也就是按 R ）来移动到该存档前。由于存档时玩家可能在不同房间，因此不适合使用 Instance 方式来进行同步。

`Step Event`:

```gml
// 检测是否存档成功，略
isSaveSuccess = ...
if (isSaveSuccess) {
     // 同步三个属性，
     // 第一个属性名为'id'，值为当前存档点的 `id`，
     // 第二个属性名为'x'，值为 player 在上一帧的 x 坐标（xprevious），
     // 第二个属性名为'y'，值为 player 在上一帧的 y 坐标（yprevious），
     // 在这里使用上一帧的坐标是为了防止出现卡墙 bug。
    ns_send_event(
        'save_sync', 3,
        'id', id,
        'x', player.xprevious
        'y', player.yprevious
    )
}
```

随后，该信息会被直接同步到其他客户端的 `handler_event_{NAME}` 脚本中，这里的 `{NAME}` 就是我们刚才发送的事件名。

因此，我们新建一个脚本，命名为 `handler_event_save_sync` ，即可开始接收从其他客户端发送来的 `save_sync` 事件。

该类脚本均接收两个参数：第一个参数为发送该事件的玩家名，第二个参数是一个 `ds_map`，存放着所有同步的数据：

```gml
// handler_event_save_sync(fromName, data)

// 所有使用到的变量必须用 var 声明，否则可能产生不可预测的错误！
var fromName, data, _id, _x, _y;
fromName = argument0
data = argument1
// json_pick 与 ds_map_find_value 完全一致，只是短一点，更好写
// 从 data 中提取（pick）名为 'id' 的数据
_id = json_pick(data, 'id')
// 从 data 中提取（pick）名为 'x' 的数据
_x = json_pick(data, 'x')
// 从 data 中提取（pick）名为 'y' 的数据
_y = json_pick(data, 'y')
// 现在 _id,  _x, _y 中就存放了其他客户端同步过来的的 'id', 'x', 'y'，
// 用这些数据去实现存档同步就可以啦。

// 获取完数据之后不需要对 data 进行任何处理，引擎会自动释放它所占据的内存空间。
```

这样便完成了在任意时间点、任意 `object` 中，对于任意数据的同步。在 `ns_send_instance` 实现不了需求的时候可以考虑考虑这个～

## Wait 等待模式

该模式使用脚本 `ns_send_wait` 声明，用于那些在所有玩家都触发某事件后额外发生的事件（例如，所有玩家进入后才会传送的 `warp` 等）。

在使用该事件时，需要传入一个标记信息（默认为当前实例的 `id`）。

?> 如果你有多个 `warp` 但传送至同一个房间，即可将标记信息设置为需要传送的房间编号（`roomTo`），这样以来服务器就会根据该标记信息来对各个客户端进行标记。

该脚本接收任意个数的参数，满足以下条件：

* 第一个参数为等待事件的名称（后面会用到）；
* 第二个参数为该事件的标记信息；
* 第三个参数为该等待事件中需要同步信息（键值对）的数量 n；
* 紧接着的 2n 个参数为形如 key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub> 的键值对。

如果返回数据中的 `fin` 项为 1，即说明所有客户端均已触发该事件。

以 `reset` 等待事件为例，该等待事件用于设置当前房间的属性为“当且仅当所有玩家选择重置时，该房间才会重置”。
Step Event:

```gml
// 判断当前房间是否需要等待重置
shouldResetWait = ...
if (shouldResetWait) {
    // 发送名为 `reset` 的等待事件
    ns_send_wait('reset', room)
}
```

随后，该信息会被直接同步到其他客户端的 `handler_wait_{NAME}` 脚本中，这里的 `{NAME}` 就是我们刚才发送的等待事件名。

因此，我们新建一个脚本，命名为 `handler_wait_reset` 即可开始接收从其他客户端发送来的 `reset` 等待事件。

该类脚本均接收三个参数：

* 第一个参数为发送该事件的玩家名；
* 第二个参数是一个 `ds_map`，存放着所有同步的数据；
* 第三个参数代表着是否所有客户端均已触发该事件

```gml
// handler_wait_reset(fromName, data, isFinished)

// 所有使用到的变量必须用 var 声明，否则可能产生不可预测的错误！
var fromName, data, isFinished;
fromName = argument0
data = argument1
isFinished = argument2

if (isFinished) {
    // 处理重置成功事件，重置当前游戏
} else {
    // 处理重置失败事件，或许给当前玩家一些提示？
}
```

# 使用 UDP 协议传输数据

## 你可能并不需要 UDP 模式

使用 UDP 协议同步数据对于网络的开销是相当大的，请慎重使用，并且在有可能不用的地方尽可能不用。

例如，`blockMove` 的运动状态在 `player` 站上的一瞬间即可确定，所以只需要利用 TCP 同步一次即可，而不需要随时随地的同步位置信息。UDP 模式的应用场景主要是与 `player` 交互较多的 `object`，例如可推动砖（参考引擎中 `blockPush` 的 `User Defined 0` 以及 `User Defined 14`）。

另外，在使用该模式之前你需要对缓冲区 `buffer` 以及基本的数据类型有一些基本的了解。关于 `buffer` 读写函数以及数据类型的说明可以参考 `Http Dll 2.3` 的[文档](http://www.maartenbaert.be/game-maker-dlls/http-dll-2/buffers/)。

## 使用 UDP 来同步

使用 UDP 模式进行同步的方式也很简单，下面以 `blockPush` 为例简单说明：

`Step Event`:

```gml
// 判断是否需要同步位置信息
shouldSyncPosition = ...
if (shouldSyncPosition) {
    // 开始进行 UDP 同步，该脚本会返回一段缓冲区供你写入
    buffer = ns_sync_begin()
    // 写入当前 x 坐标，类型为 int16（也就是 short, 范围：-32768~32767 的整数）
    buffer_write_int16(buffer, x)
    // 写入当前 y 坐标，类型为 int16（也就是 short, 范围：-32768~32767 的整数）
    buffer_write_int16(buffer, y)
    // 写入当前横向速度，类型为 int8（也就是 byte, 范围：-128~127 的整数）
    buffer_write_int8(buffer, hspeed * 10)
}
```

随后，经过服务器以及 `objClient` 的一系列处理，具有同样内容的 `buffer` 会被直接同步到其他客户端同一实例的 `Other -> User defined -> User 14` 事件中，我们只需要在该事件中读取 `buffer` 并处理即可。

`User Defined 14`:

```gml
// 在此事件发生之前，buffer 变量就被赋值为服务器传来的缓冲区了

// 读取需要同步的 x 坐标
x = buffer_read_int16(buffer)
// 读取需要同步的 y 坐标
y = buffer_read_int16(buffer)
// 读取需要同步的横向速度
hspeed = buffer_read_int8(buffer) / 10
```
