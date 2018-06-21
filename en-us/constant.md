# constant

!> This page is translated by Google Translate, Click **Edit Document** on the top left corner if you want to help the project out!

Many constants are provided in the engine to enhance code readability.

## language

| Constant Name | Constant Value | Description |
| ------------- | -------------- | ----------- |
| LANG_CN       | 1              | Chinese     |
| LANG_EN       | 2              | English     |
| LANG_JP       | 3              | Japanese    |

## player Status

| Constant Name | Constant Value | Description                   |
| ------------- | -------------- | ----------------------------- |
| IDLING        | 0              | player Free                   |
| RUNNING       | 1              | player Mobile                 |
| FALLING       | 2              | player Fall                   |
| JUMPING       | 3              | player Jump                   |
| SLIDING       | 4              | player Vine Sliding           |
| LADDER        | 5              | player Ladder (Not Available) |

## Internet connection

### Event propagation scope

| Constant Name | Constant Value | Description                            |
| ------------- | -------------- | -------------------------------------- |
| SCOPE_DEFAULT | 0              | Send to other players in the same room |
| SCOPE_OTHERS  | 1              | Send to all other players              |
| SCOPE_ALL     | 2              | Send to all players                    |

### UDP synchronization type

| Constant Name     | Constant Value | Description                |
| ----------------- | -------------- | -------------------------- |
| UDP_SYNC_PLAYER   | 1              | Synchronized Player Status |
| UDP_SYNC_INSTANCE | 2              | Sync Instance Status       |

## custom events

Do not use user-defined events 13, 14 and 15 during the creation process to avoid BUG.

| Constant Name | Constant Value | Description                |
| ------------- | -------------- | -------------------------- |
| EVENT_TRIGGER | 13             | Triggering Events          |
| EVENT_UDP     | 14             | UDP Synchronization Events |
| EVENT_TCP     | 15             | TCP Synchronization Events |

## End of the path

| Constant Name                     | Constant Value | Description                                        |
| --------------------------------- | -------------- | -------------------------------------------------- |
| PATH_ACTION_STOP                  | 0              | Stop directly after the path ends                  |
| PATH_ACTION_CONTINUE_FROM_START   | 1              | Return to Start After Path Ends                    |
| PATH_ACTION_CONTINUE_FROM_CURRENT | 2              | Continuation from current location after path ends |
| PATH_ACTION_REVERSE               | 3              | Reverse Path After Path                            |
