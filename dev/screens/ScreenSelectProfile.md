---
title: ScreenSelectProfile
description: Screen dedicated for selecting profiles
published: true
date: 2025-05-13T06:25:03.390Z
tags: 
editor: markdown
dateCreated: 2025-05-13T06:24:07.936Z
---

ScreenSelectProfile manages selection of profiles for gameplay. Most of the interactions done in this screen are done via Lua, interfaced with some dedicated functions provided by the engine.

# Functions

These functions belong to the [Screen](/en/dev/screens/Screen), so to access them, you'll need to get the [Screen](/en/dev/screens/Screen) object via `SCREENMAN:GetTopScreen()`.

## SetProfileIndex(pn, index)

Sets the profile for the player `pn` with the index `index`.
```lua
-- This will set the first profile available to Player 1.
SCREENMAN:GetTopScreen():SetProfileIndex(PLAYER_1, 0)
```

## GetProfileIndex(pn)

Gets the profile index (`int`) that the current player has.

```lua
local ind = SCREENMAN:GetTopScreen():GetProfileIndex(PLAYER_1)
Trace("Player 1's index is ".. ind)
```

## Finish()

Tells the screen that we're with profile selection, and must start performing load operations. This command can end up as a no-op if certain conditions are met:

- No players have joined.
- Both player's have the same index assigned.
- If a player requested to load from the memory card and it's not available.
- The assigned index is higher than the actual number of profiles.

```lua
SCREENMAN:GetTopScreen():Finish()
```

## Cancel()

Cancels operation and backs out from the screen.
```lua
SCREENMAN:GetTopScreen():Cancel()
```