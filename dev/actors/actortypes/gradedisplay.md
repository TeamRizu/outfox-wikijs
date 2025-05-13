---
title: GradeDisplay
description: 
published: true
date: 2025-05-13T04:57:43.035Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:53.030Z
---

An [ActorFrame](/dev/actors/actortypes/actorframe) containing [AutoActors](/dev/actors/actortypes) based on the number of grades available that are assigned by the theme (`PlayerStageStats::NumGradeTiersUsed`).

```lua
Def.GradeDisplay{
}
```

The grades that will be shown depends on the amount of Grades declared by the theme's metrics. By default, the game generates 7 grades.

## Attributes

This actor inherits the attributes from [ActorFrame](/dev/actors/actortypes/actorframe).

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