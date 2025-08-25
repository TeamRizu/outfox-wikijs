---
title: Obtaining Child and ActorFrame Levels
description: 
published: true
date: 2023-11-04T05:19:23.594Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:13:57.266Z
---

When using [Actors](/en/dev/actors/actortypes/actor), you can use `self:GetParent()` and `self:GetChild()` to get elements from other [ActorFrames](/en/dev/actors/actortypes/actorframe) or [Actors](/en/dev/actors/actortypes/actor).

> `self:GetChild()` can only be used by [ActorFrames](../../actorframe).
{.is-warning}

You can think of an [ActorFrame](/en/dev/actors/actortypes/actorframe) as a tree of objects. This is the original table. And now you've called GetParent on the [ActorProxy](/en/dev/actors/actortypes/actorproxy).

```lua
Def.ActorFrame{
	Def.BitmapText{ Name="MyText" },
	* Def.ActorProxy{
		OnCommand=function(self)
			self:GetParent()
		end
	},
}
```

```kroki
mermaid

graph LR
    AF[Def.ActorFrame] --- BT(Def.BitmapText) & AP(Def.ActorProxy)
	style AF stroke-width:4px
	style BT stroke-width:4px
	style AP fill:#585,color:#fff,stroke-width:4px
```

When calling it, you go back up a level, which in this case, it will become [ActorFrame](/en/dev/actors/actortypes/actorframe).

```kroki
mermaid

graph LR
    AF(Def.ActorFrame) --- BT(Def.BitmapText) & AP(Def.ActorProxy);
	style AF fill:#585,color:#fff,stroke-width:4px
	style BT stroke-width:4px
	style AP stroke-width:4px
```

In this new location, we get the `MyText` actor, which can be achieved by calling the GetChild command, and can also return back to the [ActorFrame](/en/dev/actors/actortypes/actorframe), as we're now in a level that can get both actors *(shown in orange)*.

```lua
Def.ActorFrame{
	* Def.BitmapText{ Name="MyText" },
	Def.ActorProxy{
		OnCommand=function(self)
			self:GetParent():GetChild("MyText"):spin()
		end
	},
}
```

```kroki
mermaid

graph LR
    AF(Def.ActorFrame ) --> BT(Def.BitmapText) & AP(Def.ActorProxy);
	style AF fill:#f85,color:#fff,stroke-width:4px
	style BT fill:#585,color:#fff,stroke-width:4px
	style AP fill:#585,color:#fff,stroke-width:4px
```

The command uses a String argument, but can also grab from nested tables in case of an [ActorFrame](/en/dev/actors/actortypes/actorframe) not having actors with names assigned. On those cases, actors are just indexed on that [ActorFrame](/en/dev/actors/actortypes/actorframe) set.

### Example Without Names

```lua
Def.ActorFrame{
	OnCommand=function(self)
		-- If we want to get to the BitmapText, we'll need to get
		-- the second entry on the ActorFrame.
		self:GetChild("")[2] -- returns the BitmapText actor.
	end,
	Def.Sprite{},
	Def.BitmapText{}
}
```

### Example With Names

```lua
Def.ActorFrame{
	OnCommand=function(self)
		-- If we want to get to the BitmapText,
		-- we'll need to get the "Text" actor.
		self:GetChild("Text") -- returns the BitmapText actor.
	end,
	Def.Sprite{ Name = "Image" },
	Def.BitmapText{ Name = "Text" }
}
```
