---
title: Shaders and the Custom Shader System
description: 
published: true
date: 2024-08-16T17:01:39.928Z
tags: 
editor: markdown
dateCreated: 2024-08-16T17:01:39.928Z
---

Shaders are (usually small) programs that your GPU runs. (As opposed to programs your CPU runs, like OutFox)

There are two types of shaders relevant to OutFox:
- Fragment (.frag) Shaders: These affect pixel/texture data. Useful for manipulating or generating the texture applied to an object. (Models, sprites, etc.)
- Vertex (.vert) Shaders: These affect vertex data. Useful for messing with objects in 3D space or altering the shape of an object. This does not allow for adding or removing vertices.

In OutFox, Actors have the "EffectMode", which has several baked-in shaders already available.

## What are Custom Shaders?
Custom shaders allow for arbitrary GLSL shaders to be compiled and run on Actors in the engine.

These are mostly seen in gimmick files, but themes can use custom shaders as well.

Usually, these can be loaded by Actors defined in lua files.

## What is GLSL?
GLSL stands for the OpenGL Shading Language. This is what gets compiled into programs that the GPU runs.

GLSL has many versions, with varying amounts of backwards compatibility.

Newer versions of GLSL can be incompatible with older GPUs (or even whole systems).

Generally, version 1.20 is a safe enough version to use, as the most common GPUs and OSs (Mac, Windows, Linux) can work with it.

To ensure that no ambiguity happens across GPUs, the first line of a shader is usually `#version 120`. This explicitly chooses GLSL 1.20 as the version to target.

## How to enable Custom Shaders
By default, custom shaders are disabled due to potentially heavy shaders being ran, which can make the game's performance significantly lower.

To enable custom shaders, set the preference `CustomShadersDisabled` to 0.

If disabled, attempting to do anything involving custom shaders will just give a warning in the game logs.

## Checking for ability to use Custom Shaders
If you are a gimmick or theme creator, you can easilly check in lua with GetPreference:
```lua
local noShader = PREFSMAN:GetPreference('CustomShadersDisabled') -- true = custom shaders are disabled
```

<!--TODO: See if this also affects vert shaders-->
## The Y Axis is flipped for texture coordinates
In GLSL sites like Shadertoy, (0,0) is the bottom left.

In OutFox, (0,0) is the top left, which matches the actor coordinate system.

This affects textureCoord, imageCoord and gl_FragCoord.

## Optimization possibilities using ActorFrameTextures
Running heavy shaders more than necessary can result in the game's performance greatly decreasing. There are ways to make it less heavy (without modifying the shader in question) with an ActorFrameTexture:
- Limit how many times the shader code is run (using SetUpdateFPS on the AFT)
- Limit how many pixels the shader has to process (Setting a smaller width & height for the AFT)
- Render the shader inside the AFT and have multiple sprites read from it (instead of having multiple sprites run the shader)

## Extra resources
- **[ShaderToy](https://www.shadertoy.com/)** - An online site with a bunch of shaders made by other people.

- **[The Book Of Shaders](https://thebookofshaders.com/)** - A useful resource for learning how to make GLSL shaders from scratch.
