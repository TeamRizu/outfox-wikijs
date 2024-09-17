---
title: ScreenAttract
description: 
published: true
date: 2023-11-04T05:06:51.429Z
tags: 
editor: markdown
dateCreated: 2023-11-04T04:18:33.411Z
---

> Parent of [ScreenWithMenuElements](/en/dev/screens/ScreenWithMenuElements).
{.is-info}

A screen dedicated to present a timed screen, meant to showcase the game to bystanders to get interest to play.

When the screen is set to this class/fallback, the 

# Available Metrics
| Name | Default Value | Description |
| --- | --- | --- |
| BackGoesToStartScreen | true | Changes the behaviour for the back button to use the NextScreen insted of PrevScreen. |
| ResetGameState | false | Requests the game to reset GameState. |
| AttractVolume | 1 | Sets the starting volume for the screen. |

# Screen Behaviour

Upon entering the screen, if the screen is the same name as `Common::FirstAttractScreen`, an internal counter is increased that will determine if this attract loop will play its audio or not. By default, the attract sound frequency is set to `EveryTime`, which will make it always play audio when it enters these kinds of screens.