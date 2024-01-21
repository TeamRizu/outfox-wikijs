---
title: ControllerStateDisplay
description: 
published: true
date: 2024-01-21T22:26:42.107Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:42.391Z
---

Creates an [ActorFrame](/en/dev/actors/actortypes/actorframe) that contains button sprites for a specific game mode to indicate their pressed state. A more visual version of Test Input.

> The class only detects input from MultiPlayer players. These are a different kind of player that are exclusively on controllers.
{.is-info}

> The ControllerStateDisplay only detects pump buttons. [It has been like this since July, 2007](https://github.com/stepmania/stepmania/commit/42c69f8bc8ae85df56591b274eebd969600c34b9).
{.is-warning}

```lua
Def.ControllerStateDisplay{
}
```

## Attributes

There are no special attributes to this actor class. It inherits from [ActorFrame](/en/dev/actors/actortypes/actorframe).

## Loaded Graphics

When running either [`LoadMultiPlayer`](#loadmultiplayer) or [`LoadGameController`](#loadgamecontroller), the following textures are loaded.

`sType` in this context is the Type provided as the first argument on both functions.

- `[sType] frame`: The background frame for the buttons
- `[sType] [ControllerState]`: A [Sprite](/en/dev/actors/actortypes/sprite/_index) that represents the button.

## Functions

### `LoadGameController`
`(string type, GameController gc)`

Loads a GameController to be used on the ControllerStateDisplay. It is automatically given a MultiPlayer of `MultiPlayer_Invalid`.

> You can theoretically use this function to have functionality on a regular controller / player, given those also use GameController.
{.is-info}

### `LoadMultiPlayer`
`(string type, MultiPlayer mp)`

Loads a MultiPlayer `mp` to detect its input. Calling this function will make the ControllerStateDisplay use a controller of `GameController_1`.
