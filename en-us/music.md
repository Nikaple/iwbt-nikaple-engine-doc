# play music

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

The engine uses the [Super Sound](http://gmc.yoyogames.com/index.php?showtopic=120034) music system. With its support, you can read sound files from the outside and pause and continue. Play music (this is what GM can't do with its own function).

?> Super Sound supports only ogg and wav music formats, ogg format is recommended (wav format music takes up too much space). Therefore, before using music, you need to convert it to ogg format. This can be done with [Beaver's Nest Universal Video Converter](http://www.leawo.cn) or [Online Transcoding Website](https://convertio.com). Co/zh/) to complete.

Music playback involves two scripts: `music_init` and `music_config`, both of which are in the `Scripts -> audio` folder.

- `music_init` is used to read music from an external folder into the game;
- `music_config` will be called once at the beginning of each room to determine the music to be played in each room.

?> The location of the music can be set via `global.music_directory` in `setGlobalsMinor`, ​​defaults to `Data/Music`

## Upgrade to 2.0

After the engine was upgraded to version 2.0, the script name for playing music was more uniform:

```gml
// Music and sound can be played using music_play
music_play(sndBlockChange)
music_play(BGM_BOSS1)
// Music and sound can be stopped using music_stop
music_stop(sndDeath)
music_stop(curMusic)
// Music can also use related script loops, pauses, resume playback
music_loop(BGM_1)
music_pause(BGM_1)
music_resume(BGM_1)
```

## How to set up room music

- In `music_init`, the engine will automatically read all files in the music folder (default is Data/Music) and store its id in the global variable `BGM_ filename`. E.g:

  - `Death.ogg` is automatically read as `BGM_Death`;
  - `faQ.ogg` is automatically read as `BGM_faQ`;
  - `myMusic.ogg` is automatically read as `BGM_myMusic`.

- In `music_config`, follow the example to add code to play music, for example:

  ```gml
  // add your code here
  case myRoom:
      music_play(BGM_myMusic);
      Break;
  ...
  ```

Note that the following `break` cannot be omitted!

## BOSS Room BGM Processing

In the BOSS room, you may want to control the timing of BGM playback yourself. It can be set as follows:

1.  First find the script `isBossRoom` and set the related room to BOSS (see the script).

2.  When you need to play BOSS Battle Music, call:

    ```gml
    music_play(myMusic);
    ```

?> By default, BOSS cannot be suspended in the room. If you need to allow pauses, you can change `global.enable_pause_in_boss_room = true` in the `setGlobalsMinor` script.
