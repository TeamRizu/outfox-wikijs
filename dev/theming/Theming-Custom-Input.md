---
title: Custom Input
description: 
published: true
date: 2023-11-04T05:07:12.971Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:19:01.100Z
---

OutFox allows custom input to be managed by the theme itself. This allows you full sandboxed control of the game for the purposes of the theme.

---

# Implementing Input

There are a few ways to implement input, but the general action is to call `Screen:AddInputCallback( input function )` to the [ActorFrame](/en/dev/actors/actortypes/actorframe/_index) responsible for the input. This can be either a function or a module that will deal with listening and sending instructions back to the engine, that actors can then pick up to provide feedback.

## Module method (OutFox Alpha 4 and onwards)
```lua
-- In the actorframe, we just call the module to handle the input.
return Def.ActorFrame{
	OnCommand = function(self)
		-- The module needs the actor handle itself to send commands back to it, so we give `self` as the
		-- argument.
		SCREENMAN:GetTopScreen():AddInputCallback( LoadModule("Lua.InputSystem.lua")(self) )
	end,
	-- With this, the actorframe is now responsible for handling input and sending it to others.
	StartCommand = function(self)
		SCREENMAN:SystemMessage("I have pressed START!")
	end
}
```

## More direct method (Works on legacy versions of SM5)
```lua
-- This function will deal with a simple input set.
-- Let's make the input send a message when we press the player's assignated Start button.
-- event is sent over from InputCallback, and contains all the information needed to obtain input.
local function myCustomInput(event)
	-- First, let's verify that the input is being performed when pressing.
	-- There are three modes of input, which will be explain later in this chapter.
	if event.type == "InputEventType_FirstPress" then
		-- Ok, we have pressed the button once. Time to detect what button was pressed.
		if event.GameButton == "Start" then
			SCREENMAN:SystemMessage("I have pressed START!")
		end
	end
end

-- On this actorframe, we'll load the function.
return Def.ActorFrame{
	OnCommand = function(self)
		-- In this case, the function itself is now responsible of handling input and sending results to others.
		SCREENMAN:GetTopScreen():AddInputCallback( myCustomInput )
	end
}
```

# Anatomy of the event variable

When recieving input, you will be given a table by the name of `event`. It gives you base elements, which contain all the information you need to determine what the user has performed to then report back to the theme.

