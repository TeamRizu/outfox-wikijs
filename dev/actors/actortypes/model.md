---
title: Model
description: 
published: true
date: 2023-05-21T01:08:37.373Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:19.640Z
---

Allows one to display MilkShape3D ASCII models, having separate attributes for materials, bones and meshes.

```lua
Def.Model{
	Meshes="MyModel.txt",
	Materials="MyModel.txt",
	Bones="MyModel.txt",
	OnCommand=function(self)
		self:Center()

		-- When a model begins its animation, it will loop indefinitely. To stop that, use the loop command to
		-- set the flag to false.
		self:loop(false)
	end
}
```

**Meshes** are the composition and structure of the Model. This data represents the vertices that make the Model take shape.

**Materials** are the textures that the model will use. These can be any of the image formats listed in the Supported File Extensions page. They can also be .ini files that define animated textures on a Def.Sprite.

**Bones** make the model come to life. They can be defined within the primary model file, or, in the case of dancing characters, be controlled via a separate file that only contains the bones.

In the above example, all three attributes used the same filepath; all the necessary data was contained within a single file. It is possible to configure the MilkShape 3D software to output distinct files for meshes, materials, and bones, and set each Def.Model attribute accordingly, but that is outside the scope of this lesson.

> All three attributes must be provided within Def.Model as paths to resources that can be loaded or the game will crash.
{.is-danger}

## Table of Contents

- [Loading Additional Bones](/en/dev/actors/actortypes/model/Model-LoadingMoreBones)

## Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
Meshes | string | Path to a MilkShape 3D ASCII text file containing model meshes.
Materials | string | Path to a MilkShape 3D ASCII text file containing model materials.
Bones | string | Path to a MilkShape 3D ASCII text file containing model bones.