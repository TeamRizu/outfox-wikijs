---
title: MemoryCardDisplay
description: 
published: true
date: 2025-03-26T18:02:00.962Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:15:07.741Z
---

Creates an [ActorFrame](/en/dev/actors/actortypes/actorframe) that contains a [Sprite](/en/dev/actors/actortypes/sprite) with the current status for a Player's MemoryCard.

```lua
Def.MemoryCardDisplay{
	PlayerNumber=PLAYER_1
}
```

On each memory card update, the actor will be updated to detect if the card is loaded, ejected, checking, toolate, non-existent, and others.

> The graphics used to update this actor are located in `Graphics/MemoryCardDisplay [Card State] p[PlayerNumber index]`.
{.is-info}

<details>

<summary>List of MemoryCard states used by MemoryCardDisplay.</summary>

- MemoryCardDisplay checking p1
- MemoryCardDisplay checking p2
- MemoryCardDisplay error p1
- MemoryCardDisplay error p2
- MemoryCardDisplay late p1
- MemoryCardDisplay late p2
- MemoryCardDisplay none p1
- MemoryCardDisplay none p2
- MemoryCardDisplay ready p1
- MemoryCardDisplay ready p2
- MemoryCardDisplay removed p1
- MemoryCardDisplay removed p2

</details>

## Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
PlayerNumber |  PlayerNumber | The player to check its current MemoryCard state.