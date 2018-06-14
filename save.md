# 存档功能

为了提高存档效率以及安全性，果引擎 2.0 版对存档系统进行了重写。新版存档用回了二进制系统，但保持了很高的可读性。

存档系统涉及到四个脚本：

* `saveGame` 用于保存游戏
* `loadGame` 用于读取游戏
* `saveDeathTime` 用于只保存时间以及死亡次数
* `loadIcons` 用于在选择存档页面读取存档信息

## 储存自定义变量

在新版引擎中，支持 64 个自定义变量的储存，它们被定义为 `global.data[1] - global.data[64]`。你可以利用它们来保存游戏中的全局状态。

你可以灵活利用 `GM` 的 `Resources -> Define Constants...` 功能来定义常量，以达到更好的代码可读性。

假设你的游戏中有许多钻石，而你需要保存玩家当前拥有的钻石数量，你可以：

1.  定义常量 `SAVE_DIAMOND_AMOUNT` 为 1；
2.  每次玩家获得钻石时，执行 `global.data[SAVE_DIAMOND_AMOUNT] += 1`；
3.  在每次读档之后，钻石数量就能够以 `global.data[SAVE_DIAMOND_AMOUNT]` 的形式获取。

?> 自定义变量的总数可以在 `setGlobalsMinor` 中设置。

## 储存 player 状态

在新版引擎中，`player` 的 `maxJumps`、`maxSpeed`、`grav` 均会被自动写入到存档，控制 `player` 的物理状态更方便了。

| 变量值                 | 状态       |
| ---------------------- | ---------- |
| 0 < shootInterval < 10 | 开启连射   |
| maxJumps = 0           | 无法跳跃   |
| maxJumps = 1           | 只有一段跳 |
| maxJumps = 3           | 三段跳     |
| maxSpeed > 3           | 高速       |
| 0 < maxSpeed < 3       | 低速       |
| grav > 0.4             | 超重       |
| 0 < grav < 0.4         | 失重       |

## 安全性

在开启 `global.enable_encryption` 配置项时，果引擎会对游戏的存档文件进行加密。加密使用的密钥可以通过 `global.key` 来设置。

?> 为了更高的安全性，`global.key` 的长度不能低于 40。

!> 使用存档加密可以使修改游戏存档变得更加困难，但不能完全阻止该问题的发生。

## 自定义储存脚本

在特殊的需求下，你可能需要增加自定义的储存变量。这可以通过以下方法修改：

1.  在 `saveGame` 中，找到下面的注释，在注释下方增加自定义变量并保存；

```gml
// for more save data, add script here
// If you don't know which buffer_write_* script to use,
// use buffer_write_float32
buffer_write_float32(buffer, global.myVar1)
buffer_write_float32(buffer, global.myVar2)
```

2.  在 `loadGame` 中，找到下面的注释，在注释下方增加自定义变量并读取。

```gml
// for more save data, add script here
// If you don't know which buffer_read_* script to use,
// use buffer_read_float32
global.myVar1 = buffer_read_float32(buffer)
global.myVar2 = buffer_read_float32(buffer)
```

注意，变量储存和读取的数据必须一致，否则存档系统会出现 BUG。

!> 在修改存档脚本之后必须 **开始新游戏** 而不能读档！
