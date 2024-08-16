---
title: OutFox GLSL variables
description: 
published: true
date: 2024-08-16T17:17:29.463Z
tags: 
editor: markdown
dateCreated: 2024-08-16T17:17:29.463Z
---

These extra variables are given by the game itself, and aren't part of a standard GLSL implementation.

## Varying variables:
Often, these variables are written to in a vertex shader and read from in a fragment shader.

These are defined in the default vertex shader.

Name | Type | Description |
:------------ | :------ | :---------- |
position | vec3 | The xyz component of gl_Vertex
normal | vec3 | The resulting normal vector after combining the normal matrix with gl_Normal and flipping the y axis
color | vec4 | The value of gl_Color, which is usually the diffuse from an Actor
textureCoord | vec2 | The current position in the texture. Comes from the default vertex shader
imageCoord | vec2 | The current position in the image. Comes from the default vertex shader

## General uniform variables
These variables are usable in both vertex and fragment shaders.

Name | Type | Description |
:------------ | :------ | :---------- |
isEnvMap | bool | This is set to true when sphere environment mapping is enabled
time | float | The current time of the song in seconds. Not available when making a theme BG shader
beat | float | The current beat of the song. Not available when making a theme BG shader
resolution | vec2 | The theme resolution. This is not the same as the window/display resolution
sampler0 | sampler2D | the first texture of the actor
sampler1 | sampler2D | the second texture of the actor
viewMatrix | mat4 | the View component of the Model View matrix.
modelMatrix | mat4 | the Model component of the Model View matrix.
materialId | int | The index of the model's material. Only seen in Models
textureSize | vec2 | The size of the texture
imageSize | vec2 | The size of the image

## NoteField uniform variables
These variables show up when using shaders on NoteFields.

Name | Type | Description |
:------------ | :------ | :---------- |
iCol | int | the column the notefield object is in
iPlayfield | int | the player number for the notefield
isReceptor | bool | only true when being used on receptors
isHold | bool | only true when being used on hold bodies (includes top/bottom cap, but not the hold head/tail.)
fYOffset | float | The Y Offset of the note. Only seen in note shaders
fColOffset | float | The x offset of the column. Only seen in hold & notepath shaders because the vertex position includes column offsets
fNoteBeat | float | The beat of the note. Only seen in note & hold shaders
fNoteBeatAdj | float | The beat of the note after going through NoteTypeMult. Only seen in note & hold shaders