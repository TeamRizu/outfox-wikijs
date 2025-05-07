---
title: Adding Sprites
description: Learn how to add sprites to your theme. Part of the theming guide.
published: true
date: 2025-05-07T06:24:58.781Z
tags: guide, theming
editor: markdown
dateCreated: 2025-05-07T06:24:58.781Z
---

So, you have your [ActorFrame](/en/dev/actors/actortypes/actorframe) declared from the previous chapters, you've learned to add actors to them, like a [BitmapText](/en/dev/actors/actortypes/bitmaptext) and a [Quad](/en/dev/actors/actortypes/quad) to render text, and to color the background respectively.

Now, let's add an image of your choosing to the screen, to learn how Sprites work. So, get an image, and place it on a new folder next to `BGAnimations` called `Graphics`. This is where all of your graphics will be stored in.

Once you placed your image of choosing to the folder, keep track of the name, because we're going to be using a special function to facilitate writing the path to this image. For this example, I'll use a file called "myimage.png".

Now, in the code, let's add a [Sprite](/en/dev/actors/actortypes/sprite). You'll notice that to add the image, we have a line that specifies a `Texture`.

```lua
return Def.ActorFrame{
	Def.Sprite{
  	Texture=THEME:GetPathG("","myimage"),
    OnCommand=function(self)
    	self:Center()
    end
  }
}
```

*Now, hold on... What is this `GetPathG` function, and what is `THEME`?*

Well, this is that special function I was talking about. This is called "GetPathGraphics" (GetPathG), which is part of the ThemeManager's namespace, which is called `THEME`. It's job is to autocomplete the path to the file that you specify on its parameters.

This means, instead of having to write a path like `../../Graphics/myimage`, you can instead just write `THEME:GetPathG("","myimage")`, and the game will automatically look for an file with the specified name. It can even alert you if the file is missing or doesn't match.

Now, reload the Title Menu, and voila! You'll see your image at the center of the screen.