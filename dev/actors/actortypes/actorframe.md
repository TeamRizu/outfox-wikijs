---
title: ActorFrame
description: ActorFrames can hold other actors. The Def. format is set up like any other lua table, allowing for creating actors in batches.
published: true
date: 2023-11-04T05:23:44.341Z
tags: actorframe
editor: markdown
dateCreated: 2023-05-16T06:14:00.966Z
---

ActorFrames can hold other actors. The ``Def.`` format is set up like any other lua table, allowing for creating actors in batches. Because of this, there are multiple ways to build an ActorFrame.

```lua
Def.ActorFrame{
    -- This sprite is now included inside of the ActorFrame.
    -- Any changes from the ActorFrame will affect the sprite, such as position, rotation,
    -- zoom and such.
    Def.Sprite{}
}
```

## Attributes
| Name | Type | Action |
| :--- | :--- | :----- |
UpdateRate | number | Defines the update rate for the actorframe to update.
FOV | number | The Field of View value for the items inside of the ActorFrame.
VanishX | number | Sets the X vanish for the ActorFrame.
VanishY | number | Sets the X vanish for the ActorFrame.
FarDistZ | number | Sets the Z draw distance for the ActorFrame.
Lighting | bool | Enables lighting for the ActorFrame (unused).

> The following require Lighting to be enabled. However, only the ambient color seems to work. This bug has been present since sm-ssc.
{.is-info}

| Name | Type | Action |
| :--- | :--- | :----- |
AmbientColor | color | Ambient coloring for the ActorFrame.
DiffuseColor | color | Diffuse coloring for the ActorFrame.
SpecularColor | color | Specular coloring for the ActorFrame.
LightDirection | {0,0,0} | The direction of the lighting for the ActorFrame.

This actor inherits attributes from [Actor](/en/dev/actors/actortypes/actor).

## Inline building

Actors can be explicitly placed into an ActorFrame like this:
```lua
Def.ActorFrame{
	Def.Actor{
		--Commands and stuff go here.
	},
	Def.Sprite{
		--More commands and stuff go here.
	}
}
```

## Concatenation

Because lua tables can be concatenated (added) to each other, so can ActorFrames.

This can allow for programmatically creating [Actor](/en/dev/actors/actortypes/actor) in batches as needed.

However, if one does not plan on creating [Actor](/en/dev/actors/actortypes/actor) programmaticly, then a simple `return Def.ActorFrame{...` is all that's needed. Storing it into a local variable that gets returned will waste resources.

There are two ways to add onto an ActorFrame.

<!-- TODO: There's probably better ways to show this. -->
### Method 1 (indexing)
```lua
local t = Def.ActorFrame{
	Def.Sprite{
		--commands & stuff
	},
	Def.BitmapText{
		--who even knows
	},
}

t[#t+1] = Def.Actor{
	--It's the third actor
}
return t
```

### Method 2 (lua concatenation)
```lua
return Def.ActorFrame{
	Def.Sprite{
		--commands & stuff
	},
	Def.BitmapText{
		--who even knows
	},
} .. Def.Actor{
	--It's the third actor
}
```

## Functions

### `AddChildFromPath`
`(string sPath)`

Adds a child to the ActorFrame from the specified path. Returns true if its successful.

### `AddChild`
`(function Actor)`

Adds a collection of [Actors](/en/dev/actors/actortypes/actor) from `actors` to the ActorFrame via a function.
Just like regular ActorFrames or [Actors](/en/dev/actors/actortypes/actor), it must return some kind of table.

```lua
self:AddChild(function()
	return Def.BitmapText{
		Font = "Common Normal",
		Text = "I am text, added during runtime!",
		-- Let's use item here to avoid confusion with self.
		InitCommand = function(item)
			item:Center()
		end
	}
end)
```

### `fardistz`
`(float fFarDistZ)`

Sets how far back in z-space an ActorFrame's contents can be visible.
If FOV is zero, this also sets the positive z-space limit as well.

### `fov`
`(float fFOV)`

Sets the field of view for the ActorFrame.

### `GetChild`
`(string sName)`

Returns the child with a name of <code>sName</code>.
If there are multiple children with that name, returns an array of those children.
The table also acts as a pass through layer, function calls pass through to the last child of that name.

obtainlevels
For more information about how obtaining ActorFrame children work, check [Obtaining Child and ActorFrame Levels](/en/dev/actors/actortypes/actor#obtaining-child-and-actorframe-levels).
