# Script Documentation

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

## Functions

#### setGlobals()

For the initial setting of the game, see [Global Settings](global.md)

| Configuration Name                 | Use                                                      | Default                               |
| ---------------------------------- | -------------------------------------------------------- | ------------------------------------- |
| Global.game_title                  | Set Game Title                                           | I wanna be the Engine Nikaple Edition |
| Global.first_stage                 | Set the initial room when the game is officially started | rHub                                  |
| Global.enable_production_mode      | Whether to enable production mode                        | false                                 |
| Global.enable_internationalization | Whether to enable multilingual                           | true                                  |
| Global.language                    | language setting, optional LANG_CN, LANG_EN, LANG_JP     | LANG_CN                               |
| Global.encoding                    | Text Encoding                                            | gb2312                                |
| Global.enable_builtin_drawing      | Whether to use built-in drawing functions                | false                                 |
| Global.enable_stream_music         | Whether to use streaming music                           | true                                  |
| Global.game_room_width             | Window Width                                             | 800                                   |
| global.game_room_height            | Window Height                                            | 608                                   |
| Global.enable_focus                | Whether to use the keyboard to simulate the focus mode   | true                                  |
| Global.focus_key_code              | Using Keyboard to Simulate Focused Keycodes              | 1                                     |
| Global.enable_encryption           | Is the archive encrypted?                                | true                                  |
| Global.key                         | Archive File Encryption Key (at least 64-bit)            | huY...BTS                             |
| Global.ip_address                  | server IP address                                        | 139.\*.\*.59                          |
| Global.tcp_port                    | Server TCP Port                                          | 3738                                  |
| global.udp_port                    | Server UDP Port                                          | 3738                                  |
| global.max_sync_cycle              | Synchronization cycle                                    | 3                                     |
| Global.enable_lite_mode            | Whether lightweight mode is enabled                      | false                                 |
| Global.debug_host_name             | Debugging Host User Name                                 | username                              |
| Global.debug_host_pass             | Debugging Host Password                                  | password                              |
| Global.debug_guest_name            | Debugging non-host user names                            | test                                  |
| Global.debug_guest_pass            | Debugging non-host passwords                             | test                                  |

#### scrSealRoom(noTop, noLeft, noBottom, noRight)

Surround the room with bricks.

- noTop: Whether it is not capped
- noLeft: Whether to leave the left
- noBottom: whether it is not closed
- noRight: Whether to close the right

#### fadeIn(time)

Used in the step event to implement the fade-in effect of obj.

- time: obj fades in the elapsed time (frame). The default is 10 (1 frame = 0.02 seconds).

