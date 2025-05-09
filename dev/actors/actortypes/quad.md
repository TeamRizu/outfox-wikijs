---
title: Quad
description: 
published: true
date: 2025-03-26T18:05:45.383Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:45.473Z
---

An arbitrary rectangle. Acts like a [Sprite](/en/dev/actors/actortypes/sprite) with a blank texture.

```lua
-- Generate a 64 x 64 rectangle on the center of the screen, and color it Yellow.
Def.Quad{
	OnCommand=function(self)
		self:zoomto( 64,64 ):diffuse( Color.Yellow )
		:xy( SCREEN_CENTER_X, SCREEN_CENTER_Y )
	end
}
```

This actor does not contain any attributes, and uses all the functions available for [Actor](/en/dev/actors/actortypes/actor).