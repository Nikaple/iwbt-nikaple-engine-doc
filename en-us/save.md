# Archive function

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

In order to improve the efficiency and security of archiving, version 2.0 of the engine has been rewritten. The new version of the archive uses a binary system but maintains high readability.

The archive system involves four scripts:

- `saveGame` is used to save the game
- `loadGame` is used to read the game
- `saveDeathTime` is used to save only time and number of deaths
- `loadIcons` is used to read archived information on select archive page

## Save Custom Variables

In the new engine, the default support for 64 custom numbers and 64 strings of storage, you can use them to save the game's global status.

- Numbers are stored using `global.data[1] - global.data[64]`
- Storage of string types using `global.text[1] - global.text[64]`

You can flexibly define the constants using `GM`'s `Resources-> Define Constants...` function to achieve better code readability.

Suppose you have a lot of diamonds in your game and you need to save the number of diamonds the player currently owns. You can:

1.  Define the constant `SAVE_DIAMOND_AMOUNT` to 1;
2.  Every time the player gets a diamond, execute `global.data[SAVE_DIAMOND_AMOUNT] += 1`;
3.  After each reading, the diamond quantity can be obtained as `global.data[SAVE_DIAMOND_AMOUNT]`.

!> `global.data` can only be used to store numeric type variables, `global.text` can only be used to store string type variables, which can result in storage failure if mixed!

?> The total number of custom variables can be set in `setGlobalsMinor`.

## save player status

In the new engine, `maxJumps`, `maxSpeed`, `grav` of `player` are automatically written to the archive, and the physical state of `player` is more convenient.

| Variable Value         | Status         |
| ---------------------- | -------------- |
| 0 < shootInterval < 10 | Open burst     |
| maxJumps = 0           | Can't jump     |
| maxJumps = 1           | Only a jump    |
| maxJumps = 3           | Three Jumps    |
| maxSpeed ​​> 3         | High speed     |
| 0 < maxSpeed ​​< 3     | Low speed      |
| Grav > 0.4             | Overweight     |
| 0 < grav < 0.4         | Weightlessness |

## safety

When the `global.enable_encryption` configuration item is enabled, the engine encrypts the game's archive file. The key used for encryption can be set via `global.key`.

?> The length of `global.key` must not be less than 40 for greater security.

!> Using archive encryption can make it more difficult to modify game archives, but it cannot completely prevent this problem from occurring.

## Custom Save Script

Under special requirements, you may need to add custom storage variables. This can be modified by the following methods:

1.  In `saveGame`, find the following comment, add a custom variable below the comment and save it;

    ```gml
    // for more save data, add script here
    // If you don't know which buffer_write_* script to use,
    // use buffer_write_float32
    Buffer_write_float32(buffer, global.myVar1)
    Buffer_write_float32(buffer, global.myVar2)
    ```

2.  In `loadGame`, find the following comment, add a custom variable below the comment and read it.

    ```gml
    // for more save data, add script here
    // If you don't know which buffer_read_* script to use,
    // use buffer_read_float32
    global.myVar1 = buffer_read_float32(buffer)
    global.myVar2 = buffer_read_float32(buffer)
    ```

Note that the variables must be stored and read in the same data and order, otherwise the archive system will have a BUG.

!> If you need to save a string, you can't use `buffer_*_float32` and you need to use `buffer_*_string`!

!> You must start a new game \*\* after modifying the archive script and cannot read the file!
