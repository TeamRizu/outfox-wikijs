---
title: What are screens?
description: An explanation about screens in Project Outfox, as they represent the container for every visual element for your theme. Part of the theming guide.
published: true
date: 2025-05-06T01:43:03.249Z
tags: guide, theming
editor: markdown
dateCreated: 2025-05-06T01:37:44.431Z
---

Before starting with anything on themes, we first need to look into what you're actually looking in your game right now. 

![screen-selectmusic-demo.png](/dev/theming/screen-selectmusic-demo.png)

All that you're seeing is contained on a [Screen](/en/dev/screens/Screen). These screens, depending on which class they're defined as, will output information (or your own) that the player can then interact with.

For example:
- All of the text that you're seeing is created by either using [Def.BitmapText](/en/dev/actors/actortypes/bitmaptext), or [Def.Text](/en/dev/actors/actortypes/text). The former being the standard form to make text, and the latter the newer method where it uses fonts for the same task.
- All of the images are created by the game using [Def.Sprite](/en/dev/actors/actortypes/sprite), but the engine can also take care of handling some of those for you.
- Some actors can be automated to perform certain tasks, like the difficulty numbers, which use [Def.RollingNumbers](/en/dev/actors/actortypes/rollingnumbers) to animate the rolling from one number to the other.
- The wheel at the bottom of the screen is handled by the theme's metrics, which declare how the wheel will be *transformed* and calculated. You can customize the look of the wheel to whatever you want!![ screen-selectmusic-demo.png](/dev/theming/ screen-selectmusic-demo.png)
- Some themes may have a notefield present, to preview what the player is about to face. These are done using [Def.NoteField](/en/dev/actors/actortypes/notefield) actors.

These are a few examples of the vast selection of [Actor Types](/en/dev/actors/actortypes) that the game provides you to play with. But, to start with our operation, we suggest starting by creating a Lua file that will represent your first file.

- [My First BGAnimation *Learn how to make your first BGAnimation file, which displays elements on the screen!*](/en/dev/theming/myfirstbga)
{.links-list}