Name | Returns | Description |
:------------ | :------ | :---------- |
controller | string | The GameController the event was mapped to, which will depend on what controller was the input mapped to. Will return nil if the button is not mapped to any controller.
button | string | The semi-raw button that was pressed. This is what the button was mapped to by the keymap settings, but without the conversions that occur when [OnlyDedicatedMenuButtons](/en/user-guide/config/preferences#onlydedicatedmenubuttons) is true.  Will be empty if the button was not mapped.
type | string | The type of event. For more information, go to [Understanding Press Events](#understanding-press-events).
GameButton | string | The cooked button that was pressed. This is applied with mapping that occurs when [OnlyDedicatedMenuButtons](/en/user-guide/config/preferences#onlydedicatedmenubuttons) is true applied. This is nil for unmapped buttons.
PlayerNumber | PlayerNumber | The player that the input is mapped to. Can be nil if its not on either player.
MultiPlayer | MultiPlayer | A MultiPlayer enumerator that is mapped to the input, can be used on MultiPlayer matches, can be nil if the input is not mapped to any MultiPlayer. Do not confuse this to PlayerNumber.

## The Device Input Table

Inside this table, is another table called `DeviceInput` (can be accessed from `event.DeviceInput`), which are the raw details on the InputEvent the player has performed, which give the device the event has been performed on, the button that was pressed, if its still pressed, how long ago was the button pressed, a Z level counter for mouse input devices, as well as checks for joystick and mouse.

Name | Returns | Description |
:------------ | :------ | :---------- |
device | string | Type of the device, which will start with `"Device_"`, and then followed with a InputDeviceNames entry.
button | string | The button that was pressed, which will start with `"DeviceButton_"`, and then followed with the key correspondant on the device.
level | float | A floating point value for analog input.
z | float | A floating point value for determining what level is the mousewheel at.
down | bool | Determines if the button is down. This is a combination of level with a threshold. and debouncing applied.
ago | float | How long ago this input occurred, in seconds.
is_joystick | bool | Checks if the device is a joystick.
is_mouse | bool | Checks if the device is a mouse.

## Understanding Press Events

When calling an input, you have `event.type`, which is the moment where the button has been pressed, and contains three states:

<center>
  
```diagram
PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIyODFweCIgaGVpZ2h0PSIyMTJweCIgdmlld0JveD0iLTAuNSAtMC41IDI4MSAyMTIiIGNvbnRlbnQ9IiZsdDtteGZpbGUgaG9zdD0mcXVvdDtlbWJlZC5kaWFncmFtcy5uZXQmcXVvdDsgbW9kaWZpZWQ9JnF1b3Q7MjAyMy0wNS0xOVQyMDozMjozOC44NDZaJnF1b3Q7IGFnZW50PSZxdW90O01vemlsbGEvNS4wIChNYWNpbnRvc2g7IEludGVsIE1hYyBPUyBYIDEwLjE1OyBydjoxMDkuMCkgR2Vja28vMjAxMDAxMDEgRmlyZWZveC8xMTMuMCZxdW90OyBldGFnPSZxdW90O3V0VktLeXEtcUVmdzZIeFhLelNYJnF1b3Q7IHZlcnNpb249JnF1b3Q7MjEuMy4yJnF1b3Q7IHR5cGU9JnF1b3Q7ZW1iZWQmcXVvdDsmZ3Q7Jmx0O2RpYWdyYW0gaWQ9JnF1b3Q7UzdkYmktc2R3amVyaEQxOVJrT2wmcXVvdDsgbmFtZT0mcXVvdDtQw6FnaW5hLTEmcXVvdDsmZ3Q7NVZaYmE5c3dGUDQxaHZWbE9MNWszdU9XTk4wZUJtVVpkSDBxaW5Wc2k4bVNrZVhFM3ErZkZFbStwbDBabzR5T1FORDV6a1dYN3pzSGUrR21iRzhFcW9vdkhBUDFBaCszWHJqMWdpRDBRL1d2Z2M0QXEvZUpBWEpCc0lVR1lFOStnZ1Y5aXpZRVF6MEpsSnhUU2FvcG1ITEdJSlVUREFuQlQ5T3dqTlBwcmhYS1lRSHNVMFNYNkIzQnNqQm9FdnNEL2dsSVhyaWRWNzcxbE1nRlc2QXVFT2FuRVJSZWUrRkdjQzdOcW13M1FQWGJ1WGN4ZWJ0SHZQM0JCREQ1bklUQUpCd1JiZXpkdkdCTlZlcEhUSTVxbWV2bFoxWTE4dnFvU243cktuallFVkhMV3dGMTdXSlYvVkg0aFFwdjdncGcrbUE2aTdCY0UxYUErajgwVW5KMjVrRDBZS1kzMEJZcDRjcFZPNGg1L2ZtdTUvZVVuU05KOElaaDBQZGNLZmVwSUJMMkZVcTE5NlJVcWJCQ2x0UzZNMExwaGxOMUNKMGJZZ1JKbGlxOGxvTC9nSkZublNad3lKUW5Gd2dUOVNUT3h6aUQvaGhqQWl3blJ4QVMyaEZrQ2JrQlhvSVVuUXF4M3NDcHBYUHRZdTNUb0xVZ3NWZ3gwcG5USDdMeXp2dlNnd0xVd29yZ3NpRENDNEtZUFN3dy9FRTNrYkpTaWhTZjZmUXRoNGYzbFFVdGtkLzErbTFzclhzYnA5ZmJkaFMyN1p6QjFLbEhTZHE4SC91R3RMUGw4aFpzN1dMOWU0cVdtamNpaFVrelNDUnlzRkdSZ1FCUEJzS1N1aEUxOFJQTUNLQklrdU4wakZ5aXkrNXd5d21UZ3pLaXVUTG1qSnZiMkt4eDI4OEtoZEcwVUYvWUZUSnZzQ2gwVms5LzdXY0pLbG9JYWpaT3ZrSUZTQzdiM00yTVFrM241Y2k0ZXNYOW5yeGd2OGUvcDRjQ3F1RnhmaWpKNU9XUkxuaXBiVERlOCt3SC9JcUppOVl2U056NlB4N1UwWEpReC8vVW9PNEhzMnZwZDM4NnFHZUZvdFhmR3RUS0hENHpUZmp3clI1ZS93ST0mbHQ7L2RpYWdyYW0mZ3Q7Jmx0Oy9teGZpbGUmZ3Q7Ij48ZGVmcy8+PGc+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjI4MCIgaGVpZ2h0PSI1MCIgcng9IjcuNSIgcnk9IjcuNSIgZmlsbD0iI2RhZThmYyIgc3Ryb2tlPSIjNmM4ZWJmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KXNjYWxlKDAuOTk5OTk5OTk5OTk5OTk5OSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDElIiBoZWlnaHQ9IjEwMSUiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNXB4OyBtYXJnaW4tbGVmdDogMXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+PGRpdj5JbnB1dEV2ZW50VHlwZV9GaXJzdFByZXNzPC9kaXY+PGRpdj4oV2hlbiBwcmVzc2luZyB0aGUgYnV0dG9uIGZvciB0aGUgZmlyc3QgdGltZSk8YnIgLz48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTQwIiB5PSIyOSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXNpemU9IjEycHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPklucHV0RXZlbnRUeXBlX0ZpcnN0UHJlc3MuLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjxwYXRoIGQ9Ik0gMTQwIDUwIEwgMTQwIDczLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiNmNWY1ZjUiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTQwIDc4Ljg4IEwgMTM2LjUgNzEuODggTCAxNDAgNzMuNjMgTCAxNDMuNSA3MS44OCBaIiBmaWxsPSIjZjVmNWY1IiBzdHJva2U9IiNmNWY1ZjUiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjAiIHk9IjgwIiB3aWR0aD0iMjgwIiBoZWlnaHQ9IjUwIiByeD0iNy41IiByeT0iNy41IiBmaWxsPSIjZGFlOGZjIiBzdHJva2U9IiM2YzhlYmYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpc2NhbGUoMC45OTk5OTk5OTk5OTk5OTk5KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMSUiIGhlaWdodD0iMTAxJSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+SW5wdXRFdmVudFR5cGVfUmVwZWF0PGJyIC8+KFdoZW4gaG9sZGluZyB0aGUgYnV0dG9uKTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSIxNDAiIHk9IjEwOSIgZmlsbD0icmdiKDAsIDAsIDApIiBmb250LWZhbWlseT0iSGVsdmV0aWNhIiBmb250LXNpemU9IjEycHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPklucHV0RXZlbnRUeXBlX1JlcGVhdC4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHJlY3QgeD0iMCIgeT0iMTYwIiB3aWR0aD0iMjgwIiBoZWlnaHQ9IjUwIiByeD0iNy41IiByeT0iNy41IiBmaWxsPSIjZGFlOGZjIiBzdHJva2U9IiM2YzhlYmYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpc2NhbGUoMC45OTk5OTk5OTk5OTk5OTk5KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMSUiIGhlaWdodD0iMTAxJSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4NXB4OyBtYXJnaW4tbGVmdDogMXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwcHg7IHRleHQtYWxpZ246IGNlbnRlcjsiIGRhdGEtZHJhd2lvLWNvbG9ycz0iY29sb3I6IHJnYigwLCAwLCAwKTsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6IHJnYigwLCAwLCAwKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgb3ZlcmZsb3ctd3JhcDogbm9ybWFsOyI+SW5wdXRFdmVudFR5cGVfUmVsZWFzZTxiciAvPihXaGVuIGxpZnRpbmcgdGhlIGJ1dHRvbiBmcm9tIGJlaW5nIHByZXNzZWQpPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE0MCIgeT0iMTg5IiBmaWxsPSJyZ2IoMCwgMCwgMCkiIGZvbnQtZmFtaWx5PSJIZWx2ZXRpY2EiIGZvbnQtc2l6ZT0iMTJweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+SW5wdXRFdmVudFR5cGVfUmVsZWFzZS4uLjwvdGV4dD48L3N3aXRjaD48L2c+PHBhdGggZD0iTSAxNDAgMTMwIEwgMTQwIDE1My42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjZjVmNWY1IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0MCAxNTguODggTCAxMzYuNSAxNTEuODggTCAxNDAgMTUzLjYzIEwgMTQzLjUgMTUxLjg4IFoiIGZpbGw9IiNmNWY1ZjUiIHN0cm9rZT0iI2Y1ZjVmNSIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjxzd2l0Y2g+PGcgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ii8+PGEgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMCwtNSkiIHhsaW5rOmhyZWY9Imh0dHBzOi8vd3d3LmRyYXdpby5jb20vZG9jL2ZhcS9zdmctZXhwb3J0LXRleHQtcHJvYmxlbXMiIHRhcmdldD0iX2JsYW5rIj48dGV4dCB0ZXh0LWFuY2hvcj0ibWlkZGxlIiBmb250LXNpemU9IjEwcHgiIHg9IjUwJSIgeT0iMTAwJSI+VGV4dCBpcyBub3QgU1ZHIC0gY2Fubm90IGRpc3BsYXk8L3RleHQ+PC9hPjwvc3dpdGNoPjwvc3ZnPg==
```


  </center>

In order to filter what kind of input you want for specific actions, just include them in a if conditional check.
```lua
-- Let's say I want my start press to increase a variable and report it,
-- but also increase it while holding the button, but not when lifting it.

-- Initialize the variable to use as the counter.
local count = 0

local function myCustomInput(event)
	-- In this case, we'll check that the input is NOT Release, because that's the only InputEventType
	-- that we don't want verified on this check.
	if event.type ~= "InputEventType_Release" then
		-- Ok, we have pressed the button. time to count and report!
		if event.GameButton == "Start" then
			count = count + 1
			SCREENMAN:SystemMessage("The counter is now ".. count)
		end
	end
end

-- Now let's load the function to the actorframe.
return Def.ActorFrame{
	OnCommand = function(self)
		SCREENMAN:GetTopScreen():AddInputCallback( myCustomInput )
	end
}
```

# Mouse Input

Mouse input is supported on OutFox and earlier releases of SM5 via a MessageCommand system that determines which button was pressed to perform actions.

| Message Name | Segment of Mouse |
| :----------- | :--------------- |
MouseLeftClick | Left Mouse Click
MouseRightClick | Right Mouse Click
MouseMiddleClick | Middle Mouse Click
MouseThumb1 | Additional Mouse Click 1
MouseThumb2 | Additional Mouse Click 2
MouseWheelUp | Mouse Wheel Up
MouseWheelDown | Mouse Wheel Down

```lua
-- Example script to show a message when the left click of the mouse is pressed.
MouseLeftClickMessageCommand = function(self)
	SCREENMAN:SystemMessage("This is the left mouse click!")
end
```

> Starting on OutFox Alpha 4.9.7GG, these MessageCommands now contain an argument to determine if the mouse click was lifted or not.
{.is-info}


```lua
-- Example script to show a message when the left click of the mouse is pressed.
MouseLeftClickMessageCommand = function(self,param)
	if param.IsPressed then
		SCREENMAN:SystemMessage("This is the left mouse click being pressed!")
	else
		SCREENMAN:SystemMessage("This is the left mouse click being lifted!")
	end
end
```

# General Recommendations

## Remove the callback when leaving the screen

Upon adding the callback into the screen, it will be stored in memory for input to be processed, but won't be cleared when leaving, which can cause input problems on the long run in the session.

```lua
-- Using the manual function method
OffCommand = function(self)
	-- To remove it, just call the same function that was used to control the screen.
	SCREENMAN:GetTopScreen():RemoveInputCallback( myCustomInput )
end
```

```lua
-- Using the InputSystem module
-- Before anything, set the function inside the actor itself.
OnCommand = function(self)
	self.callback = LoadModule("Lua.InputSystem.lua")(self)
	SCREENMAN:GetTopScreen():AddInputCallback( self.callback )
end,
-- And now, when leaving, it will have the right actor to remove.
OffCommmand = function(self)
	SCREENMAN:GetTopScreen():RemoveInputCallback( self.callback )
end
```