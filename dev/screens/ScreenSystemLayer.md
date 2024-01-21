---
title: ScreenSystemLayer
description: 
published: true
date: 2024-01-21T23:21:30.811Z
tags: 
editor: markdown
dateCreated: 2024-01-21T23:21:30.811Z
---

> Depends on [Screen](/en/dev/screens/Screen).
{.is-info}

This is an overlay that is responsible for displaying the credit information for each player and system messages that are received from `SCREENMAN:SystemMessage` function.

![screensystemlayer-scr.png](/dev/screens/screensystemlayer/screensystemlayer-scr.png)

# Customizing

The entire screen runs under an ActorFrame, so all interactions can be controlled via Lua, allowing you to add any kind of actor to this screen.

> As this is an overlay screen, it will always be shown on top of every other screen in the game.
{.is-warning}

## Receiving system messages

System messages from the `SCREENMAN:SystemMessage` function are sent via a command called `SystemMessageMessageCommand`, where its contents are stored in a variable called `Message` in the parameter.

```lua
SystemMessageMessageCommand = function(self, params)
		self:GetChild("Text"):settext( params.Message );
end
```

An additional parameter called `NoAnimate` may be provided, which should be used to not animate the SystemMessage display.

```lua
if params.NoAnimate then
		self:finishtweening();
end
```

## Credits Display

Credits actors are by default drawn as [BitmapText](/en/dev/actors/actortypes/bitmaptext) actors, which run a function defined in the same file for the screen called `CreditsText`.

```lua
local function CreditsText( pn )
	local text = LoadFont(Var "LoadingScreen","credits") .. {
		InitCommand=function(self)
			self:name("Credits" .. PlayerNumberToString(pn))
			ActorUtil.LoadAllCommandsAndSetXY(self,Var "LoadingScreen");
		end;
		UpdateTextCommand=function(self)
			local str = ScreenSystemLayerHelpers.GetCreditsMessage(pn);
			self:settext(str);
		end;
		UpdateVisibleCommand=function(self)
			local screen = SCREENMAN:GetTopScreen();
			local bShow = true;
			if screen then
				local sClass = screen:GetName();
				bShow = THEME:GetMetric( sClass, "ShowCreditDisplay" );
			end

			self:visible( bShow );
		end
	};
	return text;
end;
```

To obtain information about the current status of the player in the credits display, you need to use the `GetCreditsMessage` function inside of the `ScreenSystemLayerHelpers` namespace, which requires a player for argument.

# Error display

Alongside the screen, this screen also loads a layer called `error`. The entire purpose for this layer is to run a special actor type called [Def.LogDisplay](), which is responsible for outputting Lua errors during runtime.

![screensystemlayer-errorview.png](/dev/screens/screensystemlayer/screensystemlayer-errorview.png)

> While created in Lua, this is a layer that should **NOT be edited**. This actor is essential for debugging information and adding this to a theme won't provide any improvements in error reporting.
{.is-danger}