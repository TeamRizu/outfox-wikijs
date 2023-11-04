---
title: GradeDisplay
description: 
published: true
date: 2023-05-19T23:34:13.804Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:53.030Z
---

An [ActorFrame](/en/dev/actors/actortypes/actorframe/_index) containing [AutoActors](/en/dev/actors/actortypes/_index) based on the number of grades available that are assigned by the theme (`PlayerStageStats::NumGradeTiersUsed`).

```lua
Def.GradeDisplay{
}
```

## Attributes

This actor inherits the attributes from [ActorFrame](/en/dev/actors/actortypes/actorframe/_index).

## Functions

### `Load`
`(string sMetricsGroup)`

Load the graphics from a defined "metrics" group. It will seek for grade images with the following format:
```
[sMetricsGroup] Grade
```

> Internally it is called metrics, but this actor doesn't use any kind of graphics directly, other than the ammount of grades defined by `PlayerStageStats::NumGradeTiersUsed`.
{.is-info}

### `SetGrade`
`(Grade newGrade)`

Set the grade to display. Requires [`Load`](#load) to have been called before, otherwise it will fail.