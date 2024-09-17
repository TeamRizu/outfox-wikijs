---
title: Game Module: bongo
description: Details about the `bongo` mode supported by Project OutFox.
published: true
date: 2023-11-04T05:07:43.180Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:22:38.459Z
---

<!--
insert picture of game-play 
-->

## About

It parses files made for _taitai_ into a lane mode to play on a bongo based controller, or bongo based midi controller. One must hit the left or right bongo drum when it reaches the receptor, or clap your hands when the star appears. Scoring and timing windows are yet to be decided.

## History:

The parser support for the mode is currently actively developed, and the chart support will be aligned with the taiko simulator based parser support. We can parse .osu/.osz (Mode 1 taiko) and .tja files, although some of the scroll and time signature math needs to be concluded. As of alpha 4.18 the parsers are about 60% complete.

### Introduced:
#### Bongo (LeftDrum, RightDrum, clap):

First Seen:
 * Project OutFox LTS 4.18.0 / alpha 5.0.0-pre21 - ``(bongo-single)`` (26th October 2022)
 * Project OutFox LTS 4.18.0 / alpha 5.0.0-pre21 - ``(bongo-versus)`` (26th October 2022)

This mode is _parser specific_. It will only load and parse items designed for `taitai`.

The table below lists the supported files and their types that ``bongo`` supports, their key/button value and the original mode the parser is used for (if any).

File Type|Label|Original Mode|Key Values Supported|Notes 
------------|-------------|-------------|-------------|-------------|
 ``.osu`` | OTO | ``taitai`` | single | Mode 1 only (60% complete), (Mode 0 support coming soon!)
 ``.tja`` | TJA | ``taitai`` | single | Work in progress, about 60% complete.

## Gameplay

### Mechanics

``drum rolls`` 

You will need to ensure you hit the long note at least once for it to count!

``mines`` 

These notes should be avoided, as they will damage your life gauge

``big notes`` 

Are notes that require you to hit the both edges of the left bongo drum at the same time if it is blue, or both sides of the right bongo if it is red. These notes can be hit with one tap, but you will not get the full bonus. Hitting with one tap will _not_ drop your combo.


## Play Styles

## Grading / Accuracy

## Scoring

## Health Bar

## Modding

## Charting

## Controls

There are also notes which need to be hit a certain amount within a set time.

## Trivia
It is the second horizontal scroll game we support in _Project OutFox_.

_Written and Maintained with ♡ by Squirrel_