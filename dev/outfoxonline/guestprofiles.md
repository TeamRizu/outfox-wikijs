---
title: Guest Profiles in Outfox Online
description: A summary on how Guest profiles work for Outfox Online
published: false
date: 2024-08-31T01:04:35.161Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-29T21:57:35.953Z
---

# Guest Profiles in Outfox Online

Guest profiles in Project Outfox behave as empty profiles, which are ready for all kinds of interactions. For Outfox Online, these are used to allow content to be synced across your profiles and machines.

If the `Allow Guests` option is enabled from the Network settings screen, any player who doesn't have a player assigned beforehand is given the option to login to their OutFox Online profile via an Auth code which they can retrieve from their Outfox Online dashboard.

![oftokenguests.png](/dev/outfoxonline/oftokenguests.png){.align-center}
<small>Theme is Simply Love, made by hurtpiggypig and Mad Matt. Then converted to SM5 by quietly-turning, but now handled by teej and natano.</small>

> If your theme has custom theme preferences that are saved in a special file on the profile, these won't appear as it will be treated like a new profile.
{.is-info}

> If your theme processes modifiers in a different way than the engine upon loading a profile, please add an exception so they're not overwritten, as guest profiles are now automatically assigned the `Online` ProfileType.
{.is-warning}

