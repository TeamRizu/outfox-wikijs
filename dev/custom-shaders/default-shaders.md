---
title: Default Shaders
description: 
published: true
date: 2024-08-16T17:04:38.108Z
tags: 
editor: markdown
dateCreated: 2024-08-16T17:04:38.108Z
---

These shaders are what the game uses when a Shader attribute is undefined.

(For example, if Frag is defined, and not Vert, the default Vertex shader is used)

When making your own custom shaders, these are a good starting place.

- Fragment
```glsl
uniform sampler2D sampler0; // the texture given by the engine
varying vec2 textureCoord; // The current coordinate of the texture
varying vec4 color; // The diffuse of the actor
void main (void)
{
  gl_FragColor = texture2D( sampler0, textureCoord ) * color; // Sets the current fragment to the current coordinate of the texture.
}
```

- Vertex
```glsl
attribute vec4 TextureMatrixScale; // Used for scrolling textures & customtexturerect
varying vec3 position; // The current vertex position
varying vec3 normal; // The normal of the vertex
varying vec4 color; // The diffuse of the actor
varying vec2 textureCoord; // The current coordinate of the texture
varying vec2 imageCoord; // The current coordinate of the image
uniform vec2 textureSize; // Size of the texture
uniform vec2 imageSize; // Size of the image
void main() {
	// Vertex position & normal
	normal = gl_NormalMatrix * gl_Normal * vec3( 1.0, -1.0, 1.0 );
	gl_Position = (gl_ModelViewProjectionMatrix * gl_Vertex);
	position = gl_Vertex.xyz;

	// Texture coordinates (Includes the Texture Matrix Scale)
	gl_TexCoord[0] = (gl_TextureMatrix[0] * gl_MultiTexCoord0 * TextureMatrixScale) + (gl_MultiTexCoord0 * (vec4(1)-TextureMatrixScale));
	textureCoord = ((gl_TextureMatrix[0] * gl_MultiTexCoord0 * TextureMatrixScale) + (gl_MultiTexCoord0 * (vec4(1)-TextureMatrixScale))).xy;
	imageCoord = textureCoord * textureSize / imageSize;

	// Colors
	gl_FrontColor = gl_Color;
	color = gl_Color;
}
```
If you plan to do a vertex shader on noteskins or other 3D models, it's recommended to include the Texture Matrix Scale (the attribute at the very top) and the lines that set `gl_TexCoord[0]` and  `textureCoord`, so scrolling textures work properly.