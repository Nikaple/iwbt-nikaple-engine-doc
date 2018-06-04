# 调试功能

在果引擎中内置了许多调试功能，只需按 F6 以调试模式编译游戏即可启动。

## 调试中可见

在调试模式中，我们可以看见几乎地图中的所有 `object`。包括砖块、触发器等。如果你也需要使自己的 `object` 在调试模式下可见，可以在 `Create Event` 中写入：

`Create Event`：

```gml
if (debug_mode) {
    visible = true
}
```

## Player

`player` 在调试模式下也有一些新的特性，例如：

* 可以使用 `鼠标左键` 传送到房间任意地点
* 可以使用 `G 键` 开关无敌模式
* 可以使用 `S 键` 随时存档

## 快速登录

在脚本 `setGlobals` 中，设定了两组快速登录的用户名与密码：

```gml
global.debug_host_name = 'username'
global.debug_host_pass = 'password'
global.debug_guest_name = 'test'
global.debug_guest_pass = 'test'
```

你可以注册两组在`调试模式`中，有着以下功能：

* 按下 `Shift` 可以使用 `global.debug_host_name` 登录，使用 1 号存档
* 按下 `Ctrl` 可以使用 `global.debug_guest_name` 登录，使用 2 号存档
* 按下 `空格` 可以直接跳过登录，开始游戏

## objDebug

`objDebug` 是果引擎自带的控制台，它只在调试模式下生效。它用于在屏幕上直接输出一切非 0、'0'的变量值。启动方法：

* 在 F6 进入游戏后，按下 `End` 键。
* 按下 `Delete` 键可以切换到详细模式，在该模式下 `objDebug` 会列出它发出或收到的所有网络请求。

```gml
// debug 函数会自动在参数间添加空格
debug('I', 'Wanna', 'be', 'the', 'Guy!') // I Wanna be the Guy!
// 可能为零的参数只能通过字符串拼接来显示
debug('This is a zero: ' + string(0)) // This is a zero: 0
```
