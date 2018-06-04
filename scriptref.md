# Script 文档

## Functions

#### drawSelf

在 draw 事件中使用，用于绘制 obj 自身。 **当一个 obj 拥有 draw 事件时，它的精灵则不会自动绘制在屏幕上，这时就需要使用 drawSelf 函数来绘制该 obj 的原始精灵**。

例如在 `warp` (`roomChanger`) 中，需要同时绘制 `warp` 的精灵与 `warp` 上方的文字，所以 `draw_text` 绘制文字的同时我们还需要调用 `drawSelf` 来绘制 `warp` 的精灵。

```gml
//draw the original sprite
drawSelf();
//draw the text
if (is_string(text)) {
    i18n_draw_set_font(fontMsyh12);
    i18n_draw_set_align(fa_center, fa_bottom)
    i18n_draw_text_ext_color(x + 16, y - 8, text, 8, -1, color, color, alpha);
}
```

#### drawLife(x1, y1, x2, y2, curVal, maxVal, col1, col2, outline)

在 draw 事件中使用，用于绘制血条。

* (x1,y1), (x2,y2)：血条左上角与右下角的坐标
* curVal：表示当前血量的变量
* maxVal：最大血量
* col1：满血时血条的颜色
* col2：空血时血条的颜色
* outline：是否绘制边框

（参考示例 obj：objHPBar）

#### fadeIn(time)

在 step 事件中使用，实现 obj 的淡入效果。

* time： obj 淡入所经过的时间（帧），默认为 10（1 帧 = 0.02 秒）。

?> 在使用这个脚本之前，务必先把当前 obj 的不透明度 image_alpha 设置为 0。

#### fadeOut(time)

在 step 事件中使用，实现 obj 的淡出效果。

* time：obj 淡出所经过的时间（帧），默认为 10（1 帧 = 0.02 秒） 。

?> 如果不透明度降低到 0 以下，则会摧毁当前 obj。

#### flashObject(flash_time, flash_count)

使当前 obj 进入闪烁，并将变量“flash”设置为 `true`。

当闪烁结束后，flash 变量会自动回到 0，这在设置 boss 被子弹击中事件的时候十分有用。

* flash_time：闪烁一次所需要的时间；
* flash_count: 总共闪烁次数。

#### splitObject(number, speed, object, direction, sprite)

生成一圈相同的 `obj` 向外发散。

* number：生成 `obj` 的总数；
* speed：生成 `obj` 的速度；
* object：生成 `obj` 的名字；
* direction：第一个 `obj` 瞄准的方向；
* sprite：生成 `obj` 的精灵名称（可选） 。

其中，如果将 direction 设置为-1，生成 obj 的方向将是随机的；如果将 direction 设置为 1，生成 obj 的方向将瞄准 player；如果将 direction 设置为其他值，则会瞄准所指定的方向

?> GM 中的方向：向右为 0，向上为 90，逆时针为正

#### autoSpikeSprite, spikeSprite

参见 [自动更换刺的精灵](autosprite.md)

#### screenShake(time, shakeX, shakeY)

产生一个震屏效果。

* time：震屏效果的持续时间（帧）；
* shakeX：横向震动的振幅；
* shakeY：纵向震动的振幅。

#### screenFlash(time)

产生一个屏幕闪白效果。

* time：闪白效果的持续时间（帧）。

#### createShadow(alpha_speed, scale_speed)

产生拖影效果， 常用于 alarm 事件并重复调用。

* alpha_speed：每步影子不透明度的减小量；
* scale_speed：每步影子大小的减小量。

例如：`objBossBullet` 的 `Alarm 0` 事件：

```gml
createShadow(0.1, 0);
alarm[0] = 2;
```

#### setScale(xscale,yscale)

设置 obj 在 x、y 方向上的拉伸量。在设置触发砖（trigger）区域的时候会经常用到。

* xscale：x 方向拉伸量
* yscale: y 方向拉伸量

## System

### Player

#### killPlayer

在任意时刻直接调用，可以让玩家立刻去世。

#### playerInit

对 `player` 的参数进行初始化。

* infJump：是否可以无限跳
* jump[1]：一段跳速度
* jump[2]：二段跳速度
* maxJumps：跳跃总数
* maxSpeed：横向速度
* grav：重力
* maxAirSpeed：最大下落速度
* maxWaterSpeed：水中最大下落速度

#### playerSprite

设置 `player` 各个状态的精灵。

#### playerCheckKeyboard

判断键盘事件

#### playerMove

`player` 移动脚本

#### playerJump, playerVJump

`player` 跳跃脚本

#### playerWallJump

## Music

## Network

## Draw

## Lib

### audio

* audio_init()

初始化 ini 配置文件，只需在游戏开始时调用一次即可，无需修改。

* audio_update()

更新音乐配置，当改变音乐设置之后调用。

* audio_setsoundvolume (add_volume)

增加/降低音效音量。audio_setsoundvolume(1) 则会将音效的音量提升 1 点。

* audio_setmusicvolume (add_volume)

增加/降低音乐音量。audio_setmusicvolume(-1) 则会将音乐的音量降低 1 点。

* audio_togglesoundmuted()

切换音效静音/非静音。

* audio_togglemusicmuted()

切换音乐静音/非静音。

* audio_playsound(sound)

