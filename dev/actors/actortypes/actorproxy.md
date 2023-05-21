---
title: ActorProxy
description: 
published: true
date: 2023-05-21T01:05:42.929Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:12.564Z
---

An ActorProxy is an actor that allows rendering of other [Actors](/en/dev/actors/actortypes/actor) without the need to create the logic for it again.

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

As long as the target [Actors](/en/dev/actors/actortypes/actor) is present, it will draw it. If it's deleted during runtime, it will stop drawing.

## Functions

### `SetTarget`
([Actors](/en/dev/actors/actortypes/actor) targetActor)

Tells the ActorProxy to use `targetActor` as its draw target.


### `GetTarget`

Returns the current actor this ActorProxy is currently rendering. Returns `nil` if no actor is assigned previously.
