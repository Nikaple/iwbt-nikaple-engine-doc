# Creation Code Introduction

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

## How to use Creation Code

In the engine, there is a large number of generic objects, which are differentiated by Creation Code placed after the room. The specific use method is:

1.  Open the room editor and place the object in the room

2.  According to the GameMaker version, adding Creation Code is different

- GameMaker 8.0: `Ctrl + Right -> Creation Code...`
      - GameMaker 8.1:`Right click -> Creation Code...`

## Creation Code Specification in the Fruit Engine

There are many common codes in Creation Code. Remember that they will help you to use the engine faster and better. They are categorized as follows:

```gml
--------------- General ---------------
     spr = Sprite to be replaced (sprite_index)
     ind = sprite number (image_index)
    ispd = sprite playback speed (image_speed)
      xs = horizontal zoom (image_xscale)
      ys = vertical zoom (image_yscale)
     yrg = Trigger number
       h = trigger lateral velocity
       v = trigger vertical speed
     spd = trigger speed
     dir = trigger direction
  origin = rotation/zoom center
    time = time (in frames)
     num = number (boss number, item number, etc.)
   noDes = Do not destroy after leaving the room (default is to destroy directly after leaving the room)
  noSync = is not synchronized (default sync)
     dis = the distance to move before leaving the room (default is 0)

------------- Path related -------------
     pth = path number
     spd = speed
    enda = end of path event (reference constant table)
     scl = path magnification
    move = whether to prevent spoilers (the player will move in the current direction after death, not stop/turn)

------------- Warp related -------------
  roomTo = target room
     num = target playerStart num
    mode = warp mode ('normal' or 'border', default = 'normal')
    kind = transition effect (optional)
    text = text above warp (optional)
   color = text color above warp (optional)
```
