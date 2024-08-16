---
title: Standard GLSL variables and attributes
description: 
published: true
date: 2024-08-16T17:12:12.147Z
tags: 
editor: markdown
dateCreated: 2024-08-16T17:12:12.147Z
---

These variables and attributes are available as part of the GLSL 1.20 language. They are always prefixed with `gl_`.
<!--TODO: This section isn't quite complete, as there are still some things I'm sure about.-->

Sourced from the GLSL 1.20 spec: https://registry.khronos.org/OpenGL/specs/gl/GLSLangSpec.1.20.pdf

## Shader variables

Name | Type | Shader Type | Description |
:------------ | :------  | :------ | :---------- |
gl_Position | vec4 | Vertex | The end-result position of the vertex. This is usually the product of the entire model view projection matrix (`gl_ModelViewProjectionMatrix`) and the original vertex (`gl_Vertex`).
gl_PointSize | float | Vertex | The size of the point in pixels. Doesn't have to be written to.
gl_ClipVertex | float | Vertex | The position to use for user clipping planes. Doesn't have to be written to.
gl_FragCoord | vec4 | Fragment | The position of the current game window pixel. Cannot be written to. <!--TODO: Does this use the AFT sizes for objects inside of it?-->
gl_FrontFacing | bool | Fragment | Is the fragment being used in a front-facing object? Cannot be written to.
gl_FragColor | vec4 | Fragment | The end-result color of the fragment. Cannot be used with gl_FragData.
gl_FragData[ ] | vec4 | Fragment | An array of fragment data to write. Cannot be used with gl_FragColor.
gl_FragDepth | float | Fragment | The depth value for the current fragment. Doesn't have to be written to.

## Vertex shader attributes
Name | Type | Description |
:------------ | :------ | :---------- |
gl_Color | vec4 | This is often the diffuse of the actor. Can be read from in fragment shaders.
gl_SecondaryColor | vec4 | What is this used for? Can be read from in fragment shaders.
gl_Normal | vec3 | The normal vector of the vertex
gl_Vertex | vec3 | The original position of the vertex
gl_MultiTexCoord0 | vec4 | The multitexture coordinate? Used in the Texture Matrix Scale.
gl_MultiTexCoord1-7 | vec4 | Are these used?
gl_FogCoord | float | The vertex's distance away from the fog?

## Uniform variables
The four mat4s have Inverse, Transpose and InverseTranspose variants.
Name | Type | Description |
:------------ | :------ | :---------- |
gl_ModelViewMatrix | mat4 | The current model view matrix. Contains scale, rotation and skew.
gl_ProjectionMatrix | mat4 | The current projection matrix. Contains perspective (FOV).
gl_ModelViewProjectionMatrix | mat4 | The entire model view projection matrix.
gl_TextureMatrix[ ] | mat4 | An array of texture matrices. Used in the Texture Matrix Scale.
gl_NormalMatrix | mat3 | "transpose of the inverse of the upperleftmost 3x3 of gl_ModelViewMatrix", used in the default vertex shader
gl_NormalScale | float | "normal scaling" (Is this used?)

<!--Do I include the struct uniforms from page 51-53? (57-59 on pdf)-->

## Varying variables:
Often, these variables are written to in a vertex shader and read from in a fragment shader.
Name | Type | Description |
:------------ | :------ | :---------- |
gl_FrontColor | vec4 | The color used for the front face. The default vertex shader sets this to gl_Color
gl_BackColor | vec4 | The color used for the back face?
gl_FrontSecondaryColor | vec4 | The secondary color used for the front face?
gl_BackSecondaryColor | vec4 | The secondary color used for the back face?
gl_TexCoord[ ] | vec4 | ??? Can be read from in fragment shaders. Used with the Texture Matrix Scale
gl_FogFragCoord | float | ??? Can be read from in fragment shaders.
gl_PointCoord | vec2 | ???
