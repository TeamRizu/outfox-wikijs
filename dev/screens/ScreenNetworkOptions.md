---
title: ScreenNetworkOptions
description: Engine screen dedicated to network settings
published: true
date: 2025-05-13T04:42:51.700Z
tags: network, options, screen
editor: markdown
dateCreated: 2025-05-13T04:25:43.642Z
---

ScreenOptionsNetwork is the screen dedicated for options related with Networking, both on SMLan (the Lan-based multiplayer) and OutFox Online. It's its own dedicated class.

> All options here are handled by the engine, there's no way to modify them, but you can customize the look of them like any [OptionRow]().
{.is-info}

![online-options-before-connect.png](/user-guide/online-options-before-connect.png)

# Options

## Connection

This is the legacy functionality for SMLan, a LAN-Based multiplayer mode that connects to other SM/OutFox clients over a local network (or dedicated server that is running a compatible program that runs SMLan) to play together.

## Scoreboard

Related with `Connection`, this enables/disables the scoreboard that is shown on the opposite side of the player during gameplay, and shows the current rankings of the players throughout the song.

## OutFox Online

The dedicated connection button to connect to OutFox Online. Upon interacting with this button, messages are sent to the [OutFox Online Overlay](/dev/outfoxonline/onlineoverlay) to display the status of the connection.

## Auto Connect OutFox Online

An option to auto connect to OutFox Online when the game starts up. Disabled by default.

## Enable Discord Rich Presence
Enables Rich Presence functionality for Discord, which makes gameplay info be dislayed on your Discord profile while the game is on. These will update information depending on which screen you are.

> You must restart the game for this option to take effect.
{.is-info}

## Check For Updates

Dedicated for Non-Steam builds, this will make the game check for updates when the game starts up. If an update is available, a prompt will be shown on the title screen once per boot.