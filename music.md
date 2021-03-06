# 音乐播放

果引擎使用了 [Super Sound](http://gmc.yoyogames.com/index.php?showtopic=120034) 音乐系统，在它的支持下，你可以从外部读取声音文件，并且可以暂停与继续播放音乐（这是 GM 自带函数所做不到的）。

?> Super Sound 支持的音乐格式仅限 ogg 与 wav，推荐使用 ogg 格式（ wav 格式的音乐占用空间太大）。因此，在使用音乐前需要将其转换为 ogg 格式，这可以借助 [狸窝全能视频转换器](http://www.leawo.cn) 或 [在线转码网站](https://convertio.co/zh/) 来完成。

音乐播放主要涉及到两个脚本： `music_init` 与 `music_config` ，它们都在`Scripts -> audio`文件夹下。

- `music_init` 用来从外部文件夹中读取音乐至游戏中；
- `music_config` 会在各个房间刚开始时调用一次，决定各个房间中需要播放的音乐。

?> 音乐的存放位置可以通过 `setGlobalsMinor` 中的 `global.music_directory` 设置，默认为 `Data/Music`

## 升级到 2.0

在果引擎升级到 2.0 版之后，播放音乐的脚本名称更加统一了：

```gml
// 音乐与音效均可以使用 music_play 播放
music_play(sndBlockChange)
music_play(BGM_BOSS1)
// 音乐与音效均可以使用 music_stop 停止
music_stop(sndDeath)
music_stop(curMusic)
// 音乐还能够使用相关脚本循环、暂停、继续播放
music_loop(BGM_Stage1)
music_pause(BGM_Stage1)
music_resume(BGM_Stage1)
```

## 房间音乐的设置方法

以下两种方法任选其一，同时使用时分房间设置的 BGM 会覆盖集中设置的 BGM。在果引擎中， `/Data/Music` 目录下的所有音乐都会被默认自动加载，并将其 id 以全局变量名 `BGM_文件名` 储存。因此在制作游戏的过程中，最好不要使用 `BGM_` 开头的变量名，否则很可能发生冲突。音乐加载具体说明如下：

- `Death.ogg` 会被自动读取为 `BGM_Death`；
- `faQ.ogg` 会被自动读取为 `BGM_faQ`；
- `myMusic.ogg` 会被自动读取为 `BGM_myMusic`。

!> 注意，由于 GM 引擎限制，自动加载的音乐名称均只由 0-9, A-Z, a-z, 下划线"_" 构成，如果文件名中含有其他字符，需要手动调用 `music_load` 函数加载。

### 分房间设置（新手推荐）

在房间中放入 `objPlayMusic` （位于 rooms 文件夹下）并设置相关参数即可，如果你想将音乐文件夹中的 `faQ.ogg` 设置为当前房间的 BGM，则：

Creation Code 参数：

```gml
// 当前房间的 BGM
bgm = BGM_faQ // <- 在文件名前面加上 BGM_ 即可
```

!> 由于此处的 BGM_faQ 为全局变量，而不是 GM 中的资源名，所以在 GM 中呈现的是变量的颜色（黑色），这并不影响音乐文件的正常播放。

### 集中设置

- 在 `music_config` 中，仿照示例增加代码播放音乐，例如：

  ```gml
  // add your code here
  case myRoom:
      music_play(BGM_myMusic);
      break;
  // ...
  ```

  注意后面的 `break` 不可省略！

## 对音乐进行骚操作

如果你需要暂停、跳转播放、区域循环等高级功能，可以对需要使用高级功能的音乐使用非流模式加载。即：

```gml
globalvar BGM_myMusic;
BGM_myMusic = music_load('myMusic', 0)
```

之后，便可以使用 SS_SetSoundPosition 等函数对 BGM_myMusic 进行处理而不受缓冲区大小限制。

## BOSS 房间的 BGM 处理

在 BOSS 房间中，你可能想要自己控制 BGM 播放的时机。可以按照下面的方法设置：

1.  先找到脚本 `isBossRoom` ，并设定相关房间为 BOSS 房（参照脚本即可）。

2.  在你需要播放 BOSS 战音乐时，调用：

```gml
music_play(myMusic);
```

?> 如果需要在流式播放模式下将某首音乐设置为非流式播放，可以在 `music_init` 的 **最下方** 加上 `BGM_myMusic = music_load('myMusic', false)` （将 myMusic 更换为音乐文件的名称）即可。

?> 另外，在默认设置下，BOSS 房间中不可暂停。如果需要允许暂停，可以到 `setGlobalsMinor` 脚本中修改 `global.enable_pause_in_boss_room = true` 即可。
