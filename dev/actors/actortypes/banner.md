---
title: Def.Banner
description: 
published: true
date: 2026-05-03T22:46:31.818Z
tags: 
editor: markdown
dateCreated: 2026-05-03T19:44:22.405Z
---

A song or course banner, meant for use with custom music wheels or any other place a song's banner would show up.

![banner-intro-demo.png](/resources/actors/banner/banner-intro-demo.png){.align-center}
<center>
	<small>Example of a banner, controlled by the game engine.</small>
</center>

You can also use this actor to display different kinds of banners ranging from Songs and its groups, Courses, Character cards and Icons, SortOrder types and Unlocks.

# Example

```lua
-- This example loads the banner for a random song.
Def.Banner{
	InitCommand=function(self)
		local song = SONGMAN:GetRandomSong()
		if not song then return end -- Bail if it cannot find a song.
	
		self:LoadFromSong( song )
	end
}
```

# Functions

- `scaletoclipped( float fWidth, float fHeight )`
Scales the banner to width `fWidth` and height `fHeight` clipping if the dimensions do not match.

- `LoadFromSong( Song s )`
Loads a Banner from a specified Song.

- `LoadFromCourse( Course s )`
Loads a Banner from a specified Course.

- `LoadFromCachedBanner( string sPath )`
Loads the banner from the cache based on `sPath`. Paths from `Song:GetBannerPath()` can work on this.

- `LoadIconFromCharacter( Character c )`
Loads an icon from the specified Character.

- `LoadCardFromCharacter( Character c )`
Loads the card image from the specified Character.

- `LoadBannerFromUnlockEntry( UnlockEntry pUE )`
Loads the banner from an UnlockEntry.

- `LoadBackgroundFromUnlockEntry( UnlockEntry pUE )`
Loads the background from an UnlockEntry.

- `LoadFromSongGroup( string groupName )`
Loads a Banner from a specified Song Group.

- `LoadFromSortOrder( SortOrder so )`
Loads a Banner from a specified SortOrder.

- `GetScrolling()`
Returns `true` if the Banner is currently scrolling. 

- `SetScrolling(bool bOn)`
Tells the banner if it should start scrolling.

- `GetPercentScrolling()`
Returns a `float` from 0 to 1 based on how far the banner as scrolled.