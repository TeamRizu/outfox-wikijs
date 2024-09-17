---
title: Online Overlay
description: The in-game overlay for OutFox Online that displays on top of every theme.
published: false
date: 2024-08-31T02:02:32.629Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-29T20:26:37.605Z
---

# Online Overlay

The online overlay runs on [ScreenSystemLayer](/en/dev/screens/ScreenSystemLayer), and its the second layer running just inbetween the overlay and error layers.

The full name for this file is called: `ScreenSystemLayer ofonline.lua`, and is present on the BGAnimations folder.

By default it sits dormant on each side of the screen for each player, and upon receiveing notifications, it runs a command to determine what to report back to the players.

![ofonlineoverlayconnectd.png](/dev/outfoxonline/ofonlineoverlayconnectd.png){.align-center}

The command received is a MessageCommand called `MessageOFNetworkResponse`. In this message, the following parameters are present:

| Title | Type | Description |
| --- | --- | --- |
Name | String | The name of the command that it just receieved.
PlayerNumber | PlayerNumber | The player this command belongs to.
Status | String | Depending on the command, this variable can return a `success` or `error` based on the output of the response.
Message | String | An optional variable which outputs a reason, normally present alongside an error status.

> As it is a MessageCommand, other actors can be used outside of the overlay to report the same messages.
> 
> Feel free to modify this overlay for your theme, or even disable it completely and implement the same messages in different ways.
{.is-info}


## Message Example

```lua
MessageOFNetworkResponseMessageCommand=function(self,params)
	if params.PlayerNumber == plr then
		local xPosSeparation = SAFE_WIDTH + 140
		self:x( plr == PLAYER_1 and xPosSeparation or SCREEN_WIDTH - xPosSeparation)
		if params.Name == "ScoreSave" then
			if params.Status == "success" then
				self:GetChild("Status"):settext("Score Submitted!")
			else
				self:GetChild("Status"):settext("Error: ".. params.Message )
			end
			self:playcommand("ActionPlay")
		end
		if params.Name == "ProfileSave" then
			self:GetChild("Status"):settext("Profile Synced!")
			self:playcommand("ActionPlay")
		end
		self:GetChild("RemainingTime"):diffusealpha(1):cropright(0):linear(2.8):cropright(1):sleep(0):diffusealpha(0)
	end
	if params.Name == "MachineLogin" then
		self:x(SCREEN_CENTER_X)
		self:GetChild("Status"):settext("Connected to OutFox Online.")
		self:playcommand("ActionPlay")
	end
end,
```