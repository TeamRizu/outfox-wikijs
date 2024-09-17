---
title: RollingNumbers
description: 
published: true
date: 2023-11-04T05:45:29.317Z
tags: 
editor: markdown
dateCreated: 2023-11-04T05:45:26.828Z
---

A [BitmapText](/en/dev/actors/actortypes/bitmaptext) with a number that transitions to the target number.

```lua
Def.RollingNumbers{
	-- Load the font that the numbers will be rendered with.
	File = THEME:GetPathF("Common", "Normal"),
	InitCommand=function(self)
		-- Loads the MetricsGroup to use it's settings on.
		self:Load("RollingNumbers")

		-- To update the value, use the targetnumber function.
		self:targetnumber(300)
	end
}
```

# Attributes

It inherits its attributes from [BitmapText](/en/dev/actors/actortypes/bitmaptext).

# Required Metrics

This actor requires metrics for it to be loaded before anything else is done with it.

The following are the values for the default group called `RollingNumbers`.

```ini
[RollingNumbers]
TextFormat="%09.0f"
ApproachSeconds=0.2
Commify=true
LeadingZeroMultiplyColor=color("#777777FF")
```

> If you'd like to add a custom group, just add a new group that contains different settings than the ones shown in the example, and use the [Load](#Load) function with the name of the group.
{.is-info}

```ini
[MyNumbers]
ApproachSeconds=0.1
Commify=false
LeadingZeroMultiplyColor=color("#909040FF")
```

```lua
-- Loads the MetricsGroup to use it's settings on.
self:Load("MyNumbers")
```

# Actor Behaviour

Based on the value of `ApproachSeconds`, the actor will attempt to approach the **target value** in the same ammount of time. Attempting to use `targetnumber` without loading a metrics group previously will lead to warning requesting a group.

> You must use `Load` to load the metrics for a RollingNumbers actor before doing anything else.
{.is-warning}

If the `Commify` setting is enabled, the actor will add commas on every 3rd number in the sequence.

```
-- Without commify
123456789

-- With commify
123,456,789
```

# Functions

## `Load`
`(string sMetricsGroup)`

Loads in the MetricsGroup provided in `sMetricsGroup`. This group contains the settings for the Rolling Numbers like style, formatting, coloring, etc.

## `targetnumber`
`(int target)`

Sets the new target value to `target`. The speed for this transition is dependant on the `ApproachSeconds` metric provided on the currently loaded MetricsGroup.

> You must use `Load` to load the metrics for a RollingNumbers actor before running this command.
{.is-warning}