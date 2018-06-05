# 存档功能

为了提高存档效率以及安全性，`果引擎 2.0 版` 对存档系统进行了重写。新版存档用回了二进制系统，但保持了很高的可读性。

存档系统涉及到四个脚本：

* `saveGame` 用于保存游戏
* `loadGame` 用于读取游戏
* `saveDeathTime` 用于只保存时间以及死亡次数
* `loadIcons` 用于在选择存档页面读取存档信息

## 储存自定义变量

在新版引擎中，支持 64 个自定义变量的储存，它们被定义为 `global.data[1] - global.data[64]`，你可以在利用这些数据直接储存你需要的变量。

?> 自定义变量的总数可以在 `setGlobalsMinor` 中设置。

## 储存 player 状态

在新版引擎中，`player` 的 `maxJumps`、`maxSpeed`、`grav` 均会被自动写入到存档，控制 `player` 的物理状态更方便了。

| 变量值           | 状态       |
| ---------------- | ---------- |
| maxJumps = 0     | 无法跳跃   |
| maxJumps = 1     | 只有一段跳 |
| maxJumps = 3     | 三段跳     |
| maxSpeed > 3     | 高速       |
| 0 < maxSpeed < 3 | 低速       |
| grav > 0.4       | 超重       |
| 0 < grav < 0.4   | 失重       |
