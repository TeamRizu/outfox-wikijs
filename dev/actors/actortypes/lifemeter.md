---
title: LifeMeter
description: 
published: true
date: 2023-11-04T06:32:43.283Z
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

## `GetLife`

Returns the current life of the player.

### Bar

Returns a value from 0 to 1.

### Battery

Returns a converted value from the current lifes left and the starting ammount of batteries.

```
Lives Left / Batteries Max
```

### Time

Retuns a converted value from the current time remaining against a hard-coded value of 90. This value is clamped to return a value from 0 to 1.

```
Time Left / 90.
```

## `IsInDanger`

Returns `true` if the player is in a danger situation. For all three life types, this is determined by a `DangerThreshold` metric.

## `IsHot`

Returns `true` if the player is `Hot`. This means that the player currently has max health. This applies for **Bar** and **Battery**.

> The **Time** life type will never return true, despite reaching its max time.
{.is-warning}

## `IsFailing`

### Using Bar

Linked to the `Passmark` modifier, it will return `true` if the player's current life is under the value of `Passmark`.

### Using Battery

Returns `true` if the player has run out of batteries.

### Using Time

Returns `true` if the player has run out of time.