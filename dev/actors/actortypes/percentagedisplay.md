---
title: PercentageDisplay
description: 
published: true
date: 2025-03-26T18:05:13.983Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:41.805Z
---

The PercentageDisplay is an actor which relies on [BitmapText](/en/dev/actors/actortypes/bitmaptext) to draw a player's current score in a percentage (%).

While using this actor, any kind of text string manipulation won't work if **AutoRefresh** is enabled, as it constantly updates the [BitmapText](/en/dev/actors/actortypes/bitmaptext) for **Percent** and **PercentRemainder** (if defined) with the current percent data.

> If **Percentage Scoring** is disabled, this actor will show the score in Dance Points instead (`000000000`).
> 
> Note that this won't add commas to the score, so it will need to be declared using the `commify` function on the `FormatPercentScore` Attribute.
{.is-info}

```lua
Def.PercentageDisplay{
	DancePointsDigits = 2,
	AutoRefresh = true,
	FormatPercentScore =
	Percent = Def.BitmapText{
            Font = "Common Normal" -- Alias of the default font.
	}
	PercentRemainder = Def.BitmapText{
            Font = "Common Normal" -- Alias of the default font.
	}
}
```

## Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
DancePointsDigits | int | Defines how many digits should be shown when the score needs to be presented as dance points. Applicable if **Percentage Scoring** is **disabled**.
AutoRefresh | bool | Tells the actor to automatically update if there's any update to the player's score.
FormatPercentScore | function | Tells the actor how to present this percentage score for the Percent and PercentRemainder actors. Applicable if **Percentage Scoring** is **enabled**.
Percent | [BitmapText](/en/dev/actors/actortypes/bitmaptext) | The text that will draw the main percentage. Can also draw the entire percentage (including decimals) if **PercentRemainder** is not defined.
PercentRemainder | [BitmapText](/en/dev/actors/actortypes/bitmaptext) | The text that will draw the decimals for the percentage score.

## Functions

### LoadFromStats
`( PlayerState state, PlayerStageStats stats )`

Loads the player information so the PercentageDisplay can update based on the player data.

> If **AutoRefresh** is off, this data won't be updated automatically and the function will need to be called again manually to perform the same thing.
{.is-warning}
