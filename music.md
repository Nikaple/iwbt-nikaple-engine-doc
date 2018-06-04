# 音乐播放

果引擎使用了 [Super Sound](http://gmc.yoyogames.com/index.php?showtopic=120034) 音乐系统，在它的支持下，我们可以从外部读取声音文件，并且可以暂停与继续播放音乐（这是 GM 自带函数所做不到的）。

?> Super Sound 支持的音乐格式仅限 ogg 与 wav，推荐使用 ogg 格式（ wav 格式的音乐占用空间太大）。因此，在使用音乐前需要将其转换为 ogg 格式，这可以借助 [狸窝全能视频转换器](http://www.leawo.cn) 或 [在线转码网站](https://convertio.co/zh/) 来完成。

音乐播放主要涉及到两个脚本： `music_init` 与 `music_config` ，它们都在`Scripts -> audio`文件夹下。

* `music_init` 用来从外部文件夹中读取音乐至游戏中；
* `music_config` 会在各个房间刚开始时调用一次，决定各个房间中需要播放的音乐。

?> 音乐的存放位置可以通过 `setGlobalsMinor` 中的 `global.music_directory` 设置，默认为 `Data/Music`

?> 现在可以通过同一的脚本 `music_play` 来播放音乐和音效啦！

## 房间音乐的设置方法

* 在 `music_init` 中，仿照示例增加代码加载音乐，例如：
  ```gml
  // add your code here
  globalvar myMusic;
  myMusic = music_load("b6.ogg");
  ```
  这个变量 `myMusic` 就存入了刚载入的音乐文件 `b6.ogg`，在后面的播放脚本中用到。
* 在 `music_config` 中，仿照示例增加代码播放音乐，例如：

  ```gml
  // add your code here
  case myRoom:
      music_play(myMusic);
      break;
  ...
  ```

  注意后面的 `break` 不可省略！

另外，在 boss 房间中，在进入房间的同时可能不需要播放音乐。为了达到这个效果，请先到 `Scripts -> system` 中的脚本 `isBossRoom` 中设定该房间为 boss 房（参照脚本即可） 。

设置成功之后，在 boss 房中系统默认不会播放音乐，并且当玩家暂停游戏时，音乐会同时暂停而不是仅仅减小音量。在某个时间点，如果需要播放 boss 战音乐，可使用：

```gml
music_play(myMusic);
```

## 其他常用音乐相关函数

### music_play(music_or_sound)

用于播放外置音乐，或游戏音效

### music_stop(music_or_sound)

停止外置音乐，或游戏音效

### music_loop(music)

循环播放外置音乐

### music_pause(music)

暂停外置音乐

### music_resume(music)

继续播放外置音乐
