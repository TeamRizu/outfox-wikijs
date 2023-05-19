---
title: Doing Mods with Def.NoteField
description: 
published: true
date: 2023-05-19T23:57:49.214Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:23.169Z
---

Usually, a Player controls a [NoteField](/en/dev/actors/actortypes/notefield/_index), which includes positioning, zooming, rotation and vanish point manipulation. The game itself would also handle approach rates for modifiers used on a Player.

With [Def.NoteField](/en/dev/actors/actortypes/notefield/_index), this is now done manually, since there is no "Player" to handle everything.

## Applying modifiers

Applying modifiers is instant, unlike the approach rate behavior usually seen.

This can be done through multiple ways:

### 1. Using the ModsFromString function in the NoteField.
- Allows one to easilly set the modifiers on the [NoteField](/en/dev/actors/actortypes/notefield/_index) through modstrings.
- Some modifiers will not be usable through modstrings.

```lua
Def.NoteField{
	OnCommand= function()
		self:ModsFromString('drunk')
	end,
}
```

### 2. Grabbing the PlayerOptions of the NoteField
- For now, `"ModsLevel_Current"` has to be used, since the game will no longer handle approaching from `"ModsLevel_Song"`.
- Allows for the use of all modifiers a Player can access.
- Requires knowning how to use the PlayerOptions functions.

```lua
Def.NoteField{
	OnCommand= function()
		self:GetPlayerOptions('ModsLevel_Current'):Drunk(1)
	end,
}
```

## NoteData

A [NoteField](/en/dev/actors/actortypes/notefield/_index) starts with the chart the specified player used. However, SetNoteDataFromLua is usable on a Def.NoteField, allowing one to change the chart used. Unlike player, there is no SetNoteData function (for now), so the table format from GetNoteData has to be followed.

## Replicating Mini and Perspective

Refer to the section [How a Player Manipulates its' NoteField](/en/dev/actors/actortypes/notefield/NoteField-PlayerManipulation).
