# Quick start

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

I wanna, the derivative game of I Wanna be the Guy, is a kind of ~~shaking M~~ super fun 2D platform jumping action game. Among them, most of the I wanna derivative game production tools are `GameMaker` (hereinafter referred to as `GM`).

Before you create your own I Wanna game with I wanna be the Engine Nikaple Edition, you first need to download:

- **GameMaker 8.0 or 8.1** (GameMaker 8.0 Super Chinese Cracking is recommended) (http://p9wc9w6dq.bkt.clouddn.com/Super_Gamemaker8_1.4.2_Install.exe)
- **Engine body ** ([Download](http://p9wc9w6dq.bkt.clouddn.com/iwbte-nikaple-edition-1.9.0.zip))

Install `GM`, and use `GM` to open the `.gmk` file provided in the tarball to start the creation of the I wanna game!

## Preparation before starting

The online system is added to the new version of the engine, and the debug online function requires at least two client programs. To do this, you need to set the following:

- Open `GM 8.x`, ** uncheck ** `File -> Preferences -> General -> Hide compiler and enter wait mode when the game is running (English version: File -> Preference - > General -> Hide the designer and wait while the game is running`);
- Press the red triangle on the toolbar (compile the game in debug mode) twice, compile two games and start it in debug mode (note as `P1`, `P2`);
- Press `Shift` twice for `P1`, `Ctrl` for `P2`, and `Shift` for `P1`. Press `Shift` once to start the test;
- In order to avoid being logged off the same account by other players, you can register two accounts and set your own quick login mode with reference to [Debug Function] (/debug?id=Quick Login).

## Must read

- [Introduction to Creation Code](cc.md)

In previous versions, the `Creation Code` of object differed considerably, causing considerable inconvenience in use. Therefore, a new version of the `Creation Code` specification was redesigned in the new version so that developers can know what parameters to write without looking at the documentation.

- [New music system](music.md)

Solved the problem of long script names and was able to use a unified script to play music and sound effects.

- [New Trigger System](trigger.md)

Improves the efficiency of the `trg` system. Normal pits no longer have to write `sprite_index = xxx`

- [Debug Function](debug.md)

With the update of the online system, the debugging function has been further upgraded.

## New Features

- [Online Features](network.md)

Added full online features to support registration, login, creating/joining/leaving rooms, and up to 8 simultaneous games.

- [Multi-language support](i18n.md)

Adding a lightweight multilingual system makes your game faster and more international.

# Physics

It is basically the same as most engines.

# Compatibility

If the engine currently supports only GM 8.0 and GM 8.1.

# Thanks

Thanks to [NIHIL](http://tieba.baidu.com/home/main?un=towanoICIT) Daxuan guidance on the physics engine, without his help this engine should be: chicken::chicken::chicken:

# Known BUG

- `blockPush` gets stuck on the conveyor when pushed by the player

# Contact Author & BUG Feedback

Join Q group, verify information: I Wanna

![QR Code](../_images/group.png)

Feedback to me is also available through [Github Issues](https://github.com/nikaple/iwbt-nikaple-engine-doc/issues).
