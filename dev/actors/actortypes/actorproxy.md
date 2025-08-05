---
title: ActorProxy
description: 
published: true
date: 2023-11-04T05:58:24.864Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:12.564Z
---

An ActorProxy is an actor that allows rendering of other [Actors](/en/dev/actors/actortypes/actor) without the need to create the logic for it again.

> Anything done to the Target Actor shows up in the Proxy, but anything done to the Proxy will not show up on the Target.
{.is-info}

```lua
Def.ActorProxy{
    OnCommand=function(self)
        self:SetTarget( [target actor] ) 
    end
}
```
## Attributes

There are no special attributes for this actor class.

## Draw logic

As long as the target [Actor](/en/dev/actors/actortypes/actor) is present, it will draw it. If it's deleted during runtime, it will stop drawing.

## Functions

### `SetTarget`
([Actors](/en/dev/actors/actortypes/actor) `targetActor`)

Tells the ActorProxy to use `targetActor` as its draw target.

```lua
-- Let's assume that I have a quad that's
-- stored via a local variable.
local myQuad = ...

-- Now, in the function, we provide the actor itself.
self:SetTarget( myQuad ) 
```

In a more direct example with full [ActorFrame](/en/dev/actors/actortypes/actorframe) display:

```lua
local t = Def.ActorFrame{}

-- This will contain the handle for the BitmapText actor
-- to target.
local myText

t[#t+1] = Def.BitmapText{
	Font = "Common Normal",
	Text = "I am Text!",
	-- Not needed for this example, but it will make sense below.
	Name = "TheText",
	InitCommand = function(self)
		-- Now assign the handle to the variable.
		myText = self
	end
}

t[#t+1] = Def.ActorProxy{
	-- Notice here that we're using the OnCommand.
	-- This is to allow time for the BitmapText to assign the
	-- myText variable its handle by the time ActorProxy attempts
	-- to target it.
	OnCommand = function(self)
		self:SetTarget(myText)
		-- To show that it's a new draw copy of the actor,
		-- let's center the proxy.
		self:Center()
	end
}

return t
```

> Alternatively, the handle can also be provided by calling GetChild to that same actor from the Proxy itself, by utilizing the tricks from [Obtaining Children and ActorFrame levels](/en/dev/actors/actortypes/actor#obtaining-children-and-actorframe-levels).
{.is-info}

```lua
Def.ActorProxy{
	OnCommand = function(self)
  	-- Instead of using the myText variable, we'll reach the actor using GetParent and GetChild calls.
  	self:SetTarget( self:GetParent():GetChild("TheText") )
    -- To show that it's a new draw copy of the actor,
    -- let's center the proxy.
    self:Center()
  end
}
```

### `GetTarget`

Returns the current actor this ActorProxy is currently rendering. Returns `nil` if no actor is assigned previously.

```lua
self:GetTarget()
```