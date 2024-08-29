---
title: OutFox Online System
description: A rundown of the OutFox Online system, and how it can be implemented in themes.
published: false
date: 2024-08-29T19:04:10.028Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-29T19:04:10.028Z
---

# OutFox Online
The OutFox Online system present in Project OutFox allows player to submit scores from their machines, use temporary profiles on public cabinets, and etc.

> This system applies for Project Outfox Alpha V Pre043 and above.
{.is-info}

## Implementation

For theme creators, you don't actually have to do anything to make OutFox Online work in your theme. The system runs entire in the engine and takes care of profile loading, score saving and profile syncing for you. All of these actions are reported on the screen via an overlay in a new layer in ScreenSystemLayer called `ScreenSystemLayer ofonline.lua`.

![ofonlineoverlaystatusdemo.png](/dev/ofonlineoverlaystatusdemo.png){.align-center}

> For info about this overlay, check out [the online overlay page](/en/dev/outfoxonline/statusoverlay) for commands and examples.
{.is-info}

TODO: add info about its functionality.

## Available actors

Actors for specific actions are available for fetching information from the server on your theme. Use these to integrate the system even further.

- [OFLeaderboardInfo *OutFox Online Leaderboard Info*](/en/dev/actors/actortypes/OFLeaderboardInfo)
{.links-list}