?> Before using this script, be sure to set the current obj's opacity 'image_alpha` to 0.

#### fadeOut(time)

Used in the step event to achieve the fade effect of obj.

- time: The elapsed time (frame) after obj fades out. The default is 10 (1 frame = 0.02 second).

?> If the opacity or size drops below 0, the current obj will be destroyed.

#### flashObject(flash_time, flash_count)

Make the current obj flash and set the variable "flash" to `true`.

When flashing ends, the flash variable will automatically return to 0, which is useful when setting the boss to be hit by a bullet.

- flash_time: time required for flashing once;
- flash_count: Total number of flashes.

#### splitObject(number, speed, object, direction, sprite)

Generate a circle with the same `obj` divergence.

- number: Generates the total number of `obj`s;
- speed: generates the speed of `obj`;
- object: generates the name of the obj object.
- direction: the direction in which the first `obj` is aimed;
- sprite: Generates the obj's sprite name (optional).

Among them, if direction is set to -1, the direction in which obj is generated will be random; if direction is set to 1, the direction in which obj is generated will be aimed at player; if direction is set to another value, it will be in the specified direction.

?> Direction in GM: 0 to the right, 90 to the up, counterclockwise is positive

#### autoSpikeSprite

See [Automatically Replace Spiked Wizard](autosprite.md)

#### screenShake(time, shakeX, shakeY)

Generate a shock screen effect.

- time: duration of the screen effect (frame);
- shakeX: amplitude of lateral vibration;
- shakeY: the amplitude of the vertical vibration.

#### screenFlash(time)

Generate a screen flash effect.

- time: The duration (frame) of the flash effect.

#### createShadow(alpha_speed, scale_speed)

Produce smear effects, often used for alarm events and repeated calls.

- alpha_speed: the amount of shadow opacity reduction per step;
- scale_speed: The amount of reduction in shadow size per step.

For example: `Alarm 0` event of `obj BossBullet`:

```gml
createShadow(0.1, 0);
Alarm[0] = 2;
```

#### setScale(xscale,yscale)

Sets the amount of obj stretching in the x and y directions. It has been replaced with the `xs`,`ys` two parameters.

- xscale: the amount of x-direction stretching
- yscale: the amount of stretching in the y direction

## Music

For details, see [music player](music.md)

#### music_init()

Initialize music here.

#### music_config()

Set the music to play in each room here.

#### music_load(file)

Load a piece of external music in the format `ogg`.

#### music_play(id)

Play music or sound effects. `id` comes from the sound resource in `music_load` or `gmk`.

#### music_stop(id)

Stop music or sound effects. `id` comes from the sound resource in `music_load` or `gmk`.

#### music_loop(id)

Loop music. `id` comes from `music_load`.

#### music_pause(id)

Pause music. `id` comes from `music_load`.

#### music_resume(id)

Keep playing music. `id` comes from `music_load`.

## Network

### ns

`ns` is the `Nikaple Server`, which is the core part of the online engine functionality. Before viewing the documentation, take a look at the online system's [introduction](network.md).

It can be divided into 5 main sections:

- ns_get: Get game information;
- ns_is: determine the status of the game;
- ns_actions: Perform some operations, such as registering, logging in, joining a room, etc.
- ns_send: Synchronize information to the server (using the TCP protocol, commonly used);
- ns_sync: Synchronize information to the server (uses UDP protocol, not commonly used).

#### ns_get

| Script Name                     | Use                                                                                                  |
| ------------------------------- | ---------------------------------------------------------------------------------------------------- |
| ns_get_player_name()            | Get the current player's name (username)                                                             |
| ns_get_player_index()           | Get the number of the current player in the game (1 is homeowner, greater than 1 are non-homeowners) |
| ns_get_other_player_name(index) | Get a name based on another player's number                                                          |
| ns_get_other_player_index(name) | Get a number based on another player's name                                                          |
| ns_get_lobby_id()               | Get the current room ID, or 0 if it does not exist.                                                  |
| ns_get_lobby_name()             | Get the current room name, or an empty string if it does not exist.                                  |
| ns_get_game_id()                | Get the number of the current game on the server side.                                               |

#### ns_is

| Script Name         | Use                            |
| ------------------- | ------------------------------ |
| ns_is_online_mode() | Is Online Mode?                |
| ns_is_connected()   | Is it connected to the server? |
| ns_is_logged_in()   | Is it logged in?               |
| ns_is_in_lobby()    | Is it in the room?             |
| ns_is_host()        | Is it a homeowner?             |
| ns_is_guest()       | Is it a non-homeowner?         |
| ns_is_in_game()     | Is it in the game?             |

#### ns_actions

| Script Name       | Use               |
| ----------------- | ----------------- |
| ns_register()     | Register          |
| ns_login()        | Login             |
| ns_logout()       | Logout            |
| ns_fetch_lobby()  | Inquiry Room List |
| ns_create_lobby() | Create Room       |
| ns_join_lobby()   | Join Room         |
| ns_leave_lobby()  | Leave the room    |
| ns_start_game()   | Start the game    |

#### ns_send

##### ns_send(cmd)

Send requests directly to the server (basically no need)

##### ns_send_instance

The function of this function is shown in the following figure:

![ns_send_instance](../_images/ns_send_instance.png)

##### ns_send_event

The function of this function is shown in the following figure:

![ns_send_event](../_images/ns_send_event.png)

##### ns_send_wait

The function of this function is shown in the following figure:

![ns_send_wait](../_images/ns_send_wait.png)

For detailed usage of these three scripts, see [Introduction to Online](network.md)

##### ns_send_instance_direct(ds_map)

##### ns_send_event_direct(ds_map)

##### ns_send_wait_direct(ds_map)

Sometimes the three scripts `ns_send_instance`, `ns_send_event`, `ns_send_wait` may not meet your needs. This may be because:

- Add attributes only under certain conditions to reduce the transfer size;
- Since the `GM` supports up to 16 parameters, the added attribute may exceed the upper limit of the parameter.

At this point the `ns_send_*_direct` family of functions happens to come in handy. They all receive a `cmd` that represents the properties that need to be synchronized.

For example, in the `alarm[11]` of `player`, sync the current room:

```gml
// Create a ds_map with 5 elements
eventMap = cmd_init(
    4,
    'r', room,
    'x', x,
    'y', floor(y),
    'xs', image_xscale,
)
// Optionally add rev and sync
cmd_add_if_exists(
  eventMap, 2,
  'sync', global.__sync_position,
  'rev', global.reverse
)
// Send this ds_map directly as an event
ns_send_event_direct('warp', eventMap)
// Do not need to manually call ds_map_destroy
```

```gml
// If there are too many attributes to sync, you can add 7 first:
eventMap = ds_map_init(
  7,
  'a', 1,
  'b', 2,
  'c', 3,
  'd', 4,
  'e', 5,
  'f', 6,
  'g', 7
)
// continue to add
ds_map_append(
  eventMap, 2,
  'h', 8,
  'i', 9
)
// This will send an event with 9 properties
ns_send_instance_direct(eventMap)
```

#### ns_sync

##### ns_sync_begin

Use UDP protocol to synchronize other object needs to use. See details: [Use UDP synchronization](/network?id=using-udp-to-synchronize)

##### ns_sync_player

Synchronize `player` with UDP protocol, generally do not need to modify.

### handler

This folder stores various event handlers.

#### commands

Processing ordinary instructions

| Script Name                      | Event Name                    |
| -------------------------------- | ----------------------------- |
| handler_cmd_connected            | Server Connection Successful  |
| Handler_cmd_connect_failed       | server connection failed      |
| Handler_cmd_udp_shakehand        | UDP handshake success         |
| Handler_cmd_register_success     | Registration Successful       |
| handler_cmd_register_failed      | Registration failed           |
| handler_cmd_login_success        | Login Success                 |
| handler_cmd_login_failed         | Login failed                  |
| handler_cmd_login_already        | Already logged in             |
| Handler_cmd_login_needed         | Sign in to continue           |
| handler_cmd_logout               | Log Out Success               |
| Handler_cmd_lobby_fetch_success  | Successfully loaded room list |
| Handler_cmd_lobby_create_success | Successfully created room     |
| Handler_cmd_lobby_join_success   | Successfully Joined Room      |
| Handler_cmd_lobby_leave_success  | Successfully left room        |
| Handler_cmd_lobby_not_exists     | Room number does not exist    |
| Handler_cmd_lobby_not_found      | Quit non-existent room        |
| Handler_cmd_lobby_pass_not_valid | Room password error           |
| Handler_cmd_lobby_same_id        | Repeating Join Room           |
| Handler_cmd_lobby_is_full        | Room is full                  |
| Handler_cmd_lobby_not_authorized | Non-Homeowner Start Game      |
| Handler_cmd_game_start           | Homeowners start the game     |
| handler_cmd_sync                 | Synchronizing Game Data       |
| Handler_cmd_player_drop          | Player dropped                |

#### event

Handling event synchronization instructions

| Script Name                | Event Name              |
| -------------------------- | ----------------------- |
| Handler_event_player_shoot | Player Shooting         |
| Handler_event_player_death | Player Death            |
| Handler_event_warp         | Player Send or Reset    |
| handler_event_reset_sync   | Synchronization Reset   |
| handler_event_save_sync    | Synchronization Archive |

#### wait

Process wait event synchronization instructions

| Script Name        | Event Name           |
| ------------------ | -------------------- |
| handler_wait_reset | Waiting for reset    |
| handler_wait_save  | Waiting for save     |
| handler_wait_warp  | Waiting for Delivery |

## Util

Practical method.

### ds_map

#### ds_map_init(kvCount, k1, v1, k2, v2, ..., kn, vn)

Initialize a `ds_map` and return `id`.

- The first parameter is the number of key-value pairs n;
- The next 2n parameters are of the form key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub>'s key-value pair.

#### ds_map_append(id, kvCount, k1, v1, k2, v2, ..., kn, vn)

Append a key-value pair to a `ds_map` to return `id`.

- The first argument is `id` of `ds_map`;
- The first parameter is the number of key-value pairs n;
- The next 2n parameters are of the form key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub>'s key-value pair. W

#### ds_map_clone(id)

[Shallow Clone] (https://baike.baidu.com/item/Shallow Copy/12601426) A `ds_map` that returns the `ds` of the new `ds_map`.

#### ds_map_log(id)

Output a `ds_map` as a string.

### ds_list

#### ds_list_init(itemCount, item1, item2, ..., itemn)

Initialize a `ds_list` and return `id`.

- The first parameter is the number of elements in the list;
- The next n parameters are the elements that need to be added to the list.

#### ds_list_append(id, itemCount, item1, item2, ..., itemn)

Appends an element to a `ds_list`, returning `id` .

- The first argument is `id` of `ds_list`;
- The first parameter is the number of elements in the list;
- The next n parameters are the elements that need to be added to the list.

#### ds_list_clone(id)

[Shallow Clone] (https://baike.baidu.com/item/Shallow Copy/12601426) A `ds_list` returns the `id` of the new `ds_list`.

#### ds_list_log(id)

Output a `ds_list` as a string

#### ds_list_remove(id, item)

Removed the first element with the value `item` from `ds_list`

#### ds_list_replace_item(id, item, newItem)

Replace the first element of `dsm` in `ds_list` with `newItem`

### error

For error message processing

| Script Name      | Use                                                                                                           |
| ---------------- | ------------------------------------------------------------------------------------------------------------- |
| ensure           | Make sure a variable exists (not 0)                                                                           |
| error_ind_zero   | Make sure a resource with a 0 number does not exist                                                           |  |
| error_kv         | When using `cmd`, `ns_send`, etc. functions did not declare `kvCount`                                         |
| Error_item       | Not declared when using the `cmd_list` series function `ite mCount`                                           |
| Error_kv_zero    | When using functions such as `cmd`, `ns_send`, etc., provide more key/value pairs than the declared `kvCount` |
| error_arg_exceed | Too many parameters                                                                                           |
| Error_info       | Common Error Messages                                                                                         |

### Miscellaneous

#### debug(str1, str2, str3, ...)

Output debugging information. See [Debugging Features](/debug?id=objdebug) for details

#### set_default(value, default)

Used to set the default value.

```gml
// sprite_index is set to spr if spr is provided, otherwise unchanged.
sprite_index = set_default(spr, sprite_index)
```

#### ensure_not_empty

Verify that user input cannot be empty.

#### destroy_if_exists(obj)

Destroy `obj` if `obj` exists

#### clamp(x, a, b)

Returns a when x < a, b if x > b, otherwise x

#### is_zero

Type safety verification is 0

## Draw

Extra drawing function.

#### drawSelf

Used in the draw event to draw obj itself. **When an obj owns the draw event, its sprite is not automatically drawn on the screen. At this time, you need to use the drawSelf function to draw the obj's original sprite**.

For example, in `warp` (`roomChanger`), you need to draw both the `warp` sprite and the text above `warp`, so when `drawing_text` draws text, you also need to call `drawSelf` to draw the `warp` sprite. .

```gml
//draw the original sprite
drawSelf();
//draw the text
If (is_string(text)) {
  I18n_draw_set_font(fontMsyh12);
  I18n_draw_set_align(fa_center, fa_bottom)
  I18n_draw_text_ext_color(x + 16, y - 8, text, 8, -1, color, color, alpha);
}
```

#### drawLife(x1, y1, x2, y2, curVal, maxVal, col1, col2, outline)

Used in the draw event to draw a blood bar.

- (x1,y1), (x2,y2): The coordinates of the upper left and lower right corners of the bloodstrip
- curVal: variable representing current blood volume
- maxVal: maximum blood volume
- col1: The color of the blood bar when it is full
- col2: The color of the blood bar when empty
- outline: Whether to draw a border

`obj HPBar - Draw Event`:

```gml
drawLife(
  40, 10, 760, 22,
  boss_obj.curHP, boss_obj.maxHP,
  C_lime, c_red, 1, c_black
);
```

#### draw_set_align(halign, valign)

Quickly set the horizontal and vertical alignment of text

#### draw_rectangle_view()

Draws a rectangle in the current view. Without parameters, color/alpha needs to be set in advance.

#### draw_rectangle_width(x1, y1, x2, y2, width)

Draw a rectangle with width `width`

#### draw_rectangle_single_color(x1, y1, x2, y2, color, outline)

Draw a single color rectangle

#### draw_text_transformed_outline(x, y, string, xscale, yscale, angle, outline_color, text_color)

Draw stroke text

- x, y position
- string text
- xscale horizontal zoom
- yscale vertical scale
- angle text angle
- outline_color stroke color
- text_color text color

## System

### Player

#### killPlayer

Calling directly at any time allows the player to die immediately.

#### playerInit

Initialize the parameters of `player`.

- infJump: whether it can jump infinitely
- jump[1]: a jump speed
- jump[2]: second-hop speed
- maxJumps: Total number of jumps (written to archive)
- maxSpeed: horizontal speed (written to archive)
- grav: Gravity (written in archive)
- shootInterval: burst interval (written to archive)
- maxAirSpeed: maximum drop speed
- maxWaterSpeed: The maximum drop speed in the water

#### remaining player scripts

| Script Name         | Use                                              |
| ------------------- | ------------------------------------------------ |
| playerSprite        | Settings Wizard                                  |
| playerCheckKeyboard | Keyboard Key Detection                           |
| playerMove          | mobile                                           |
| playerJump          | Jumping                                          |
| playerVJump         | Jump Related                                     |
| playerWallJump      | Climbing Wall                                    |
| playerPlatform      | Board Collision                                  |
| playerColllideBlock | Brick Collision                                  |
| playerReverse       | Flip Gravity                                     |
| playerSync          | sync information                                 |
| playerForceSync     | for synchronizing player positions               |
| playerMisc          | Miscellaneous, such as debugging functions, etc. |

### World

| Script Name              | Use                                               |
| ------------------------ | ------------------------------------------------- |
| scrWorldInit             | Initialization                                    |
| scrWorldInitPlugins      | Initialize Plugins                                |
| scrWorldInitMessageBox   | Initialize Popup Style                            |
| scrWorldInitRunCheck     | Pre-operation check                               |
| scrWorldInitBlocks       | Initializing Red and Blue Bricks                  |
| scrWorldInitViews        | Initialize View                                   |
| scrWorldAppendDifficulty | Show difficulty in game titles                    |
| scrWorldUpdateCaption    | Update Game Title                                 |
| scrWorldUpdateTime       | Update Game Time                                  |
| scrWorldCleanmem         | Clean Up Memory                                   |
| scrWorldCenterMessage    | Message Window Centering                          |
| scrWorldReset            | Reset Game                                        |
| scrWorldStopDeathSound   | Stop Death Sound                                  |  |
| scrWorldPause            | Paused Games                                      |
| scrWorldFixBug           | Resolve a bug that pushes 1 frame when pressing R |
| scrWorldLoadGlobalSave   | Synchronization Archive for Online Mode           |

### Controls

### Save

#### saveGame()

Save the game. For details, see [New Archive System](save.md)

#### loadGame()

Read the game. For details, see [New Archive System](save.md)

#### saveDeathTime()

#### loadIcons()

### Miscellaneous

#### setGlobalsMinor()

Some modify the less likely configuration items.

| Configuration Name               | Use                                             | Default     |
| -------------------------------- | ----------------------------------------------- | ----------- |
| Global.enable_pause_in_boss_room | BOSS Allowed to pause in the room               | false       |
| global.enable_jump_cancel        | Whether to allow skip cancellation (JC)         | false       |
| Global.enable_fullscreen         | Is it permissible to press F4 full screen       | true        |
| global.enable_keypad             | Is the keypad allowed                           | true        |
| Global.enable_auto_spike_sprite  | Does it automatically change the spear's sprite | true        |
| Global.boss_number               | BOSS cap                                        | 64          |
| global.item_number               | Maximum Number of Items                         | 64          |
| global.data_number               | Maximum number of custom data                   | 64          |
| global.saving_directory          | Archive Save Path                               | Data/Save   |
| global.music_directory           | Music Read Path                                 | Data/Music  |
| global.sound_directory           | Sound Read Path                                 | Data/Sound  |
| global.plugin_directory          | Plugin Read Path                                | Data/Plugin |
| global.font_directory            | Font Read Path                                  | Data/Font   |
| global.option_file_name          | Configuration File Name                         | options.ini |

#### spikeSprite(spr, miniSpr, image_speed)

Used for [Automatically changing thorn sprites](autosprite.md)

#### getSaveFile(num)

Get the save file name with the number `num`

#### gamePause()

Pause the game

#### gameResume()

Continue the game

#### gameReset()

Called when you press `F2`

#### isInGameRoom()

To determine if it is an in-game room (non-title, lobby, select levels, etc.)

#### scrWarpTo(r, num, mode, width, height, clearSpeed, screens, kind)

Warping function. See [Warps](en-us/objectref?id=warps)

## Lib

### audio

#### audio_init()

Initializing the ini configuration file is done only once at the beginning of the game and does not require modification.

#### audio_update()

Updates music configuration and is called after changing music settings.

#### audio_setsoundvolume (add_volume)

Increase/Decrease sound volume. audio_setsoundvolume(1) increases the sound volume by 1 point.

#### audio_setmusicvolume (add_volume)

Increase/decrease music volume. audio_setmusicvolume(-1) will reduce the volume of music by 1 point.

#### audio_togglesoundmuted()

Toggle sound mute/unmute.

#### audio_togglemusicmuted()

Switch music mute/unmute.

#### audio_playsound(sound)

For playing sound effects (sound variables in the Sound folder in the GM), this script solves the win8 compatibility issue, so use this script instead of direct sound_play to play sound effects. Since the global volume is used, the volume of the sound file cannot be adjusted directly in the GM, but a value is required in front of the script to adjust the default volume. (You can correct your own sound according to the example.)

#### audio_playmusic(music)

Play external music (see section 3)

#### audio_loopmusic(music)

Looping external music (see section 3)

#### audio_pausemusic(music)

Suspend external music

#### audio_resumemusic(music)

When the music is paused, the music continues to play.

### i18n

#### i18n_init

Initialize i18n multi-language script.

#### i18n_font_init()

This script is used to initialize all `i18n fonts`.

#### i18n_font_load(name, size, bold, italic, underline)

Read a font from the `Data/Fonts` directory and return its id.

- name: font file name;
- size: font size;
- Bold: Bold;
- italic: whether italic;
- underline: whether to underline.

#### i18n_font_add(name, cn, en, jp)

Add an `i18n font`.

- name: font name;
- cn: Chinese font;
- en: English font;
- jp: Japanese font.

#### i18n_add(i18n_id, cn, en, jp)

Add an entry to the i18n library.

- i18n_id: i18n identifier;
- cn: Chinese string represented by this identifier;
- ce: the English string represented by this identifier;
- jp: Japanese string represented by this identifier.

#### i18n_get(i18n_id)

Extract the string represented by i18n_id in the current language

#### i18n_set_lang(lang)

Set the current language to `lang`. Possible values ​​are: `LANG_CN`, `LANG_EN`, `LANG_JP`.

#### i18n_get_lang()

Get current language

#### i18n_free()

Release the memory space of the i18n module

#### i18n_auto_encoding()

This script is called in `objEffectParent` to set the encoding for various languages.

#### i18n Extended Script List

The draw series and message series functions are preceded by `i18n_` which is the corresponding multi-language content. See [Multilingual Support](i18n.md)

| i18n script                          | Corresponding native function   | Remarks                                 |
| ------------------------------------ | ------------------------------- | --------------------------------------- |
| i18n_draw_set_alpha                  | draw_set_alpha                  | Fully consistent with native function   |
| i18n_draw_set_color                  | draw_set_color                  | Fully consistent with native function   |
| i18n_draw_set_font                   | draw_set_font                   | Can only add i18n font                  |
| I18n_draw_set_align                  | None                            | Quick Set Horizontal and Vertical align |
| i18n_draw_set_halign                 | draw_set_halign                 | None                                    |
| i18n_draw_set_valign                 | draw_set_valign                 | None                                    |
| i18n_draw_text                       | draw_text                       | None                                    |
| i18n_draw_text_ext                   | draw_text_ext                   | None                                    |
| i18n_draw_text_transformed           | draw_text_transformed           | None                                    |
| i18n_draw_text_ext_transformed       | draw_text_ext_transformed       | None                                    |
| I18n_draw_text_color                 | draw_text_color                 | There can only be two color             |
| i18n_draw_text_ext_color             | draw_text_ext_color             | There can only be two color             |
| i18n_draw_text_transformed_color     | draw_text_transformed_color     | There can only be two color             |
| i18n_draw_text_ext_transformed_color | draw_text_ext_transformed_color | There can only be two color             |
| i18n_string_width                    | string_width                    | None                                    |
| i18n_string_height                   | string_height                   | None                                    |
| i18n_string_width_ext                | string_width_ext                | None                                    |
| i18n_string_height_ext               | string_height_ext               | None                                    |
| i18n_show_message                    | show_message                    | None                                    |
| i18n_show_message_ext                | show_message_ext                | None                                    |
| i18n_get_integer                     | get_integer                     | None                                    |
| i18n_get_string                      | get_string                      | None                                    |

### json

This module is used for the parsing of [JSON](https://www.json.org/json-zh.html) strings.

#### json_init()

Initialize the JSON module

#### json_decode(str)

Parse a JSON string (str) and return a ds_map

#### json_destroy(ds_map)

Releases the memory space parsed by ds_map

#### json_free()

Free up the memory space of the JSON module

#### json_pick(key)

Extract a property `key` from JSON. This function is exactly the same as `ds_map_find_value`.

#### json_get

Deeply extract a property from JSON. E.g:

```gml
json = json_decode('
  {
    "foo": {
      "bar": ["baz", "qux"]
    }
  }
')

json_get(json, 3, "foo", "bar", 0) // baz
```

#### json_log(str)

Output a JSON string in a read-friendly way

### cmd

This module is used to build a serializable `ds_map`.

!> Due to the inability to construct serializable JSON using the `ds` and `ds_map` built-in to `GM`, you need to use the `cmd_*` function to construct the request directly.

#### cmd_init(cmd)

Initialize a `cmd` and return `cmdId`. E.g:

```gml
cmd = cmd_init('hello', 1, 'name', 'Nikaple')
// Convert cmd to json
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "name": "Nikaple"
}
*/
```

?> An empty `ds_map` will be created if cmd is not provided.

#### cmd_destroy(cmd)

Clear a `cmd` to release the memory it occupies.

#### cmd_log(cmd)

Output a `cmd` in a read-friendly way.

#### cmd_add(cmd, kvCount, key1, value1, ..., keyn, valuen)

Add a new key-value pair to `cmd` and return `cmdId`. E.g:

```gml
cmd = cmd_init('hello')
cmd_add(
  cmd, 1,
  'name', 'Nikaple',
  'text', 'faQ'
)
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "name": "Nikaple",
    "text": "faQ"
}
*/
```

#### cmd_add_list(cmd, key, itemCount, item1, item2, ..., itemn)

Add a `list` to `cmd` and return `listId`. E.g:

```gml
cmd = cmd_init('hello', 1, 'name', 'Nikaple')
cmd_add_list(
  cmd, 'text', 5,
  'I', 'Wanna', 'be', 'the', 'guy!'
)
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "name": "Nikaple",
    "text": ["I", "Wanna", "be", "the", "guy!"]
}
*/
```

#### cmd_add_map(cmd, key, kvCount, key1, value1, ..., keyn, valuen)

Add a `ds_map` to `cmd` and return `mapId`. E.g:

```gml
cmd = cmd_init('hello')
cmd_add_map(
  cmd, 'content', 2,
  'name', 'Nikaple',
  'text', 'faQ'
)
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "content": {
        "name": "Nikaple",
        "text": "faQ"
    }
}
*/
```

#### cmd_list_add(list, itemCount, item1, item2, ..., itemn)

Add a new element to a `list` in `cmd` and return `listId`. E.g:

```gml
cmd = cmd_init('hello', 1, 'name', 'Nikaple')
list = cmd_add_list(
  cmd, 'text', 5,
  'I', 'Wanna', 'be', 'the', 'guy!'
)
cmd_list_add(list, 1, 'Gaiden')
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "name": "Nikaple",
    "text": ["I", "Wanna", "be", "the", "guy!", "Gaiden"]
}
*/
```

#### cmd_list_add_list(list, itemCount, item1, item2, ..., itemn)

Add a `list` to a `list` in `cmd` and return `listId`. E.g:

```gml
cmd = cmd_init('hello', 1, 'name', 'Nikaple')
list = cmd_add_list(
  cmd, 'text', 5,
  'I', 'Wanna', 'be', 'the', 'guy!'
)
cmd_list_add_list(list, 1, 'Gaiden')
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "name": "Nikaple",
    "text": ["I", "Wanna", "be", "the", "guy!", ["Gaiden"]]
}
*/
```

#### cmd_list_add_map(cmd, kvCount, key1, value1, ..., keyn, valuen)

Add a `map` to a `list` in `cmd` and return `mapId`. E.g:

```gml
cmd = cmd_init('hello', 1, 'name', 'Nikaple')
list = cmd_add_list(cmd, 'content')
cmd_list_add_map(
  cmd, 2,
  'name', 'Nikaple',
  'text', 'faQ'
)
cmd_log(cmd)
/*
{
    "cmd": "Hello",
    "content": [{
        "name": "Nikaple",
        "text": "faQ"
    }]
}
*/
```

### fake_random

Used for pseudo-random. In the BOSS battle, no other object other than BOSS should use the random series function, otherwise it will destroy the current random number seed. To use it, you must use pseudo-random.

| Name               | Use                          |
| ------------------ | ---------------------------- |
| fake_random_init   | Pseudo Random Initialization |
| fake_random        | pseudo random                |
| fake_irandom       | Pseudo-irandom               |
| fake_random_range  | pseudo random_range          |
| fake_irandom_range | Pseudo-irandom_range         |

### auto_tile

Used to automatically draw textures. See [Automatic Mapping](autotile.md)

## Plugins

### Http Dll 2.3

- [Http Dll 2.3 Help Documentation](http://www.maartenbaert.be/game-maker-dlls/http-dll-2/)

### FoxWriting

- [FoxWriting Help Documentation](http://docs.magecorn.com/doc-view-54.shtml)

### CleanMem

- cleanmem_init(free_switch)

- free_switch = 0: Initialize Dll
     - free_switch = 1: Release Dll

- cleanmem_get_mem

Get current memory footprint

- cleanmem

Clear memory

### Super Sound System

#### Commonly used

- SS_Init()

Initialization must be called at the beginning of the game.

- SS_LoadSound(fname, stream)

This function returns a music `id` to be used by other functions.

- fname: filename
    - stream: set to 0 to load music into memory at once; set to 1 to load in sections

- SS_PlaySound(id)

play music. `id` from `SS_LoadSound`

- SS_LoopSound(id)

Loop music. `id` from `SS_LoadSound`

- SS_StopSound(id)

Stop playing music. `id` from `SS_LoadSound`

- SS_FreeSound(id)

Free up memory space occupied by music. `id` from `SS_LoadSound`

- SS_PauseSound(id)

Pause music playback. `id` from `SS_LoadSound`

- SS_ResumeSound(id)

Keep playing music. `id` comes from`SS_LoadSound`. If the music is paused, it will continue to play; otherwise it will start playing again. Returns 1 if successful, otherwise returns 0.

- SS_Unload()

Must be called at the end of the game.

#### SS_Set Series Functions

SS_Set series function allows you to set the parameters of the sound

- SS_SetSoundVol(id, vol)

Set the music volume. `id` comes from`SS_LoadSound`. The minimum is 0 and the maximum is 10000.

- SS_SetSoundPan(id, pan)

Set the music channel position. `id` comes from`SS_LoadSound`. -10000 is completely left, 0 is middle, and 10000 is completely right.

- SS_SetSoundFreq(id, freq)

Set the music frequency. `id` comes from`SS_LoadSound`. The freq range is 10000 - 100000.

- SS_SetSoundPosition(id, pos)

Set the music playback position. `id` comes from`SS_LoadSound`. Pos is the music's location (bytes), real type.

#### SS_Get Series Functions

SS_Get series function allows you to get the parameters of the sound

- SS_GetSoundVol(id)

Get music volume settings. `id` comes from`SS_LoadSound`.

- SS_GetSoundPan(id)

Get the channel position of the music. `id` comes from`SS_LoadSound`.

- SS_GetSoundfreq(id)

Get the frequency of music. `id` comes from`SS_LoadSound`.

- SS_GetSoundPosition(id)

Get music playback position. `id` comes from`SS_LoadSound`.

- SS_GetSoundLength(id)

Get the total length of music in bytes. `id` comes from`SS_LoadSound`.

- SS_GetSoundBytesPerSecond(id)

Get the number of bytes per second of music. `id` comes from`SS_LoadSound`.

#### SS_IsSound Family Functions

The SS_IsSound family of functions helps you to get the status of your music

- SS_IsSoundPlaying(id)

Get music is playing. `id` comes from`SS_LoadSound`. This function cannot distinguish between play and pause. The pause needs to be judged by the next function.

- SS_IsSoundPaused(id)

Get music paused. `id` comes from`SS_LoadSound`.

- SS_IsSoundLooping(id)

Get whether the music loops. `id` comes from`SS_LoadSound`.

- SS_IsidValid(id)

Get music id is valid. `id` comes from`SS_LoadSound`.
