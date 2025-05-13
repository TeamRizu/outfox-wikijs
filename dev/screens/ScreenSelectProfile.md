---
title: ScreenSelectProfile
description: Screen dedicated for selecting profiles
published: true
date: 2025-05-13T06:32:47.620Z
tags: 
editor: markdown
dateCreated: 2025-05-13T06:24:07.936Z
---

ScreenSelectProfile manages selection of profiles for gameplay. Most of the interactions done in this screen are done via Lua, interfaced with some dedicated functions provided by the engine.

![screen-demo.png](/dev/screens/screenselectprofiles/screen-demo.png)

<small>The ScreenSelectProfile screen from Soundwaves.</small>

# Available Metrics

The following are the metrics that this screen uses (from `_fallback`):
```ini
Fallback="ScreenWithMenuElements"
Class="ScreenSelectProfile"
LoginScreenName="ScreenOutFoxOnlineLoginFromSelect"
#
ScreenOnCommand=%function(self) self:lockinput(1); end;
#
NextScreen=Branch.AfterSelectProfile()
PrevScreen=Branch.TitleMenu()
StartScreen=Branch.AfterSelectProfile()
#
TimerSeconds=30
LockInputSecs=0.35
#
CodeNames=SelectProfileKeys()
CodeUp="+MenuUp"
CodeUp2="+Up"
CodeUp3="+MenuLeft"
CodeUp4="+Left"
CodeDown="+MenuDown"
CodeDown2="+Down"
CodeDown3="+MenuRight"
CodeDown4="+Right"
CodeStart="+Start"
CodeBack="Back"
CodeCenter="Center"
CodeDownLeft="DownLeft"
CodeDownRight="DownRight"
```

# OutFox Online Interoperability

If the client is connected to [OutFox Online](/en/dev/outfoxonline), upon making a selection and calling `Finish()`, the engine will verify if the selected profiles are eligible for automatic login.

If a selected profile is not eligible (a.k.a they don't have a token assigned to them), if they have the "Allow Guest Profiles" option enabled on [ScreenNetworkOptions](/en/dev/screens/ScreenNetworkOptions), the game will automatically overwrite the NextScreen to the value of `LoginScreenName`.

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