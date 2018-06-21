# Automatically change spike sprites

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

In the game, you often need the spikes of many different sprites, and this is a very tedious job. When you want to use it in a room, you need to find different sprites' stings in different folders, which further reduces the efficiency of creation.

In the engine, you can define the style of stabbing in each room. After the success is defined, the engine will automatically replace eight common spears, spikeUp, spikeDown, spikeLeft, spikeRight, minispikeUp, minispikeDown, minispikeLeft, and minispikeRight.

This function can be set in the script `Scripts -> functions -> autoSpikeSprite`.

In line 8 of the `autoSpikeSprite` script, copy the sample to add the script:

```gml
case myRoom:
    spikeSprite(mySpike, myMiniSpike, myImageSpeed);
    break;
```

- `mySpike` is the sprite used for normal spikes, size is `32 * 32`, the direction of the spike is up, the origin of the sprite needs to be in the center of the image (see `sprSpikeM`)
- `myMiniSpike` is the sprite used for the small spine, `16 * 16`, the direction of the spike is up, and the origin of the sprite needs to be in the center of the image (see `sprMiniSpikeM`). If the item is omitted or is 0, it will use the normal spike. The sprite and shrunk to half of original as a spit sprite.
- `myImageSpeed` When the sprite is dynamic, you can specify the `image_speed` value of the sting used. If a stinging sprite has only a single frame, it can be ignored.

After the setting is completed, the eight common stings of `spikeUp, spikeDown, spikeLeft, spikeRight, minispikeUp, minispikeDown, minispikeLeft, and minispikeRight` can be placed and designed in each room, and they will automatically be in the designated room. Replaced with the sprite specified in the script.

!> When using `Creation Code` to add `path_start` to the spine to make it expand (or other path), it will make path not work properly. You can use [pathSpike](objectref?id=pathspike) instead.
