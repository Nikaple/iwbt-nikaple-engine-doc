# Global configuration

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

## Common Global Settings

In the engine, the main game-related global configurable items are placed in `Scripts -> functions -> setGlobals`.

### Game-related settings

#### global.game_title

The title of the game is displayed in the title bar of the game window.

#### global.first_stage

The initial room when the game officially begins (excluding rooms such as titles and selections).

#### global.enable_production_mode

Whether to enable production mode, the default is `false`. In the production mode, the custom error message in the engine is not triggered (GM cannot report error).

#### global.enable_internationalization

Whether to enable [multi-language support](i18n.md), the default is `true`.

#### global.language

Default language setting, default is `LANG_CN`. The options are `LANG_CN`, `LANG_EN`, `LANG_JP`.

#### global.encoding

Text encoding, defaults to `gb2312`. This should be the same as the operating system text code you are using. See the Encoding Table (https://msdn.microsoft.com/en-us/library/windows/desktop/dd317756.aspx).

#### global.enable_builtin_drawing

Whether to use the built-in drawing function, the default is `false`. If on, the built-in return function will be used when the language is `LANG_EN`; if it is off, `FoxWriting` will be used for drawing.

#### global.game_room_width

Game window width

#### global.game_room_height

Game window height

#### global.enable_stream_music

Whether to enable streaming, the default is `true`. After opening, the music will be loaded into memory in sections, which greatly improves the operating efficiency, but the defect is that it cannot be suspended.

?> In streaming mode, when the player dies or the game is paused, the background music will not be paused but only decrease the volume.

#### global.enable_focus

Whether to use the keyboard to simulate the focus mode. The principle is to constantly trigger a non-existent key in the game. This key can only be valid when the window is focused. Open by default.

#### global.focus_key_code

Use the keyboard to simulate the focused key code. The default is `1`, which is `?`.

#### global.enable_encryption

Whether the save file is encrypted, the default is `true`.

#### global.key

save file encryption key. To ensure security, the key length should not be less than 64.

### Network related settings

#### global.ip_address

Server IP address. The address provided in the engine is for testing purposes only and is not guaranteed to be available at any time. Recommend deploying your own server to enhance stability when you release the game.

#### global.tcp_port

Server TCP port, default 3738.

#### global.udp_port

Server UDP port, default 3738.

#### global.online_mode

Online mode, turned on by default.

#### global.max_sync_cycle

Synchronization cycle. This value determines the frequency of data synchronization between clients. By default, a synchronous packet is sent every 3 frames.

### debugging related settings

#### global.enable_lite_mode

Lightweight mode (fast test only). After opening, it will directly read the number one save after running the game compilation, skip the title, menu and other interfaces.

#### global.debug_host_name

Debugging host user name (for fast login)

#### global.debug_host_pass

Commissioning host password (for fast login)

#### global.debug_guest_name

Non-host user name for debugging (fast login)

#### global.debug_guest_pass

Non-host password for debugging (fast login)

## Secondary global settings

Some basic configuration items that will not be changed are located in `system -> setGlobalsMinor`.

#### global.enable_pause_in_boss_room

BOSS is allowed to pause in the room. The default is `false`.

#### global.enable_jump_cancel

Whether to allow skip cancellation (JC), the default is `false`.

#### global.enable_fullscreen

Whether to allow pressing F4 full screen, the default is `true`.

#### global.enable_keypad

Whether to allow the use of a keypad, the default is `true`.

#### global.enable_auto_spike_sprite

Whether it is [auto sprite sprite](autosprite.md), defaults to `true`.

#### global.boss_number

The maximum number of BOSSs, the default is `64`.

#### global.item_number

The maximum number of items, the default is `64`.

#### global.data_number

The maximum number of custom data, the default is `64`.

#### global.saving_directory

save path, default is `Data/Save`.

#### global.music_directory

The music read path defaults to `Data/Music`.

#### global.plugin_directory

Plug-in read path, default is `Data/Plugin`.

#### global.option_file_name

Configuration file name, defaults to `options.ini`.