用于播放音效（GM 中的 Sound 文件夹中的声音变量），这个脚本解决了 win8 的兼容性问题，所以播放音效请用这个脚本而不是直接 sound_play。由于使用了全局音量，所以声音文件的音量不能直接在 GM 中调整， 而需要在脚本前面给予一个值来调整默认音量。（按照范例来修正你自己的音效即可）

* audio_playmusic(music)

播放外置音乐（参见第三节）

* audio_loopmusic(music)

循环播放外置音乐（参见第三节）

* audio_pausemusic(music)

暂停外置音乐

* audio_resumemusic(music)

当音乐暂停时，继续播放音乐。

### i18n

* i18n_init
* i18n_font_init
* i18n_font_load
* i18n_font_add
* i18n_add
* i18n_get
* i18n_set_lang
* i18n_get_lang
* i18n_show
* i18n_free

### i18n/draw

* i18n_draw_auto_encoding

  该脚本在 `effect_parent` 中调用，用于设置各种语言的编码

* i18n_draw_set_alpha
* i18n_draw_set_color
* i18n_draw_set_font
* i18n_draw_set_align
* i18n_draw_set_halign
* i18n_draw_set_valign
* i18n_draw_text
* i18n_draw_text_ext
* i18n_draw_text_transformed
* i18n_draw_text_ext_transformed
* i18n_draw_text_color
* i18n_draw_text_ext_color
* i18n_draw_text_transformed_color
* i18n_draw_text_ext_transformed_color
* i18n_string_width
* i18n_string_height
* i18n_string_width_ext
* i18n_string_height_ext

### i18n/message

* i18n_show_message
* i18n_show_message_ext
* i18n_get_integer
* i18n_get_string

### json

* json_init
* json_decode
* json_destroy
* json_free
* json_pick
* json_get
* json_log

### cmd

* cmd_init
* cmd_destroy
* cmd_log
* cmd_add
* cmd_add_list
* cmd_add_map
* cmd_list_add
* cmd_list_add_list
* cmd_list_add_map

## Plugins

### Http Dll 2.3

* [Http Dll 2.3 帮助文档](http://www.maartenbaert.be/game-maker-dlls/http-dll-2/)

### FoxWriting

* [FoxWriting 帮助文档](http://docs.magecorn.com/doc-view-54.shtml)

### CleanMem

这个也需要文档吗？

### Super Sound System

#### 常用

* SS_Init()

  初始化，必须在游戏开始时调用。

* SS_LoadSound(fname, stream)

  该函数返回一个其他函数均要用到的音乐 `id`。

  * fname：文件名
  * stream：设置为 0，则一次性将音乐加载至内存；设置为 1，则会分段加载

* SS_PlaySound(id)

  播放音乐。`id` 来自 `SS_LoadSound`

* SS_LoopSound(id)

  循环播放音乐。`id` 来自 `SS_LoadSound`

* SS_StopSound(id)

  停止播放音乐。`id` 来自 `SS_LoadSound`

* SS_FreeSound(id)

  释放音乐所占的内存空间。`id` 来自 `SS_LoadSound`

* SS_PauseSound(id)

  暂停播放音乐。`id` 来自 `SS_LoadSound`

* SS_ResumeSound(id)

  继续播放音乐。如果该音乐被暂停，则会继续播放；否则重头开始播放。如果成功则返回 1，否则返回 0。`id` 来自 `SS_LoadSound`

* SS_Unload(id)

  必须在游戏结束时调用。

#### SS_Set 系列函数

SS_Set 系列函数可以让你设定声音的参数

* SS_SetSoundVol(id,vol)

  设置音乐音量。`id` 来自 `SS_LoadSound`。最小为 0，最大为 10000.

* SS_SetSoundPan(id,pan)

  设置音乐声道位置。`id` 来自 `SS_LoadSound`。-10000 为完全左，0 为中间，10000 为完全右。

* SS_SetSoundFreq(id,freq)

  设置音乐频率。`id` 来自 `SS_LoadSound`。freq 范围为 10000 - 100000.

* SS_SetSoundPosition(id,pos)

  设置音乐的播放位置。`id` 来自 `SS_LoadSound`。pos 是音乐的位置（字节），real 类型。

#### SS_Get 系列函数

SS_Get 系列函数可以让你获取声音的参数

* SS_GetSoundVol(id)

  获取音乐的音量设定。`id` 来自 `SS_LoadSound`。

* SS_GetSoundPan(id)

  获取音乐的声道位置。`id` 来自 `SS_LoadSound`。

* SS_GetSoundfreq(id)

  获取音乐的频率。`id` 来自 `SS_LoadSound`。

* SS_GetSoundPosition(id)

  获取音乐的播放位置。`id` 来自 `SS_LoadSound`。

* SS_GetSoundLength(id)

  获取音乐的总长度（字节）。`id` 来自 `SS_LoadSound`。

* SS_GetSoundBytesPerSecond(id)

  获取音乐每秒钟的字节数。`id` 来自 `SS_LoadSound`。

#### SS_IsSound 系列函数

SS_IsSound 系列函数可以帮助你获取音乐的状态

* SS_IsSoundPlaying(id)

  获取音乐是否正在播放。该函数无法区分播放与暂停，暂停需要用下一个函数判断。

* SS_IsSoundPaused(id)

  获取音乐是否暂停。

* SS_IsSoundLooping(id)

  获取音乐是否循环播放。

* SS_IsidValid(id)

  获取音乐 id 是否有效。
