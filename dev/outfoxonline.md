---
title: OutFox Online System
description: A rundown of the OutFox Online system, and how it can be implemented in themes.
published: false
date: 2024-08-29T20:46:49.843Z
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

<small>Theme is [pop-candy 2](https://josevarela.net/SMArchive/Themes/ThemePreview.php?Category=SM3.9&ID=pcd2) by LOLO, Hirose Madoka and [fether](https://fether.exblog.jp/), [ported to SM5 by Inorizushi](https://github.com/Inorizushi/popcandy2-SM5).</small>

> For info about this overlay, check out [the online overlay page](/en/dev/outfoxonline/onlineoverlay) for commands and examples.
{.is-info}

In addition to this system, it allow allows interoperability with [GrooveStats](https://groovestats.com) and [BoogieStats](https://boogiestats.andr.host/) (with an compatible theme that supports BoogieStats) for score submissions and general networking, as well as other systems that want a GET/POST request via a domain whitelist.

![ofgsinteropeval.png](/dev/outfoxonline/ofgsinteropeval.png){.align-center}

## Available actors

Actors for specific actions are available for fetching information from the server on your theme. Use these to integrate the system even further.

- [OFLeaderboardInfo *OutFox Online Leaderboard Info*](/en/dev/actors/actortypes/OFLeaderboardInfo)
{.links-list}