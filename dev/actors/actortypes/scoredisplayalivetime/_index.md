---
title: ScoreDisplayAliveTime
description: 
published: true
date: 2023-05-20T00:06:04.484Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:49.058Z
---

A [BitmapText](/en/dev/actors/actortypes/bitmaptext/_index) that provides the amount of time the player has survived throughout the current session.

```lua
Def.ScoreDisplayAliveTime{
	PlayerNumber = PLAYER_1,
	MultiPlayer = "MultiPlayer_P1"
}
```

## Attributes

> Only one of the attributes is needed to make the actor function.
{.is-info}

| Name | Type | Action |
| :--- | :--- | :----- |
PlayerNumber | PlayerNumber | The player to obtain its alive time during the session.
MultiPlayer | Multiplayer | The multiplayer to obtain its alive time during the session.

This actor inherits the attributes from [BitmapText](/en/dev/actors/actortypes/bitmaptext/_index#attributes).