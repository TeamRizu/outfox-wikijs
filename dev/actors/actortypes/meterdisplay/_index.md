---
title: MeterDisplay
description: 
published: true
date: 2023-05-19T23:47:28.095Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:11.487Z
---

The base for [SongMeterDisplay](/en/dev/actors/actortypes/songmeterdisplay/_index), which uses two [Actors](/en/dev/actors/actortypes/_index) to render the progress of a given value.

> Unlike [SongMeterDisplay](../songmeterdisplay/), MeterDisplay doesn't update by itself. In order to perform updates, you have to
> manually set a new width and position value for **Stream** and **Tip**.
{.is-warning}

```lua
Def.MeterDisplay{
	-- The width the MeterDisplay. Can be adjusted later with SetStreamWidth.
	StreamWidth = 100,
	InitCommand=function(self)
		-- This generates a 300 x [the height of your Stream texture] that will define the current progress of whatever song is currently being played.
		-- The actor will automatically update progress for the Tip and the Stream.
		self:SetStreamWidth( 300 )
	end,
	-- Both the Stream and Tip are AutoActors, so they can be any actor type.
	Stream=Def.Sprite{ Texture="MyStreamBar" },
	Tip=Def.Sprite{ Texture="MyTip" }
}
```

## Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
StreamWidth | number | The width the MeterDisplay. Can be adjusted later with [SetStreamWidth](#setstreamwidth).
Stream | [Actor](/en/dev/actors/actortypes/actor/_index) | The actor that will represent the progress of the song.
Tip | [Actor](/en/dev/actors/actortypes/actor/_index) | The actor that will represent the current position of the song.

> The **Stream** attribute is required for the SongMeterDisplay to be created. Otherwise it will return an empty [Actor](../actor/).
{.is-warning}

> Both **Stream** and **Tip** can be any kind of [Actor](../../actortypes/).
{.is-info}

## Functions

### SetStreamWidth
`(float Width)`

Adjusts the width of the MeterDisplay to the desired `Width`.