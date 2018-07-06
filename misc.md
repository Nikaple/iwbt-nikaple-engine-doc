# 其他新特性

## playerStart 参数

在 playerStart 中，可以直接设定自动存档、无限跳等参数了。参考：[playerStart](objectref?id=playerstart)

## 传送点变化

在新版中废弃了 warpX、warpY，并加入了新的传送特性。参考：[warp](objectref?id=warps-传送点)

## 存档点变化

在新版中可以通过 mode 设置存档点模式了，Creation Code 参数：

```gml
mode = SAVE_MODE_XXXXXX
```

可选值有：

- SAVE_MODE_SHOOT：射击存档（默认）
- SAVE_MODE_TOUCH：触碰存档
- SAVE_MODE_PRESS：按键存档，默认为 'S'。默认按键可到 `controls_init` 脚本中修改 `global.savebutton`。
