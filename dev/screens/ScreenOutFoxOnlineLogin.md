---
title: Outfox Online Login Screen
description: Login screen for Outfox Online
published: true
date: 2025-09-12T20:49:44.561Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-31T02:33:08.747Z
---

# ScreenOutfoxOnlineLogin
This screen takes care of loading online profiles, processing link token requests, invalid tokens, duplicates, and many other elements.

![oftokencyberia.png](/dev/outfoxonline/oftokencyberia.png)
<small>Theme is [CyberiaStyle: LAST APPROACH](https://josevarela.net/SMArchive/Themes/ThemePreview.php?Category=StepMania%205&ID=CS8LA), by gl_yukt.</small>

# Workflow

If no profiles are loaded at all, if the machine has the `AllowGuestProfiles` option enabled from [ScreenOptionsNetwork](/dev/screens/ScreenOptionsNetwork), each user will be prompted for a 4-digit Link code, which they can access from their Outfox Online dashboard. They can also use an NFC card that contains the token code for their profile to sign in as well.

If a user has a profile that is locally stored on the machine, the game will automatically attempt to login with their provided token. If this process fails, they'll be prompted with the same 4-digit screen as if there was no profile, where the difference is that upon successful sync, it updates the profile's token with the correct one for future logins.

# Functions

These functions belong to the [Screen](/en/dev/screens/Screen), so to access them, you'll need to get the [Screen](/en/dev/screens/Screen) object via `SCREENMAN:GetTopScreen()`.

## EnterDigit(player, digit)

Adds a `digit` to the `player`'s current guest code entry.

```lua
-- Adds 4 to Player 1's current guest code.
SCREENMAN:GetTopScreen():EnterDigit(PLAYER_1, 4)
```

Once all 4 digits have been entered, the engine will automatically clear the code.

## SkipProcess(player)

Tells the screen that this `player` wants to skip the login process.

```lua
-- This will tell the game that Player 1 will skip.
SCREENMAN:GetTopScreen():SkipProcess(PLAYER_1)
```

## NeedsTyping(player)

Returns true if the `player` needs to insert their guest code.
```lua
local need = SCREENMAN:GetTopScreen():NeedsTyping(PLAYER_1)
if need then
	Trace("Hey, type something!")
end
```

# Receiving commands

Depending on which action is taken by the user or response received by the client, a command gets called.

## SendingLinkCodeCommand

Sent when the player has sent their 4-digit link code, and is in the process of logging in.

The following parameters are sent along with the command:

| - | - |
| Name | Value | Description
| Player | PlayerNumber | Player the message belongs to.


## PlayerLoginFailCommand

Sent when a login attempt for the player has failed.

The following parameters are sent with the command:

| - | - |
| Name | Value | Description
| Player | PlayerNumber | Player the message belongs to.
| Reason | String | Reason for failure.
| NeedsLinkCode | bool | If the player needs to reinsert their Link Code, this will return true.

## PlayerLoginSuccessCommand

Sent when a login attempt for the player has succeeded.

The following parameters are sent along with the command:

| - | - |
| Name | Value | Description
| Player | PlayerNumber | Player the message belongs to.

## TokenCodeChangedCommand

Sent when a player has entered a new digit for the Guest code. The actual code isn't sent on this message, as the engine takes care of keeping track. Think of this message more for updating the visual elements that compose your pin keyboard.

The following parameters are sent along with the command:

| - | - |
| Name | Value | Description
| Player | PlayerNumber | Player the message belongs to.
| Length | int | The current length of the code. Max is 4.