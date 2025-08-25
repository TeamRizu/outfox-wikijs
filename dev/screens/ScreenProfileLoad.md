---
title: ScreenProfileLoad
description: Responsible for automating the process of loading the profiles in a safe manner.
published: true
date: 2024-01-21T23:37:49.122Z
tags: 
editor: markdown
dateCreated: 2024-01-21T23:36:29.893Z
---

> Depends on [ScreenWithMenuElementsBlank]().
{.is-info}

This screen is responsible for automating the process of loading the profiles in a safe manner.

Only a metric is used here to toggle a setting:
```ini
# Can be true or false.
LoadEdits=true
```

`LoadEdits` will allow the game to load chart or song edits that originate from the user's memory card. Use that to toggle the behaviour.

By default the screen will act as a middle man to load up the contents, and takes about 0.1 seconds to finish processing all necessary information before moving on (Any extra time can be due to In/Out and/or actor animations).

# Calling the load manually

The screen contains a function to `Continue`, which will begin the process of loading the profiles. By using this logic, you can effectively create your ScreenProfileLoad screen and call the function on a different point in time via a command, rather than running the command as soon as the In transition is out.

```lua
SCREENMAN:GetTopScreen():Continue()
```

# Functions

## `Continue`

Runs the profile loading process and exits to the next screen when done.

```lua
OnCommand=function(self)
		SCREENMAN:GetTopScreen():Continue()
end
```

## `HaveProfileToLoad`

Returns true if there are any profiles available that need to be loaded.

```lua
OnCommand=function(self)
		local haveProfiles = SCREENMAN:GetTopScreen():HaveProfileToLoad()
    if haveProfiles then
				SCREENMAN:GetTopScreen():Continue()
    end
end
```