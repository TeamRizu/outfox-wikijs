---
title: Connecting to OutFox Online
description: This small guide will explain how to connect to OutFox online, and the ways you can connect through other Project OutFox powered machines.
published: true
date: 2025-05-13T04:11:56.975Z
tags: guide, outfoxonline
editor: markdown
dateCreated: 2025-03-25T19:30:19.338Z
---

Connecting to OutFox Online is a simple process, so let's go through the steps.

Before starting this guide, **make sure you make an [OutFox Online account](https://outfox.online/register)** so you get access to your own dashboard for the following steps.

# Step 1: Connecting the client

In order to access OutFox Online, you need to make your OutFox client connect to the server. You can do this by going to Options -> Network Options, and you'll see an `OutFox Online` option on the list.

![online-options-before-connect.png](/user-guide/online-options-before-connect.png)
<small>Theme is StepMania Ultimate, created by Luiszan, [ported to OutFox by Jose_Varela](https://github.com/JoseVarelaP/ultimate-of-theme).</small>

Just press enter, and you'll see its text update to `Connecting...` as it performs the handshake.

![onilne-options-connecting.png](/user-guide/onilne-options-connecting.png)

Once the connection has been established, or failed, you'll see a status on the bottom of your screen via the online overlay. If it's successful, then congrats, the client is now connected to the online component!

![online-options-overlay-connected.png](/user-guide/online-options-overlay-connected.png)

> Themes can change the look of this overlay to fit its own design, but the functionality is the same.
{.is-info}

# Step 2: Linking a profile

Now that the client is connected, it's time to link a local profile that you have to your account. You can have many profiles assigned to your profile, which you use to categorize your plays.

Maybe you want a profile that is for pure keyboard play, or one for playing on a real cabinet? You can just make a profile for it!

- Head to the `Profiles` section on the Options Menu to enter the profile selector.
- Choose the profile you want to link to your account.
- Select "Link Online Account".
> If the profile is already linked, it will say "Relink Online Account" instead.

This will ask for a Link Code, which you can find on your online dashboard. So head to https://outfox.online/dashboard to generate one.

Click on the "Link Additional" button on the dashboard, and a new section will appear with instructions on what to do next with this code.

![online-dashboard-step-click-additional.png](/user-guide/online-dashboard-step-click-additional.png)

Once you provide the link code, you'll see a confirmation message saying that the account is linked!

At this point, you can just play like normal. There's no more steps to do as the game will automatically login with your profile when you start playing. You'll see this as the login screen automatically shows up.

# Step 3: Playing outside of your computer / public cabinet

If you're not on the computer you made the profile in, there's nothing to worry about. **You can still use the same profile on other machines/cabinets that use Project OutFox!**

> By default, guest login is disabled. To turn it on, enable "Allow Online Guests" on the Network Options screen shown at the beginning of this guide.
{.is-info}

All you'll need to do is generate a Login Pin for your specific profile. This will be used on the guest login prompt.

![online-pin-login-screen.png](/user-guide/online-pin-login-screen.png)

To generate the pin, head over to https://outfox.online/dashboard/profiles (or scan the QR code that is provided on the guest login screen). This is where you'll see all the profiles you've linked to your account. Just choose which profile you want to use on the cabinet, click/press on "Generate Pin", and input the pin it gives you back on the machine!

![online-dashboard-profiles.png](/user-guide/online-dashboard-profiles.png)

![online-pin-success.png](/user-guide/online-pin-success.png)

And voila! Your profile has now been loaded on the cabinet, and you play as normal. All scores made during the session will be saved to your account, along with any mods you've setup during the session, which will be carried over for next time when you play on the same cabinet, or the computer you made the account on.

> Some themes might not respect the modifiers you saved on OutFox Online (like Simply Love)! Please keep this in mind if some settings don't transfer during load.
{.is-warning}