---
title: WorkoutGraph
description: A graph showing the difficulty meter values of each entry on a course. Despite its name, it doesn't actually calculate anything about calories or workout.
published: true
date: 2023-11-04T05:10:32.872Z
tags: workoutgraph
editor: markdown
dateCreated: 2023-05-16T06:16:25.987Z
---

A graph showing the difficulty meter values of each entry on a course. **Despite its name, it doesn't actually calculate anything about calories or workout**.

The graph has a hardcoded ceiling of 35, being tied to the maximum difficulty value allowed in legacy SM.

> This actor will only work on Course Mode!
{.is-warning}

```lua
Def.WorkoutGraph{
    OnCommand=function(self)
        self:SetFromCurrentWorkout()
    end
}
```

![WorkoutGraph demonstration](/resources/actors/workoutgraph/demo.png)

An example of the WorkoutGraph in action, after a 5-song course.

> This image is using custom graphics to demonstrate the functionality of the actor. It is empty graphics by default.
{.is-info}

## Attributes

There are no special attributes for this actor class. It inherits from [ActorFrame](/en/dev/actors/actortypes/actorframe/_index#attributes).

## Graphics used

This actor loads special graphics to create the graph.

- `WorkoutGraph empty`

Background for the workout graph.

- `WorkoutGraph bar`

The vertical bar to indicate the calories burned on each song. 

## Functions

### `SetFromCurrentWorkout`

Calls the data to be obtained from the "current workout", which is the current session of your course.

### `SetFromGameStateAndHighlightSong`
`(number numSongs)`

Performs the same action as [`SetFromCurrentWorkout`](#setfromcurrentworkout), but allows you to set a limit on how many songs should be shown in the graph.
