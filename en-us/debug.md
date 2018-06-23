# debugging function

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

Many built-in debugging features are available in the engine. Just press F6 to compile the game in debug mode to start.

## visible in debugging

In debug mode, you can see almost any object in the map. Including bricks, triggers and so on. If you also need to make your own object visible in debug mode, you can write it in `Create Event`:

`Create Event`:

```gml
If (debug_mode) {
    visible = true
}
```

## Player

`player` also has some new features in debug mode, such as:

- You can use `left mouse button` to send to any place in the room
- You can use the `G key` switch invincible mode
- You can use the `F key` to set the room frame rate (room_speed)
- Archived at any time using `S key`
- You can use the `A key` to move 1 pixel to the left
- You can use the `D key` to move 1 pixel to the right

## Quick Login

In the script `setGlobals`, two sets of quick login user names and passwords are set:

```gml
Global.debug_host_name = 'username'
Global.debug_host_pass = 'password'
Global.debug_guest_name = 'test'
Global.debug_guest_pass = 'test'
```

After changing the above account password to your own registered account password, you can enable the quick login function:

- Press `Shift` to log in using `global.debug_host_name` and use number 1 archive
- Press `Ctrl` to log in using `global.debug_guest_name` and use archive 2
- Press `space` to skip login and start the game
- Use `Shift` to create a room in the lobby and `Ctrl` to join the first room in the room list
- Use `Shift` to start the game in the room

## objDebug

`objDebug` is a simple console that comes with the engine and only works in debug mode. It is used to output all non-zero and non-zero values ​​directly on the screen.

Instructions:

```gml
// The debug script will automatically add spaces between the arguments
debug('I', 'Wanna', 'be', 'the', 'Guy!') // I Wanna be the Guy!
// parameters that may be zero can only be displayed by string concatenation
debug('This is a zero: ' + string(0)) // This is a zero: 0
```

Console startup method:

- After entering the game in F6, press the `End` key.
- Pressing the `Delete` key switches to verbose mode, where `objDebug` lists all network requests it sends or receives;
- After pressing the `Insert` key, the sync information of `player` will be displayed;
- Press the `Home` key to clear the console.
- Press the `PageDown` key to quickly switch languages.
