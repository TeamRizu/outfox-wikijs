---
title: Stylizing the background
description: A rundown of creating a background layer for a screen, and seeing the loading rules for this layer in particular.
published: true
date: 2025-05-06T03:28:58.051Z
tags: guide, theming
editor: markdown
dateCreated: 2025-05-06T03:28:58.051Z
---

For this example, let's create a background for the same ScreenTitleMenu. So, make a new file called `ScreenTitleMenu background.lua` and input the following:

```lua
return Def.ActorFrame{
	Def.Quad{
  	OnCommand=function(self)
    	self:FullScreen():diffuse(Color.Blue)
    end
  }
}
``` 

Once you save the file, restart the game again (faster reloading methods will be discussed later) and you'll see that now the dark area has been replaced with a blue color.

We've just made our own background layer, very nice. But now try to change the color on it. Try for example: `Color.Green`. Have you noticed something? Maybe that the color isn't updating?

This is because the background is special, where it is always running as long as the screen is correspondant to the screen is defined in, so, as long as you're in ScreenTitleMenu, no matter how many times you reload it, it will run the same background from where it was. This is done to make seamless playback while switching screens.

But what if you want to see the changes? Well, this is where we're going to introduce our first helper: The creator menu!

You can open this menu by holding the F2 key. This will bring up an overlay with options on the top of the screen.