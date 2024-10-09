---
title: OutFox Online Leaderboard Info
description: An Autoscroller actor that outputs the leaderboard info of the current song and difficulty from OutFox Online.
published: true
date: 2024-10-09T20:03:10.838Z
tags: outfoxonline
editor: markdown
dateCreated: 2024-08-29T18:56:34.928Z
---

# OFLeaderboardInfo

> This actor is only present on Project OutFox Alpha V pre043 onwards.
{.is-info}

> This actor is part of the OutFox Online system. For more information on this system, check out [OutFox Online System](/dev/outfoxonline).
{.is-info}

The OutFox Online Leaderboard Info actor is an [Dynamic ActorScroller](/en/dev/actors/actortypes/dynamicactorscroller) that outputs the information of the scores in a particular song - per-player - from the OutFox Online leaderboards.

![ofleaderboardfullexample.png](/dev/actors/ofleaderboardfullexample.png){.align-center}

## Attributes
| Name | Type | Action |
| :--- | :--- | :----- |
Player | int | Which player will this information be from? Note that its a number, so Player 1 is 0, and Player 2 is 1.
AutoUpdate | bool | Request a refresh everytime the player changes their difficulty or the song is changed. Disable this for manual updates.
TransformFunction |  function | The function that positions every item in the ActorScroller. For more information, check [Transforming the Scroller](/en/dev/actors/actortypes/actorscroller#transforming-the-scroller).

> Despite being a [Dynamic ActorScroller](/en/dev/actors/actortypes/dynamicactorscroller), it **does NOT** inherit the attributes from that actor.
{.is-info}

## Usage

The following is an example of how the actor is used. This will place it on the center of the screen. This is assuming there's a loop for each player's leaderboard actor.

```lua
Def.OFLeaderboardInfo {
		Condition=not GAMESTATE:IsHumanPlayer(pn),
		Player=pn == PLAYER_2 and 0 or 1,
		NumItemsToDraw=20,
		TransformFunction=function(self,offset,itemIndex,numItems)
					self:y(28*offset)
		end,
		InitCommand=function(self)
				self:Center()
		end,
    -- No song is currently selected. This is triggered when
    -- players are in the song group selection or sort picker.
		NoSongCommand=function (self)
				self:GetChild("Loading"):visible(false)
				self:GetChild("NoScoresText"):visible(false)
				self:GetChild("Scroller"):visible(false)
    end,
    -- A request has been made. Thus this command will be run.
    -- Use this to indicate the user that data is being fetched.
    LoadingCommand=function (self)
        self:GetChild("Loading"):visible(true)
        self:GetChild("NoScoresText"):visible(false)
        self:GetChild("Scroller"):visible(false)
    end,
    -- Data has been loaded and contains scores! Use this to hide elements
    -- that you used for loading.
    LoadedCommand=function (self)
        self:GetChild("Loading"):visible(false)
        self:GetChild("Scroller"):visible(true)
    end,
    -- Data was loaded but there are no scores in the leaderboard?
    -- That's when this command gets loaded. Use this to notify the player
    -- that this chart has no scores.
    NoScoresCommand=function (self)
        self:GetChild("Loading"):visible(false)
        self:GetChild("NoScoresText"):visible(true)
        self:GetChild("Scroller"):visible(false)
    end,

    Def.Sprite{
    		-- We'll use the loading circle to indicate the player that 
        -- the game is fetching the data.
        Texture=THEME:GetPathG("ScreenOutFoxOnlineLogin items/Player Loading","circle"),
        Name="Loading",
        InitCommand=function(self)
            self:y( 100 ):spin():zoom(0.4):effectmagnitude(0,0,720):visible(false)
        end
    },

    Def.BitmapText {
      Font="_Bold";
      InitCommand=function(self) self:y(100):maxwidth(240):diffuse(ColorLightTone(PlayerColor(pn))) end;
      OnCommand=function(self)
          self:visible(false)
          self:diffuseshift():effectcolor1(ColorLightTone(PlayerColor(pn))):effectcolor2(ColorLightTone(PlayerCompColor(pn))):effectperiod(4)
      end;
      Name="NoScoresText",
      Text="No scores have been submitted.";
    }
}
```

# Displaying the information
By default, the game will load the OFChartLeaderboard ScrollerItem actor present in your theme's Graphics folder, or the one provided in Fallback to display said information. The following is the fallback's version of the file.

```lua
return Def.ActorFrame{
	InitCommand=function(self)
		local fullWidth = 140
		-- self:GetChild("BG"):zoomto( BGWidth - 40, 26  ):diffuse(Color.Green)
		self:GetChild("Index"):x( -fullWidth ):maxwidth(36)
		self:GetChild("PlayerName"):x( -fullWidth*.85 ):zoom(0.8):halign(0):maxwidth(90)
		self:GetChild("Score"):x( fullWidth ):zoom(0.8):halign(1)
		self:GetChild("Date"):x(fullWidth*.55):zoom(0.8):maxwidth(140):halign(1)
	end,
	SetCommand=function(self,param)
		self:GetChild("Index"):settext(param.Index+1)
		if param.PlayerName then
			self:GetChild("PlayerName"):settext(param.PlayerName)
			self:GetChild("Date"):settext(param.Date)
			self:GetChild("Score"):settext(param.Score ~= nil and FormatPercentScore(param.Score) or "")
		else
			self:GetChild("PlayerName"):settext("")
			self:GetChild("Date"):settext("")
			self:GetChild("Score"):settext("")
		end
	end,
	--
	Def.BitmapText{ Name="Index", Text="11", Font="Common Normal" },
	Def.BitmapText{ Name="PlayerName", Text="-N/A-", Font="Common Normal" },
	Def.BitmapText{ Name="Date", Text="---", Font="Common Normal" },
	Def.BitmapText{ Name="Score", Text=FormatPercentScore(0), Font="Common Normal" },
}
```

The item receives a command by the name of "Set" which contains the following parameters depending if there is a score on its corresponding column or not.

| Name | Type | Description |
| :--- | :--- | :----- |
PlayerName | String | The name/username of the player who achieved the score.
Score | String | The score that this player has achieved. Depending on the current timing mode, it will output the value as either percentages, or a full number score.
Date | String | The date when this score took place.

> If a score isn't present on a particular column, the data will be `null`! Make sure to check if the data is available to avoid errors.
{.is-warning}

> The date provided from the server is in a timestamp format, so you'll need some conversion to present the date in a more readable format. The following example displays this date in a MM/DD/YY format.
> ```lua
> local year, month, day = param.Date:match("([%d]+)-([%d]+)-([%d]+)")
> self:GetChild("Date"):settext( string.format("%d/%d/%d", month, day, string.sub(""..year,2)) )
> ```
> {.is-info}

