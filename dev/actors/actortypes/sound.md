---
title: Sound
description: Used to play sound files outside of the common theme sound effects and the simfile's song itself.
published: true
date: 2024-01-21T22:26:21.227Z
tags: actor, sound
editor: markdown
dateCreated: 2023-05-16T06:16:07.300Z
---

Used to play sound files outside of the common theme sound effects and the simfile's song itself.

Removes the need to use `SOUND:PlayOnce()`, as it allows for pre-loading the sound file at the start instead of loading (possibly many times) and playing the sound mid-screen.

```lua
Def.Sound{
	-- Load the audio called MySound, which is a ogg file in this example.
	File="MySound.ogg",
	-- Lets the audio pane from side to side. Useful for audios that need to play on a specific player side.
	SupportPan=true,
	-- Allows the audio to change rate and pitch.
	SupportRateChanging=false,
	-- this assigns the audio to be an Action, which is a flag for sounds that allows it to be muted by the player,
	-- with the use of the Mute Actions key (Default to "Pause").
	IsAction=true,
	OnCommand=function(self)
		-- When creating the actor, sound will not play automatically, so you need to use the play command
		-- to perform such action.
		self:play()

		-- If the audio has the "(loop)" flag set on its filename, it will loop infinetly. So to top it, use the
		-- appropiate command.
		self:stop()

		-- If the sound needs to be paused on a particular frame, and not to reset, use the pause command.
		self:pause( true ) -- Use false to resume it.
	end
}
```

# Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
File | string | The audio file to be utilized for this Sound.
SupportPan | bool | Lets the audio pane from side to side. Useful for audios that need to play on a specific player side.
SupportsRateChanging | bool | Allows the audio to change rate and pitch.
IsAction |  bool | Assigns the audio to become a Sound Effect, which allows it to be muted by the player if they so choose from the Effect Volume [Introduced in Project OutFox 4.9.9](/en/releases/A499) or by the [MuteActions](/en/user-guide/config/preferences#muteactions) preference.
Precache | bool | Tells the engine to store this sound on memory for later use.

# Controlling Sound

The Def.Sound actor is part of RageSound, another component in the engine that deals with audio, and they both work together to provide playback of said sounds. That said, in order to control specific elements from them, you must understand how to access them.

Only using commands directly inside Def.Sound will provide commands related to the sound actor; to use commands related to its RageSound component, you must `get()` the component.

```lua
-- To control actions like volume, you need to access the ActorSound's RageSound, by using the get function.
local MyRageSound = self:get()
```

With this object obtained, you can control elements like the sound's position, volume, pitch and speed.
Note that some components need some flags to be enabled which have been pointed out as commments alongside them.
```lua
-- This function will return the value for the Def.Sound's RageSound component, which allows for expanded
-- controls.
local MyRageSound = self:get()

MyRageSound:volume( 0.5 ) -- Changes volume (0 to 1).
MyRageSound:pitch( 1.2 ) -- Requires SupportRateChanging to work.
MyRageSound:speed( 1.4 ) -- Requires SupportRateChanging to work.
```

## Adjusting Properties

With RageSound, you have access to different kinds of sound properties to determine how you want your sound to be played.

```lua
MyRageSound:SetParam( "Property Name", Value )
```

The available properties to change are detailed on the table below.

| Name of Property | Description |
| :--------------- | :---------- | 
Speed | Determines how fast the speed will play.
Pitch | Determines the notation for the sound's tune.
StartSecond | Sets the initial time of the sound to play.
LengthSeconds | Sets the length of the sound.
FadeInSeconds | How long the audio transition to full volume at the start.
FadeSeconds / FadeOutSeconds | How long the audio transition to silence at the end.
Volume | How loud will the sound be (0 to 1 value).

--- 

<!--Pan | (Requires the SupportRateChanging flag), sets the direction of the audio to go through, like the left or right channel.-->