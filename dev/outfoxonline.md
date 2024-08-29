---
title: OutFox Online System
description: A rundown of the OutFox Online system, and how it can be implemented in themes.
published: false
date: 2024-08-29T21:45:37.082Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-29T19:04:10.028Z
---

# OutFox Online
> This system applies for Project Outfox Alpha V Pre043 and above.
{.is-info}

The OutFox Online system present in Project OutFox allows player to submit scores from their machines, use temporary profiles on public cabinets, and etc.

![ofevalsm4alpha.png](/dev/outfoxonline/ofevalsm4alpha.png){.align-center}
<small>Theme is StepMania 4's Alpha theme. Originally made by Chris Danford, Plaguefox. [Ported to SM5 by MadkaT182](https://github.com/MadkaT182/SM4Alpha).</small>

It supports [guest profiles](/dev/outfoxonline/guestprofiles), so you can take your session and scores on the go, by just entering a 4-digit pin code assigned to your profile.

![oftokencyberia.png](/dev/outfoxonline/oftokencyberia.png)
<small>Theme is [CyberiaStyle: LAST APPROACH](https://josevarela.net/SMArchive/Themes/ThemePreview.php?Category=StepMania%205&ID=CS8LA), by gl_yukt.</small>

In addition to this system, it allow allows interoperability with [GrooveStats](https://groovestats.com) and [BoogieStats](https://boogiestats.andr.host/) (with an compatible theme that supports BoogieStats) for score submissions and general networking, as well as other systems that want a GET/POST request via a domain whitelist. No need for an external client!

![ofgsinteropeval.png](/dev/outfoxonline/ofgsinteropeval.png){.align-center}
<small>Theme is Simply Love, made by hurtpiggypig and Mad Matt. Then converted to SM5 by quietly-turning, but now handled by teej and natano.</small>

## Implementation

For theme creators, you don't actually have to do anything to make OutFox Online work in your theme. All you need is your theme being able to either load [ScreenProfileLoad]() or [ScreenSelectProfile]() for login. The engine takes care of the rest.

The system runs entire in the engine and takes care of profile loading, score saving and profile syncing for you. All of these actions are reported on the screen via an overlay in a new layer in ScreenSystemLayer called `ScreenSystemLayer ofonline.lua`.

![ofonlineoverlaystatusdemo.png](/dev/ofonlineoverlaystatusdemo.png){.align-center}

<small>Theme is [pop-candy 2](https://josevarela.net/SMArchive/Themes/ThemePreview.php?Category=SM3.9&ID=pcd2) by LOLO, Hirose Madoka and [fether](https://fether.exblog.jp/), [ported to SM5 by Inorizushi](https://github.com/Inorizushi/popcandy2-SM5).</small>

> For info about this overlay, check out [the online overlay page](/en/dev/outfoxonline/onlineoverlay) for commands and examples.
{.is-info}

## Available actors

Actors for specific actions are available for fetching information from the server on your theme. Use these to integrate the system even further.

- [OFLeaderboardInfo *OutFox Online Leaderboard Info*](/en/dev/actors/actortypes/OFLeaderboardInfo)
{.links-list}