---
title: DeviceList
description: 
published: true
date: 2023-11-04T05:12:08.239Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:46.022Z
---

A [BitmapText](/en/dev/actors/actortypes/bitmaptext) actor that shows the current list of devices connected and recognized by the game.

```lua
Def.DeviceList {
	Font="Common Normal"
}
```

This actor is used on the Test Input screen to showcase which controllers are detected.

Attributes for this actor can be found on [BitmapText](/en/dev/actors/actortypes/bitmaptext).

> Text application to this actor is ignored as the game automatically updates it with the current devices.
{.is-warning}