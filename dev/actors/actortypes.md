---
title: Actor Types
description: A list of the available actors in the game.
published: true
date: 2023-11-04T06:44:00.387Z
tags: actors, types
editor: markdown
dateCreated: 2023-05-16T06:13:45.791Z
---

StepMania (and it's many forks) use what's known as the [Actor model](https://en.wikipedia.org/wiki/Actor_model). OutFox inherits this behaviour. Everything in the engine is an Actor at its' very core.

Because everything is an actor, there are many types of actors, which are described below. Not everything listed is able to be created in Lua. Those that aren't will be noted as such. However, all of these can be found in the Lua environment.

> **A note on LoadActor()**
>
> This is a helper function that can be used to dynamically load an actor based on the file type. However, this should not be used as it is more resource intensive and can be easily avoided when the filetype is known. For loading external lua files, `loadfile(path)()` can be used, though the full path is required.
{.is-info}

# List of Actors

- [Def.Actor](./actortypes/actor) This is the base that everything derives from. Whatever an Actor can do, everything else can as well.
- [Def.ActorFrame](./actortypes/actorframe) ActorFrames can hold other actors. The Def. format is set up like any other lua table, allowing for creating actors in batches
- [Def.ActorFrameTexture](./actortypes/actorframetexture) Project items on an ActorFrame into a texture you can manipulate.
- [Def.ActorMultiTexture](./actortypes/actormultitexture) A Quad that allows for layering of multiple textures.
- [Def.ActorMultiVertex](./actortypes/actormultivertex) Allows for arbitrary polygons to be created.
- [Def.ActorProxy](./actortypes/actorproxy) Render another actor without worrying about duplicating logic
- [Def.ActorScroller](./actortypes/actorscroller) An ActorFrame that acts as a scroller, allowing for a selection-styled menu with choices and animations.
- [Def.Banner](./actortypes/banner) A song or course banner.
- [Def.BGAnimation](./actortypes/bganimation) A compatibility actor class that allows you to run older .ini files for background animations.
- [Def.BitmapText](./actortypes/bitmaptext) Render text in the game.
- [Def.BPMDisplay](./actortypes/bpmdisplay) A general-purpose BPM display that cycles between two values.
- [Def.ControllerStateDisplay](./actortypes/controllerstatedisplay) A more visual style of Test Input.
- [Def.ComboGraph](./actortypes/combograph) Shows the combos that were held throughout the song.
- [Def.CourseContentsList](./actortypes/coursecontentslist) A list of the songs for a given course.
- [Def.DeviceList](./actortypes/devicelist) Lists connected devices.
- [Def.DynamicActorScroller](./actortypes/dynamicactorscroller) A runtime version of ActorScroller.
- [Def.GradeDisplay](./actortypes/gradedisplay) Showcase the grade to the player.
- [Def.HelpDisplay](./actortypes/helpdisplay) Display help text to the player via blinking text
- [Def.InputList](./actortypes/inputlist) Show the current buttons being pressed.
- [Def.MemoryCardDisplay](./actortypes/memorycarddisplay) Show which player has a memory card inserted
- [Def.MeterDisplay](./actortypes/meterdisplay) An auto-updating meter that tracks song progress.
- [Def.Model](./actortypes/model) Render 3D models in the game.
- [Def.NoteField](./actortypes/notefield) The playfield.
- [Def.PercentageDisplay](./actortypes/percentagedisplay) A BitmapText that renders the player's score in percentage.
- [Def.RollingNumbers](./actortypes/rollingnumbers) A BitmapText that animates the transition of a number to the next.
- [Def.Quad](./actortypes/quad) Arbitrary squares.
- [Def.ScoreDisplayAliveTime](./actortypes/scoredisplayalivetime)
- [Def.ScoreDisplayCalories](./actortypes/scoredisplaycalories)
- [Def.SongBPMDisplay](./actortypes/songbpmdisplay)
- [Def.SongMeterDisplay](./actortypes/songmeterdisplay)
- [Def.Sound](./actortypes/sound) Play sounds on demand.
- [Def.Sprite](./actortypes/sprite) Project images, sprites and video.
- [Def.StepsDisplay](./actortypes/stepsdisplay) 
- [Def.TextBanner](./actortypes/textbanner) An ActorFrame that contains information about a given song.
- [Def.WorkoutGraph](./actortypes/workoutgraph) A graph ""showing the calories burned over time during a workout"".
{.links-list}

# Pre-generated Actor Types

The following actors cannot be generated with Lua, but instead can be accessed based on the current screen with `self:GetChild`.

- [LifeMeter](./actortypes/lifemeter) Shows how much life a Player currently has.
- [HoldJudgment](./actortypes/holdjudgment) The judgment that shows up on a column when dropping or clearing a hold & roll.
- [MusicWheel](./actortypes/musicwheel) The wheel used to select songs in ScreenSelectMusic or courses in ScreenSelectCourse.
- [NoteColumnRenderer](./actortypes/NoteColumnRenderer) This is a dedicated actor for a column in the notefield, and can be treated like any other actor.
- [Player](./actortypes/player) The entirety of the playfield. Holds the judgment, hold judgments, combo and the NoteField.
{.links-list}

## Banner

A song or course banner, meant for use with custom music wheels or any other place a song's banner would show up.

## ComboGraph

Shows the combos that were held throughout the song, with combo breaks separating the blocks, and the largest combo being colored.

```lua
Def.ComboGraph{
	InitCommand=function(self)
		-- Load the MetricsGroup that will create the basis for the graph.
		self:Load("ComboGraph")
		local playerStageStats = STATSMAN:GetCurStageStats():GetPlayerStageStats(player)
		local stageStats = STATSMAN:GetCurStageStats()
		-- Data is graph from the current stage stats and the player's stats.
		self:Set(stageStats, playerStageStats)
	end
}
```

## CourseContentsList

A list of the songs for a given course. Can be given a limit for how many songs to show and how many to show at a time.

## DeviceList

Displays a list of all input devices. Often, Keyboard and Mouse will be listed.

Functions like most other BitmapText actors.

## DifficultyIcon

A Sprite-type actor that shows a different icon for each difficulty.

If there number of frames are double the amount of difficulties available in the engine, the player number will offset the icon shown.

## FadingBanner

A song or course banner that can fade between the banner for different songs or courses.

Often seen in ScreenSelectMusic.

## GraphDisplay

Displays a graph containing data points for a player's life throughout the stage.

Settings for a GraphDisplay can only be defined through metrics.
<!--TODO: Maybe we could make a different load function to allow for one to be set up through lua and not metrics???-->

```lua
Def.GraphDisplay{
	InitCommand=function(self)
		-- Load the MetricsGroup that will create the basis for the graph.
		self:Load("GraphDisplay")
		local playerStageStats = STATSMAN:GetCurStageStats():GetPlayerStageStats(player)
		local stageStats = STATSMAN:GetCurStageStats()
		-- Data is graph from the current stage stats and the player's stats.
		self:Set(stageStats, playerStageStats)
	end
}
```

## GrooveRadar

A recreation of the five-point "Groove Radar" from DDR. Can take arbitrary values as well as the song's radar values.
Note that the visual aspect of the GrooveRadar depends on metrics set on the `GrooveRadar` metrics group, and the 
GrooveRadar graphics set.
<!--TODO: Do we mention what the radar values are?-->
```lua
Def.GrooveRadar {
	InitCommand=function(self)
		-- Let's use random values to fill the graph.
		self:SetFromValues({1,0.5,0.8,0.4,1})
	end
}
```

## HoldJudgment

Often found in Player, though there is no way to grab the ones that are in Player.

The judgment that shows up on a column when dropping or clearing a hold & roll.

There is an extra function to allow tracking the hold judgments from a MultiPlayer.

```lua
Def.HoldJudgment{
	File=THEME:GetPathG("Hold","Judgment"),
	InitCommand=function(self)
		
	end
}
```

## LogDisplay

This is an actor type created from _fallback's scripts.

Displays lua script errors as they happen. Most themers shouldn't need to touch this.

## LifeMeter

Cannot be created from lua, but can be grabbed from ScreenGameplay.

Often used in gameplay screens. This shows how much life a Player currently has.

## LifeMeterBattery

Cannot be created from lua.

Often used in gameplay screens. This shows how many more mistakes a player is allowed before failing.

## MemoryCardDisplay

Shows the current state of a player's inserted memory card. Made of images, with one for each state.

```lua
Def.MemoryCardDisplay{
	PlayerNumber=PLAYER_1
}
```

## MenuTimer

Cannot be created from lua, but is a part of every screen that inherits from ScreenWithMenuElements.

A Timer that counts down and proceeds to the next screen when it reaches 0.

## MeterDisplay

Shows the current progress of an operation. It appears to only show the progress as 50%.
<!--TODO: Is there a way to set the percentage?-->

## ModIconRow

Shows icons for the currently set modifiers of a player.

Not all modifiers have an icon, and the settings can only be set through metrics.

## MusicWheel

Cannot be created from lua, but can be grabbed from the TopScreen.

The wheel used to select songs in ScreenSelectMusic or courses in ScreenSelectCourse.

## NoteColumnRenderer

Cannot be created from lua, but can be grabbed from NoteField.

This is a dedicated actor for a column in the notefield, and can be treated like any other actor.

## OptionRow

Cannot be created from lua.

Often seen in options screens, this actor allows for picking and choosing various options for a given setting.

## PaneDisplay

Shows the number of steps, jumps, holds, rolls, mines, hands, lifts, fakes, the machine profile's highscore & name and the current profile's high score for a given chart.

Settings must be defined through Metrics.

## Player

Cannot be created from lua, but is part of ScreenGameplay

The entirety of the playfield. Holds the judgment, hold judgments, combo and the NoteField.

## Quad

An arbitrary rectangle. Acts like a Sprite with a blank texture.

```lua
-- Generate a 64 x 64 rectangle on the center of the screen, and color it Yellow.
Def.Quad{
	OnCommand=function(self)
		self:zoomto( 64,64 ):diffuse( Color.Yellow )
		:xy( SCREEN_CENTER_X, SCREEN_CENTER_Y )
	end
}
```

## Screen

Can't be defined in lua, but can be defined in a theme's metrics.

A screen the theme can go to. There are screens for gameplay, selecting music, pre-gameplay, etc. Each screen has a background, underlay, overlay and decorations that can be used.

<!--TODO: Do I note down the other ScreenTypes listed in luadocs?-->

## StepsDisplay

Displays the data for a given chart. Can show difficulty number, description, credit, if it's autogen and steps type.

Currently, all setings are done through metrics.

## StepsDisplayList

Shows the list of steps available for a given song.

The name given determines what metrics group to load from.

```lua
Def.StepsDisplayList {
	Name="StepsDisplayList",
	-- These define the cursor the players will be controlling. The rest of the elements are defined
	-- by the metrics.
	CursorP1=Def.Actor{},
	CursorP2=Def.Actor{},
	CursorP1Frame=Def.Actor{},
	CursorP2Frame=Def.Actor{}
}
```

## TextBanner

A "Banner" that contains the song name, artist and subtitle.

Usually seen in the CourseContentsList of ScreenSelectMusic or the ScrollerItem in ScreenHighScores.

```lua
-- This example uses this set from a CourseContentsList, hence the SetSong command.
Def.TextBanner {
	InitCommand=function(self)
		self:Load("TextBannerCourse"):SetFromString("", "", "", "", "", "")
	end,
	SetSongCommand=function(self, params)
		if params.Song then
			self:SetFromSong( params.Song )
			self:diffuse(color("#FFFFFF"))
		else
			self:SetFromString( "??????????", "??????????", "", "", "", "" )
			self:diffuse( color("#FFFFFF") )
		end
	end
}
```

## WheelBase

Cannot be created from lua.

A base class for wheels. Currently, the MusicWheel and RoomWheel inherit from this.

## WheelItemBase

Cannot be created from lua.

A base class for items residing in wheels. MusicWheelItems inherit from this.