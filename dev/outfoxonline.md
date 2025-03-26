---
title: OutFox Online System
description: A rundown of the OutFox Online system, and how it can be implemented in themes.
published: true
date: 2025-03-26T17:47:28.108Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-29T19:04:10.028Z
---

# OutFox Online
> This system applies for Project Outfox Alpha V Pre043 and above.
{.is-info}

The Outfox Online system present in Project Outfox allows players to submit scores from their machines, use temporary profiles on public cabinets, check out their scores through an online portal, and more in the future.

## Features 
![ofevalsm4alpha.png](/dev/outfoxonline/ofevalsm4alpha.png){.align-center}
<small>Theme is StepMania 4's Alpha theme. Originally made by Chris Danford, Plaguefox. [Ported to SM5 by MadkaT182](https://github.com/MadkaT182/SM4Alpha).</small>

### Guest Profiles
It supports [guest profiles](/dev/outfoxonline/guestprofiles), so you can take your session and scores on the go, by just entering a 4-digit pin code assigned to your profile.

Settings like your modifiers and profile names are synced up automatically for the next time you play on a different location.

![oftokencyberia.png](/dev/outfoxonline/oftokencyberia.png){.align-center}
<small>Theme is [CyberiaStyle: LAST APPROACH](https://josevarela.net/SMArchive/Themes/ThemePreview.php?Category=StepMania%205&ID=CS8LA), by gl_yukt.</small>

### Interoperability with GrooveStats and BoogieStats
In addition to this system, it also allows interoperability with [GrooveStats](https://groovestats.com) and [BoogieStats](https://boogiestats.andr.host/) (with an compatible theme that supports BoogieStats) for score submissions and general networking, as well as other systems that want a GET/POST request via a domain whitelist. No need for an external client!

![ofgsinteropeval.png](/dev/outfoxonline/ofgsinteropeval.png){.align-center}
<small>Theme is Simply Love, made by hurtpiggypig and Mad Matt. Then converted to SM5 by quietly-turning, but now handled by teej and natano.</small>

## Implementation

For theme creators, you don't actually have to do anything to make OutFox Online work in your theme. All you need is your theme being able to either load [ScreenProfileLoad](/dev/screens/ScreenProfileLoad) or [ScreenSelectProfile](/dev/screens/ScreenSelectProfile) for login. The engine takes care of the rest.

Users can quickly connect to Outfox Online via the [ScreenOptionsNetwork](/dev/screens/ScreenOptionsNetwork) screen with a one-press `Connect` button.

![ofonlinenetworksettings.png](/dev/outfoxonline/ofonlinenetworksettings.png){.align-center}
<small>Theme is ITG: GrooveNights by DivinElegy (Now known as [peekingboo](https://www.twitch.tv/peekingboo)), [ported to Project Outfox by Jose_Varela](https://github.com/JoseVarelaP/SM5-GrooveNights).</small>

> Please note that if the user does not have the `Auto Connect To OutFox Online` (AutoConnectToServer) preference enabled, they'll need to navigate to [ScreenOptionsNetwork](/dev/screens/ScreenOptionsNetwork) to connect to Outfox Online on every boot. Otherwise, you're going to be have confused people wondering where the screen is.
>
> So please consider checking if your theme contains [ScreenOptionsNetwork](/dev/screens/ScreenOptionsNetwork) on your settings screen. 
{.is-info}


The system runs entirely on the engine and takes care of profile loading, score saving and profile syncing for you. All of these actions are reported on the screen via an overlay in a new layer in ScreenSystemLayer called `ScreenSystemLayer ofonline.lua`.

![ofonlineoverlaystatusdemo.png](/dev/ofonlineoverlaystatusdemo.png){.align-center}

<small>Theme is [pop-candy 2](https://josevarela.net/SMArchive/Themes/ThemePreview.php?Category=SM3.9&ID=pcd2) by LOLO, Hirose Madoka and [fether](https://fether.exblog.jp/), [ported to SM5 by Inorizushi](https://github.com/Inorizushi/popcandy2-SM5).</small>

> For info about this overlay, check out [the online overlay page](/en/dev/outfoxonline/onlineoverlay) for commands and examples.
{.is-info}

## Available actors

Actors for specific actions are available for fetching information from the server on your theme. Use these to integrate Outfox Online even further.

- [OFLeaderboardInfo *OutFox Online Leaderboard Info*](/dev/actors/actortypes/OFLeaderboardInfo)
{.links-list}

## Screens managed by the system

The system also brings in a new screen and expands on others to handle requests.

- [ScreenOutFoxOnlineLogin *OutFox Online Login Screen*](/dev/screens/ScreenOutFoxOnlineLogin)
- [ScreenProfileLoad *Standard Profile Loader*](/dev/screens/ScreenProfileLoad)
- [ScreenSelectProfile *Profile Picker Screen*](/dev/screens/ScreenSelectProfile)
- [ScreenEvaluation *Evaluation Screens*](/dev/screens/ScreenEvaluation)
{.links-list}