---
title: Outfox Online Login Screen
description: Login screen for Outfox Online
published: false
date: 2024-08-31T02:33:08.747Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-31T02:33:08.747Z
---

# ScreenOutfoxOnlineLogin
This screen takes care of loading online profiles, processing link token requests, invalid tokens, duplicates, and many other elements.

[imabge]

## Workflow

If no profiles are loaded at all, if the machine has the `AllowGuestProfiles` option enabled from [ScreenOptionsNetwork](/dev/screens/ScreenOptionsNetwork), each user will be prompted for a 4-digit Link code, which they can access from their Outfox Online dashboard. They can also use an NFC card that contains the token code for their profile to sign in as well.

[imabge]

If a user has a profile that is locally stored on the machine, the game will automatically attempt to login with their provided token. If this process fails, they'll be prompted with the same 4-digit screen as if there was no profile, where the difference is that upon successful sync, it updates the profile's token with the correct one for future logins.

[imabge]

## Receiving commands

Depending on which action is taken by the user or response received by the client, a command gets called.

### SendingLinkCodeCommand

Sent when the player has sent their 4-digit link code, and is in the process of logging in.

The following parameters are sent along with the command:

### PlayerLoginFailCommand

### PlayerLoginSuccessCommand

### TokenCodeChangedCommand