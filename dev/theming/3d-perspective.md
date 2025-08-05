---
title: 3D Perspectives on Actors
description: This document will go into detail about setting up an ActorFrame to perform operations that resemble a 3D environment.
published: true
date: 2025-05-31T07:53:23.581Z
tags: 
editor: markdown
dateCreated: 2025-05-31T07:47:11.523Z
---

> This document is in very early stages! Code is incomplete!
> \- Jose_Varela
{.is-warning}

As Project OutFox is a 3D game engine, the entire game is running in 3D space, but it's not clearly noticeable at first until you see elements like [NoteSkins]() or [Dancing Characters]() that you find out that it's possible. So how about getting something like that setup on your theme?

For this, we need to describe some quirks about 3D in Project OutFox (and other SM-based builds):

- The FOV for every ActorFrame defaults to 35. This can be modified later.
- By default, the game will render out up to 1000 pixels on the z axis on the actor. This isn't scaled by the engine, so 1000px on a 720p theme will be closer than on a 480p theme. This can also be modified later.
- Every ActorFrame by default will have it's vanish point set to the game's origin point, which is {0,0}, on the top left of the screen.


# Adjusting the FOV

To adjust the FOV on your environment [ActorFrame](/en/dev/actors/actortypes/actorframe), you have two options:

- Adjust the FOV attribute on the [Def.ActorFrame](/en/dev/actors/actortypes/actorframe) object.
- Use the `self:fov` function on said [ActorFrame](/en/dev/actors/actortypes/actorframe).
```lua
self:fov(90) -- This will set it to a FOV of 90.
```


# Adjusting the draw distance

To adjust the draw distance, we make use of the `fardistz` function, available for [ActorFrames](/en/dev/actors/actortypes/actorframe).

```lua
self:fardistz(3000) -- This will set it to 3000px.
```

# First-Person Environment Example

To perform this kind of 3D projection, we'll be performing a trick that's usually shown in 3D rendering where the "Camera" - which is what the user is seeing - is completely stationary, and instead, the entire world (objects and all) are moving relative to that camera.

To start, we need to setup some variables, and some functions: such as a way to calculate the vector position of the "Camera", and every object you want to place down. For this, here's a simple `Vector3` metatable that will help out with these calculations.

<details>

<summary>Vector3 metatable Lua code</summary>

```lua
local function Vector3(x,y,z) end

---@class Vector3
Vector3 = {
    __add = function (a,b)
        return Vector3.new(
            a.x + b.x,
            a.y + b.y,
            a.z + b.z
        )
    end,
    __sub = function (a,b)
        return Vector3.new(
            a.x - b.x,
            a.y - b.y,
            a.z - b.z
        )
    end,
    __tostring = function (this)
        return ("{%f,%f,%f}"):format(this.x, this.y, this.z)
    end
}
Vector3.__index = Vector3

function Vector3.new(x, y, z)
    local instance = {
        x = x or 0,
        y = y or 0,
        z = z or 0,
    }
    setmetatable(instance, Vector3)
    return instance
end

function Vector3.distance(a,b)
    local sum = math.abs((a.x - b.x))^2 + math.abs((a.y - b.y))^2 + math.abs((a.z - b.z))^2
    local root = math.sqrt(sum)
    return root
end
```

</details>

With the code, now let's setup some initial variables that will aid on calculating rotation, position and movement speed.

```lua
local pitch = 0
local yaw = 0
local curSpeed = Vector3.new(0,0,0)
local rad = math.pi/180
local cam = Vector3.new(0,0,0)
```

Since the "Camera" in Project OutFox doesn't ever move, we'll do a technique were an [ActorFrame](/en/dev/actors/actortypes/actorframe) will pretend to the camera, and another one, the environment that it will project from.

```lua
--[[
	This will our "Camera", which will be positioned at the center of the screen,
  and will handle things like yaw and pitch, for rotation.
]] 
local EnvCamera = Def.ActorFrame{
    InitCommand=function (self)
    		-- The addz function here will shift this camera 450px backwards so
        -- the perspective trick can work.
        self:Center():addz(450)
    end,
    -- This rotateactor command will be executed whenever we have an input.
    rotateactorCommand=function(self)
        self:rotationx(pitch):rotationy(yaw)
    end
}

local Environment = Def.ActorFrame{
		FOV=90,
    OnCommand=function (self)
        self:fardistz(9e9)
        self:z( -cam.z )
        :y( -cam.y )
        :x( -cam.x )
    end,
    rotateactorCommand=function(self)
        -- self:rotationx(pitch):rotationy(yaw)
        self:z( -cam.z )
        :y( -cam.y )
        :x( -cam.x )

        :fov( curFOV )
    end
}
```