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
music_loop(BGM_1)
music_pause(BGM_1)
music_resume(BGM_1)
```

## 房间音乐的设置方法

- 在 `music_init` 中，引擎会自动读取音乐文件夹（默认为 Data/Music）中的所有文件，并将其 id 储存至全局变量 `BGM_文件名` 中。例如：

  - `Death.ogg` 会被自动读取为 `BGM_Death`；
  - `faQ.ogg` 会被自动读取为 `BGM_faQ`；
  - `myMusic.ogg` 会被自动读取为 `BGM_myMusic`。

- 在 `music_config` 中，仿照示例增加代码播放音乐，例如：

  ```gml
  // add your code here
  case myRoom:
      music_play(BGM_myMusic);
      break;
  ...
  ```

  注意后面的 `break` 不可省略！

## BOSS 房间的 BGM 处理

在 BOSS 房间中，你可能想要自己控制 BGM 播放的时机。可以按照下面的方法设置：

1.  先找到脚本 `isBossRoom` ，并设定相关房间为 BOSS 房（参照脚本即可）。

2.  在你需要播放 BOSS 战音乐时，调用：

```gml
music_play(myMusic);
```

?> 在默认设置下，BOSS 房间中不可暂停。如果需要允许暂停，可以到 `setGlobalsMinor` 脚本中修改 `global.enable_pause_in_boss_room = true`
