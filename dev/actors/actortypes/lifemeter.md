---
title: LifeMeter
description: 
published: true
date: 2026-05-03T18:10:33.899Z
tags: 
editor: markdown
dateCreated: 2023-11-04T06:30:08.753Z
---

The LifeMeter is an [ActorFrame](/en/dev/actors/actortypes/actorframe) that provides a few functions to determine the current state of the player's health.

# Functions

The way LifeMeter returns the value for the functions is based on the player's current **Life Type**, which can be one of the following three:

- Bar: The standard life meter which fills up from 0 to 1.
- Battery: A more limited life meter with a set number of lives. Any time the player gets a miss or hits a note poorly will be penalized.
- Time: A more dynamic version of the Life meter commonly seen in Survival, where the meter is constantly draining with the passage of time, and the player can replenish it by playing accurately.

> For the following function examples, we're using `ScreenGameplay`, as that has a `GetLifeMeter` function to obtain this object.
> `ScreenHowToPlay` is the only other screen that has this function call as well.
{.is-info}

## `GetLife`

Returns the current life of the player.

```lua
-- For this example, we're going to grab the player's current health.
local health = SCREENMAN:GetTopScreen():GetLifeMeter(PLAYER_1):GetLife()
```

|Life Type| Return Type|
|---|---|
| Bar | Returns a value from 0 to 1.
| Battery | Returns a converted 0 to 1 float value of `Batteries Left / Max Batteries`.
| Time | Return a converted 0 to 1 float value from `Time Left / 90`. The `90` is hard-coded as it was meant for ITG Survival.

## `IsInDanger`

Returns `true` if the player is in a danger situation. For all three life types, this is determined by a `DangerThreshold` metric.

```lua
local indanger = SCREENMAN:GetTopScreen():GetLifeMeter(PLAYER_1):IsInDanger()
```

## `IsHot`

Returns `true` if the player is `Hot`. This means that the player currently has max health. This applies for **Bar** and **Battery**.

```lua
local ishot = SCREENMAN:GetTopScreen():GetLifeMeter(PLAYER_1):IsHot()
```

> The **Time** life type will never return true, despite reaching its max time.
{.is-warning}

## `IsFailing`

```lua
local isFailing = SCREENMAN:GetTopScreen():GetLifeMeter(PLAYER_1):IsFailing()
```

|Life Type|Return Type|
|---|---|
| Bar | Linked to the `Passmark` modifier, it will return `true` if the player's current life is under the value of `Passmark`. |
| Battery | Returns `true` if the player has run out of batteries. |
| Time | Returns `true` if the player has run out of time. |
