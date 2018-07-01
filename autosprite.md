# 自动更换刺的精灵

在游戏中，你往往需要许多不同精灵的刺，而这是一项十分繁琐的工作。当要在房间中使用时，需要在不同的文件夹中去寻找不同精灵的刺，这更降低了创作的效率。

在果引擎中，你可以分别定义在各个房间中刺的样式，定义成功之后引擎则会自动替换 `spikeUp、spikeDown、spikeLeft、spikeRight、minispikeUp、minispikeDown、minispikeLeft、minispikeRight` 这八种普通刺的精灵。

该功能可以到脚本 `Scripts -> functions -> autoSpikeSprite` 中设置。

在 `autoSpikeSprite` 脚本的第 8 行，仿造示例添加脚本：

```gml
case myRoom:
    spikeSprite(mySpike, myMiniSpike, myImageSpeed);
    break;
```

* `mySpike` 为普通刺所使用的精灵，大小为`32 * 32`，刺的方向向上，精灵的原点需要在图像中心（参考 `sprSpikeM`）
* `myMiniSpike` 为小刺所使用的精灵，`16 * 16`，刺的方向向上，精灵的原点需要在图像中心（参考 `sprMiniSpikeM`），如果该项省略或为 0 时，会使用普通刺的精灵并缩小至原来的一半的方法来作为小刺的精灵。
* `myImageSpeed` 用于刺的精灵为动态时，可以指定所用刺的 `image_speed` 值。如果刺的精灵只有单帧可忽略不写。

设置完毕之后， 在各房间中的就可以使用 `spikeUp、spikeDown、spikeLeft、spikeRight、minispikeUp、minispikeDown、minispikeLeft、minispikeRight` 这八种普通刺来进行摆放与设计了，它们在指定的房间中会自动更换为脚本中所指定的精灵。

!> 当使用 Creation Code 来给刺添加 `path_start` 使其伸缩（或其他路径）的时候，会使得 path 并不能正常工作。 这时可以使用 [pathSpike](objectref?id=pathspike) 来代替。
