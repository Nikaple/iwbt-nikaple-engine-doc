# 常量

引擎中提供了许多常量以增强代码可读性。

### 游戏模式

| 常量名             | 常量值 | 说明         |
| ------------------ | ------ | ------------ |
| MODE_TOURNAMENT    | 1      | 强制竞技模式 |
| MODE_COOPERATION   | 2      | 强制合作模式 |
| MODE_USER_SELECT   | 3      | 玩家自选模式 |
| MODE_SINGLE_PLAYER | 4      | 仅单人模式   |

## 语言

| 常量名  | 常量值 | 说明 |
| ------- | ------ | ---- |
| LANG_CN | 1      | 中文 |
| LANG_EN | 2      | 英文 |
| LANG_JP | 3      | 日文 |

## player 状态

| 常量名  | 常量值 | 说明                      |
| ------- | ------ | ------------------------- |
| IDLING  | 0      | player 空闲               |
| RUNNING | 1      | player 移动               |
| FALLING | 2      | player 下落               |
| JUMPING | 3      | player 跳跃               |
| SLIDING | 4      | player 藤蔓滑动           |
| LADDER  | 5      | player 爬梯（暂无该功能） |

## 存档模式

| 常量名          | 常量值 | 说明     |
| --------------- | ------ | -------- |
| SAVE_MODE_SHOOT | 0      | 射击存档 |
| SAVE_MODE_TOUCH | 1      | 触碰存档 |
| SAVE_MODE_PRESS | 2      | 按键存档 |

## 路径结束动作

| 常量名                            | 常量值 | 说明                     |
| --------------------------------- | ------ | ------------------------ |
| PATH_ACTION_STOP                  | 0      | 路径结束后直接停止       |
| PATH_ACTION_CONTINUE_FROM_START   | 1      | 路径结束后返回起点继续   |
| PATH_ACTION_CONTINUE_FROM_CURRENT | 2      | 路径结束后从当前位置继续 |
| PATH_ACTION_REVERSE               | 3      | 路径结束后反转路径       |

## 难度

| 常量名         | 常量值 | 说明       |
| -------------- | ------ | ---------- |
| DIF_LOAD       | 0      | 读取       |
| DIF_MEDIUM     | 1      | Medium     |
| DIF_HARD       | 2      | Hard       |
| DIF_VERYHARD   | 3      | VeryHard   |
| DIF_IMPOSSIBLE | 4      | Impossible |

## 网络连接

### 事件传播范围

| 常量名        | 常量值 | 说明                   |
| ------------- | ------ | ---------------------- |
| SCOPE_DEFAULT | 0      | 发送给同房间的其他玩家 |
| SCOPE_OTHERS  | 1      | 发送给所有其他玩家     |
| SCOPE_ALL     | 2      | 发送给所有玩家         |

### UDP 同步类型

| 常量名            | 常量值 | 说明         |
| ----------------- | ------ | ------------ |
| UDP_SYNC_PLAYER   | 1      | 同步玩家状态 |
| UDP_SYNC_INSTANCE | 2      | 同步实例状态 |

## 自定义事件

在创作过程中请不要使用 13、14、15 号用户自定义事件，以免出现 BUG。

| 常量名        | 常量值 | 说明         |
| ------------- | ------ | ------------ |
| EVENT_TRIGGER | 13     | 触发事件     |
| EVENT_UDP     | 14     | UDP 同步事件 |
| EVENT_TCP     | 15     | TCP 同步事件 |
