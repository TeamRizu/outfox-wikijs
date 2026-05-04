---
title: HoldJudgment
description: The actorframe representing if you held a hold/roll successfully or not.
published: true
date: 2026-05-04T00:28:43.684Z
tags: 
editor: markdown
dateCreated: 2026-05-03T18:21:07.454Z
---

The HoldJudgment is a [Sprite](/en/dev/actors/actortypes/sprite) that is shown to the notefield if you held a hold or roll succesfully.

<video src="/resources/actors/holdjudgment-example.mp4" controls autoplay height=200></video>

Normally this is used only with images, which the game can accomodate, but it can be controlled as well with a separate Lua file called `HoldJudgment label 1x2.lua` in the `Graphics` folder.

>The file *must* include `1x2` in its file name, as the game will control this actor as a 2-frame sprite.
> You must return *some* image or the game will complain!
{.is-warning}

All animations for this actor are handled by the `HoldJudgment` metrics group on your theme. The following are the default animations from the fallback theme.

```ini
[HoldJudgment]
# System Direction
HoldJudgmentMissedHoldCommand=
HoldJudgmentLetGoCommand=finishtweening;visible,true;shadowlength,0;diffusealpha,1;zoom,1;y,-10;linear,0.8;y,10;sleep,0.5;linear,0.1;zoomy,0.5;zoomx,2;diffusealpha,0
HoldJudgmentHeldCommand=finishtweening;visible,true;shadowlength,0;diffusealpha,1;zoom,1.25;linear,0.3;zoomx,1;zoomy,1;sleep,0.5;linear,0.1;zoomy,0.5;zoomx,2;diffusealpha,0
```

# Functions

- `LoadFromMultiPlayer( MultiPlayer mp )`
Makes this HoldJudgment track progress of a specific `MultiPlayer` instead of its asigned `Player` or `MultiPlayer`.