---
title: Sprite
description: Allows one to display images on screen. These images can be a png, jpeg, gif or even a video file.
published: true
date: 2024-01-21T23:24:58.359Z
tags: actor, def.sprite, sprite
editor: markdown
dateCreated: 2023-05-16T06:16:14.886Z
---

Allows one to display images on screen. These images can be a png, jpeg, gif or even a video file.

```lua
Def.Sprite{
	Texture="MyTexture.png", -- The Texture is optional, you can start a sprite without a texture.
	-- You can manipulate the amount of frames that a sprite can use using the Sprite argument.
	Frames={
		-- The structure for the Frame is as follows:
		--{ Frame = int, Delay = float , {float,float}, {float,float} }
		-- The two tables are optional upper left and lower right corners of the fraction of the
		-- frame to use.

		-- This will make a 4 frame sprite toggle between its frames for 0.5 seconds,
		-- making a 2 second animation.
		{ Frame = 0, Delay = 0.5 },
		{ Frame = 1, Delay = 0.5 },
		{ Frame = 2, Delay = 0.5 },
		{ Frame = 3, Delay = 0.5 },
	},
	OnCommand=function(self)
		-- You can also load new textures after assigning one beforehand.
		-- The path in Load is absolute, so you must put the entire path to the new image.
		self:Load( --[[ [Path to another texture] ]] )

		-- You can pause or jump to other sprites with the following commands.
		self:animate(0) -- 0 pauses the animation, 1 resumes it (Can be used as well for Models).
		self:pause() -- An alias for animate(0) (Can be used as well for Models).
		self:play() -- An alias for animate(1) (Can be used as well for Models).

		-- setstate jumps to a frame of the animation assigned. Animation states are 0-indexed.
		self:setstate( 2 ) -- Jumps to the third frame of the animation.
		-- If an out-of-range value is assigned ( < 0 or > #Frames ), an error is displayed
		-- displaying the total amount of frames available on the current sprite.

		-- The Frames set can also be manipulated during runtime, by using the SetStateProperties
		-- function. This example now inverts the animation.
		self:SetStateProperties(
			{
				{ Frame = 3, Delay = 0.5 },
				{ Frame = 2, Delay = 0.5 },
				{ Frame = 1, Delay = 0.5 },
				{ Frame = 0, Delay = 0.5 },
			}
		)
	end
}
```

# Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
Texture | string | Path to the texture to use for this sprite actor.
Frames | table | The table containing the frame per frame information to be interpreted by the actor. For more information, see [Managing Frames](/en/dev/actors/actortypes/sprite/Frames).
Frame[NNNN] |  number |  Alternative method for Frames's version of { Frame = `number` }, used for backwards compatibility with older actors.
Delay[NNNN] |  number |  Alternative method for Frames's version of { Delay = `number` }, used for backwards compatibility with older actors.

# Managing frames

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