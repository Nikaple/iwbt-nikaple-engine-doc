# Online introduction

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

In order to customize the online effect in the game, you first need to have a basic concept of the online game's operating mechanism.

## Disable

In the script `setGlobals`, set `global.game_mode = MODE_SINGLE_PLAYER`. (enabled by default)

## Server

The server is the medium of communication between the client and the client. Without the support of the server, the game created using the nikaple engine can only be run in stand-alone mode. The server-side code [iw-nikaple-server](https://github.com/Nikaple/iw-nikaple-server) is written using [Node.js](https://nodejs.org), based on [ Patchwire](https://www.npmjs.com/package/patchwire) The magic comes from, in the absence of special needs, generally do not need to modify.

The engine provides developers with a default IP address (139.\*.\*.59, see the engine's `setGlobals` script) for testing purposes only. It is best to change the IP address to the IP of your own server when you publish the game to increase the stability of the game server.

## client

The basic engine part of the client is based on [I wanna be the Engine Yuuutu Edition](https://www.delicious-fruit.com/ratings/game_details.php?id=10483) (~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ ), The network communication part is a highly customized patchwire package [GM:S Engine](https://github.com/gm-core/patchwire-gm). The Dll plug-ins used include:

- [Http Dll 2.3](http://www.maartenbaert.be/game-maker-dlls/http-dll-2/) for network communication
- [Super Sound System](http://gmc.yoyogames.com/index.php?showtopic=120034) for music playback
- [FoxWriting](https://www.noisyfox.io/fox-writing-gamemaker.html) for multilingual support
- [CleanMem](http://gmc.yoyogames.com/index.php?showtopic=438215) Used to free extra memory

## Protocol

The communication protocol between server and client is mainly divided into two types: TCP and UDP. Their characteristics are as follows:

- TCP: stable but relatively inefficient
- UDP: Unstable, relatively high packet loss rate, but high efficiency

Based on the above characteristics, you need to select different protocols for different data to transmit:

- Users log in, create rooms, shoot archives, reset games, and other functions. Because of their small amount of data (usually only sent once the data can be), in order to ensure its stability using the TCP protocol transmission.
- Synchronization of player position, positional synchronization of pushable boxes, etc. Because of the large amount of data (almost every frame will transmit data), but the stability requirements are not high (the latter data will naturally cover the front, so even if the loss is also Will return to normal soon) using UDP protocol transmission.

## Transfer data using TCP protocol

In the engine, there are three preset TCP transmission modes that can meet most of the requirements. they are, respectively:

- [Instance instance mode] (/network?id=instance-instance mode) for synchronous static placement in a room with instances of the same `id`.

- [Event event mode] (/network?id=event-event mode), used to synchronize arbitrary information at any point in time in any instance.

- [Wait wait mode] (/network?id=wait-wait mode) Used to synchronize events that require all clients to trigger at the same time.

?> Note that due to the limitation of the engine, the synchronization script `ns_send_*` can only be written in ** other events except Create, Begin Step, End Step, Draw**. If it is really necessary to call the synchronization script in these events, set alarm[i] = 1 in the place where synchronization is needed and send the synchronization request in the event of Alarm i (i = 0 ~ 11).

?> For the internals of these three modes, refer to [script documentation](scriptref?id=ns_send)

In addition, in these three modes, the scope of the message receiver can be controlled by specifying the `scope` parameter in the synchronization information (key-value pair).

The value of `scope` can be:

- The default range of `SCOPE_DEFAULT`, sent to other players in the same room (don't fill it)
- `SCOPE_OTHERS` sent to other players (whether in the same room or not)
- `SCOPE_ALL` sent to everyone (including yourself)

E.g:

```gml
// Send a `hello` event to all other players, including a familiar name
ns_send_event(
    'hello', 1,
    'name', 'crazy_tiger',
    'scope', SCOPE_OTHERS
)
```

### Instance instance pattern

This pattern uses the script `ns_send_instance` declaration to synchronize `object`with the same`id`.

The script receives any number of parameters, but the following conditions must be met:

- The first parameter is the number of required synchronization information (key-value pairs) n;
- The next 2n parameters are of the form key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub>'s key-value pairs, represent information that needs to be synchronized.

Note that this script can only be used to synchronize directly placed in the room, fixed `id`ofobject. (Theobjectcreated with`instance_create` is invalid, an error will be reported)

?> When no data need to be synchronized, parameters can be omitted.

The following uses blockMove as an example to illustrate the application of the Instance instance pattern.

When `player` stands on `blockMove`, `blockMove` will start moving in the set direction. Among them, horizontal speed is `h` and vertical speed is `v`. Therefore, at the moment you determine the `player` station, you need to synchronize the status of the bricks to other clients.

`Create Event`:

```gml
// Set the data synchronization status to not synchronized
sent = false
```

`Step Event`:

```gml
// Check if the player is standing on a brick, slightly
isPlayerOnBlock = ...
// Send data only when the player is standing on the brick and the synchronization status is not synchronized,
// If you do not use the sent variable, data is sent every frame, resulting in a large network overhead
If (isPlayerOnBlock && !sent) {
    // Set the horizontal speed
    hspeed = h
    // Set the vertical speed
    vspeed = v
    // Sync 2 properties,
    // The first property is named 'h' and the value is the current horizontal speed.
    // The second property is named 'v' and the value is the current portrait speed
    ns_send_instance(
        2,
        'h', hspeed,
        'v', vspeed
    )
    // Set the data synchronization status to synchronized
    sent = true
}
```

Afterwards, this information will be directly synchronized to other client's `Other -> User defined -> User 15` event. You only need to process the data in it:

`User Defined 15`:

```gml
// At this time, h, v have been set to the horizontal and vertical speeds that need to be synchronized,
// You need to use them to handle the current instance.
hspeed = h
vspeed = v
```

This completes the synchronization of the speed of the instance in different clients. This mode is also the most widely used mode.

### Event Event Mode

This pattern uses the script `ns_send_event` declaration to synchronize arbitrary information in any object at any point in time.

The script receives any number of parameters, but the following conditions must be met:

- The first parameter is the name of the event (will be used later);
- The second parameter is the number of synchronization information (key-value pairs) in the event n;
- The next 2n parameters are of the form key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub>'s key-value pairs, represent information that needs to be synchronized.

Using `savePointSync` as an example, when a client's `player` is saved with this archive, all other players can move to the archive by resetting the game (that is, pressing R ). Since the player may be in a different room when archiving, it is not suitable to use the Instance method to synchronize.

`Step Event`:

```gml
// Check if the file is saved successfully.
isSaveSuccess = ...
If (isSaveSuccess) {
     // sync three attributes,
     // The first property is named 'id' and the value is the `id` of the current archive point.
     // The second property is named 'x' and the value is the xprevious of player in the previous frame.
     // The second property is named 'y' and the value is the y-coordinate of the player in the previous frame (yprevious).
     // The coordinates of the previous frame are used here to prevent card wall bugs.
    ns_send_event(
        'save_sync', 3,
        'id', id,
        'x', player.xprevious
        'y', player.yprevious
    )
}
```

This information is then immediately synchronized to other client `handler_event_{NAME}` scripts, where `{NAME}` is the name of the event you just sent.

Therefore, a new script, named `handler_event_save_sync`, can start receiving `save_sync` events sent from other clients.

This type of script receives two parameters: the first argument is the name of the player who sent the event, and the second argument is a `ds_map`, which holds all the synchronized data:

```gml
// handler_event_save_sync(fromName, data)

// All used variables must be declared with var, otherwise unpredictable errors may occur!
Var fromName, data, _id, _x, _y;
fromName = argument0
data = argument1
// json_pick is exactly the same as ds_map_find_value, but it is shorter and better
// Pick the data named 'id' from data
_id = json_pick(data, 'id')
// Pick the data named 'x' from data
_x = json_pick(data, 'x')
// Pick the data named 'y' from data
_y = json_pick(data, 'y')
// Now 'id', 'x', 'y' synced with other clients are stored in _id, _x, _y.
// It's okay to use this data to achieve archive synchronization.

// No data processing is required after the data is acquired, and the engine automatically releases the memory it occupies.
```

This completes the synchronization of any data at any point in time in any object. When considering the need for `ns_send_instance`, consider this.

### Wait Waiting Mode

This pattern uses the script `ns_send_wait` declaration for events that occur after all players have triggered an event (for example, `warp`, which is passed after all players enter).

When using this event, you need to pass in tag information (default is the current instance's `id`).

?> If you have more than one `warp` but send to the same room, you can set the tag information to the room number (`r`) that you want to transfer, so that the server will use this flag information to perform on each client. mark.

The script receives any number of arguments and satisfies the following conditions:

- The first parameter is the name of the waiting event (will be used later);
- The second parameter is the tag information of the event;
- The third parameter is the number of synchronization information (key-value pairs) in the wait event; n;
- The next 2n parameters are of the form key<sub>1</sub>, value<sub>1</sub>, key<sub>2</sub>, value<sub>2</sub>, ..., key<sub>n</sub>, value<sub>n</sub>'s key-value pair.

If the `fin` entry in the returned data is 1, it means that all clients have triggered the event.

Taking the `reset` wait event as an example, this wait event is used to set the current room's attribute to "if and only if all players choose to reset, the room will be reset."
Step Event:

```gml
// Determine if the current room needs to wait for reset
shouldResetWait = ...
If (shouldResetWait) {
    // Send a wait event named `reset`
    ns_send_wait('reset', room)
}
```

This information is then immediately synchronized to other client `handler_wait_{NAME}` scripts, where `{NAME}` is the name of the wait event you just sent.

Therefore, create a new script named `handler_wait_reset` to start receiving `reset` wait events sent from other clients.

This type of script receives three parameters:

- The first parameter is the name of the player who sent the event;
- The second parameter is a `ds_map`, which holds all the synchronized data;
- The third parameter indicates whether all clients have triggered the event

```gml
// handler_wait_reset(fromName, data, isFinished)

// All used variables must be declared with var, otherwise unpredictable errors may occur!
Var fromName, data, isFinished;
fromName = argument0
data = argument1
isFinished = argument2

If (isFinished) {
    // Process a reset success event and reset the current game
} Else {
    // Handle the reset failed event, perhaps give some hints to the current player?
}
```

## Use UDP protocol to transmit data

### You may not need UDP mode

Using UDP protocol to synchronize data is very costly for the network. Please use it carefully and try not to use it where possible.

For example, the motion state of `blockMove` can be determined instantaneously on the `player` station, so you only need to use TCP to synchronize once, and you don't need to synchronize the position information anytime anywhere. The application scenario of the UDP mode is mainly the `object`that interacts with`player`, for example, to push the brick (refer to` UserPass``User Defined 0 `and`User Defined 14`).

In addition, before using this pattern you need to have some basic understanding of buffer `buffer` and basic data types. For a description of the `buffer` read-write function and data type, refer to the `Documentation of`Http Dll 2.3` (http://www.maartenbaert.be/game-maker-dlls/http-dll-2/buffers/).

### Using UDP to Synchronize

The way to use UDP mode for synchronization is also very simple. Here's a simple explanation using `blockPush` as an example:

`Step Event`:

```gml
// Determine if you need to synchronize location information
shouldSyncPosition = ...
If (shouldSyncPosition) {
    // Start UDP synchronization, this script will return a buffer for you to write
    buffer = ns_sync_begin()
    // Write the current x coordinate, type int16 (that is, short, range: integer of -32768~32767)
    Buffer_write_int16(buffer, x)
    // Write the current y coordinate, type int16 (that is, short, range: integer of -32768~32767)
    Buffer_write_int16(buffer, y)
    // Write the current horizontal velocity, type int8 (that is, byte, range: integer from -128 to 127)
    Buffer_write_int8(buffer, hspeed * 10)
}
```

Then, after a series of processing by the server and `objClient`, the`buffer`with the same content will be directly synchronized to the`Other -> User defined -> User 14`event of the same instance of the other client. You only need to Read`buffer` and handle it in the event.

`User Defined 14`:

```gml
// Before this event occurs, the buffer variable is assigned to the server's buffer

// Read the x coordinate that needs to be synchronized
x = buffer_read_int16(buffer)
// read the y coordinate that needs to be synchronized
y = buffer_read_int16(buffer)
// Read the horizontal speed that needs to be synchronized
hspeed = buffer_read_int8(buffer) / 10
```
