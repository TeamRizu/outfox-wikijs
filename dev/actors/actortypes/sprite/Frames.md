---
title: Managing Frames
description: 
published: true
date: 2023-11-04T05:11:28.560Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:16:11.168Z
---

The frames in a sprite are composed of an array containing arrays of two values, **Frame** and **Delay**. These describe what frame in a spritesheet the actor should focus on and for how long in seconds.

> Sprites that use a video file do not apply for this guide, as the sprite only recognizes it as a single frame, given it's now using FFMpeg to handle playback of said video. For this, you'll need to obtain the Sprite's RageTexture and use the `position` function, which handles its value in seconds.
> 
> ```lua
> self:GetTexture():position( --[[Time in secs]] )
> ```
> {.is-warning}

As an example to demonstate each sprite table, we'll utilize the fox from the staff roll.

## Standard format

![fox.gif](/resources/actors/sprite/fox.gif){.align-right}

```lua
Frames = {
	{ Frame = 0, Delay = 0.1 },
	{ Frame = 1, Delay = 0.1 },
	{ Frame = 2, Delay = 0.1 },
	{ Frame = 3, Delay = 0.1 }
},
```

In this example, we're creating an animation of 4 frames (these are 0-indexed), that will last 0.4 seconds total, given the sum of each Delay.

## Utilizing Sprite.LinearFrames

![fox-4.gif](/resources/actors/sprite/fox-4.gif){.align-right}

This is a helper function inside the Sprite namespace that facilitates the creation of the Frames table, by automating the creation of the table with just 2 arguments, the amount of frames to use, and how long in general the animation will be.

```lua
Frames = Sprite.LinearFrames( 4, 2 )
-- Will return
--[[
{
	{ Frame = 0, Delay = 0.5 },
	{ Frame = 1, Delay = 0.5 },
	{ Frame = 2, Delay = 0.5 },
	{ Frame = 3, Delay = 0.5 },
},
]]
```

## Utilizing SetAllStateDelays on existing frames
This function can be utilized to update all delay amounts of the current frames in the sprite on the fly.

In the example, I have a sprite that already loads a sprite that has 4 frames, and plays on 0.1 second delays, making the animation on the top of the page, but now we want to make it slightly slower.

```lua
Frames = {
	{ Frame = 0, Delay = 0.1 },
	{ Frame = 1, Delay = 0.1 },
	{ Frame = 2, Delay = 0.1 },
	{ Frame = 3, Delay = 0.1 }
},
OnCommand=function(self)
	self:SetAllStateDelays(0.5)
end
```

Before

![fox.gif](/resources/actors/sprite/fox.gif){.align-center}

After

![fox-4.gif](/resources/actors/sprite/fox-4.gif){.align-center}

## Utilizing SetStateProperties

![fox-2.gif](/resources/actors/sprite/fox-2.gif){.align-right}

The SetStateProperties function can be utilized to update frame information on a sprite on the fly, by updating the entire table.

In this example, let's assume that the current sprite has the table describe above, and now we want to update the sprite to only show two frames of animation instead of 4. In this case, we just need to return a table into the function that only has the two frames.


```lua
self:SetStateProperties({
	{ Frame = 0, Delay = 0.5 },
	{ Frame = 1, Delay = 0.5 }
})
```