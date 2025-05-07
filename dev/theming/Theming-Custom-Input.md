---
title: Custom Input
description: 
published: true
date: 2025-05-07T06:06:30.229Z
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
PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHN0eWxlPSJiYWNrZ3JvdW5kOiB0cmFuc3BhcmVudDsgYmFja2dyb3VuZC1jb2xvcjogdHJhbnNwYXJlbnQ7IGNvbG9yLXNjaGVtZTogbGlnaHQgZGFyazsiIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIyODFweCIgaGVpZ2h0PSIyMTJweCIgdmlld0JveD0iLTAuNSAtMC41IDI4MSAyMTIiIGNvbnRlbnQ9IiZsdDtteGZpbGUgaG9zdD0mcXVvdDtlbWJlZC5kaWFncmFtcy5uZXQmcXVvdDsgYWdlbnQ9JnF1b3Q7TW96aWxsYS81LjAgKE1hY2ludG9zaDsgSW50ZWwgTWFjIE9TIFggMTAuMTU7IHJ2OjEzOC4wKSBHZWNrby8yMDEwMDEwMSBGaXJlZm94LzEzOC4wJnF1b3Q7IHZlcnNpb249JnF1b3Q7MjYuMi4xNCZxdW90OyZndDsmbHQ7ZGlhZ3JhbSBpZD0mcXVvdDtTN2RiaS1zZHdqZXJoRDE5UmtPbCZxdW90OyBuYW1lPSZxdW90O1DDoWdpbmEtMSZxdW90OyZndDszVlpMYjlzd0RQNDFCdGJMa1BpUlpjY3RTYnNkQmhUTGdLNm5RckZvVzVnc0diS2NPUHYxa3lMSmx1MWtMWXFoR0hJeHhJOHZpUjlKT0loV1pYc25VRlY4NHhob0VNNXdHMFRySUF6RDVLUDZhdUJvZ2RuTUFMa2cyRUR6SHRpUzMyQkJaOVlRRFBYQVVISk9KYW1HWU1vWmcxUU9NQ1FFUHd6Tk1rNkhXU3VVd3dUWXBvaE8wUWVDWldIUVpUTHI4UzlBOHNKbG5ydjNsY2daVzZBdUVPWUhENG8yUWJRU25FdHpLdHNWVUYwN1Z4ZmpkM3RCMjExTUFKTXZjUWlOd3g3UnhyNHRDQmRVdVg3R1pLK091VDUrWlZVak4zc1Y4c2V4Z3FkYkltcDVMNkN1bmEySzc1bWZpZkR1b1FDbUw2YTlDTXMxWVFXbzc2NlJrck1UQjZJRE01MUFTNlNFR3hkdEo4Ynh4MWxQOVpSSFI1TGdEY09nM3psWDZrTkJKR3dybEdydFFYV2x3Z3BaVXF2T0NLVXJUdFVsdEcrRUVTeXpWT0cxRlB3WGVKcEZ1b1JkMXVYeksyMkx2d2Nob2ZVZ1cvazc0Q1ZJY1ZRbTdhanQ3UmhFVGo3MFRSVXVMVlo0RGVVYURkayt6cnZRUGRYcVlOayt6M3gwaHZsUkJZSGhUM3BhbEpSU3BJaExoMFhyS3p4VEVyUkUvdFRuOTRtVkhxMmRQcTliejJ4OWRBSlR0L2FjdFBqbzYzcTNrK1Q4TGhhLzVvMUlZZERiRW9rY3JGVnNJTUNEK1o0UzVCR1EvS1grQWlpU1pEL2NDdWRJc1JudU9XR3k1ejhlOHovbTFiekdldmxUUEFvVXhjTkFYV0FYeU5SZ0V1alVJOTJ6WDlRMjhhUnRSdHZoTzFTQTVIUnEzUW9vMUxLZGJvQ2JheGpmNVJ1T2IvSThEeFJRRFplSm9DU1Q1MWV4NEtXV3dXaFBPeHZ3TlRBVUw5NlFvY1hWTDloNHVtQ1QvMnJCZGd2VlRlaUgxeTdZVWFCNC9xOFdyQkw3dnoxajN2OHlSNXMvJmx0Oy9kaWFncmFtJmd0OyZsdDsvbXhmaWxlJmd0OyI+PGRlZnMvPjxnPjxnIGRhdGEtY2VsbC1pZD0iMCI+PGcgZGF0YS1jZWxsLWlkPSIxIj48ZyBkYXRhLWNlbGwtaWQ9IjIiPjxnPjxyZWN0IHg9IjAiIHk9IjAiIHdpZHRoPSIyODAiIGhlaWdodD0iNTAiIHJ4PSI3LjUiIHJ5PSI3LjUiIGZpbGw9IiNkYWU4ZmMiIHN0eWxlPSJmaWxsOiBsaWdodC1kYXJrKHJnYigyMTgsIDIzMiwgMjUyKSwgcmdiKDI5LCA0MSwgNTkpKTsgc3Ryb2tlOiBsaWdodC1kYXJrKHJnYigxMDgsIDE0MiwgMTkxKSwgcmdiKDkyLCAxMjEsIDE2MykpOyIgc3Ryb2tlPSIjNmM4ZWJmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjxnPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNXB4OyBtYXJnaW4tbGVmdDogMXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7IGNvbG9yOiAjMDAwMDAwOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogJnF1b3Q7SGVsdmV0aWNhJnF1b3Q7OyBjb2xvcjogbGlnaHQtZGFyaygjMDAwMDAwLCAjZmZmZmZmKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5JbnB1dEV2ZW50VHlwZV9GaXJzdFByZXNzPC9kaXY+PGRpdj4oV2hlbiBwcmVzc2luZyB0aGUgYnV0dG9uIGZvciB0aGUgZmlyc3QgdGltZSk8YnIgLz48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTQwIiB5PSIyOSIgZmlsbD0ibGlnaHQtZGFyaygjMDAwMDAwLCAjZmZmZmZmKSIgZm9udC1mYW1pbHk9IiZxdW90O0hlbHZldGljYSZxdW90OyIgZm9udC1zaXplPSIxMnB4IiB0ZXh0LWFuY2hvcj0ibWlkZGxlIj5JbnB1dEV2ZW50VHlwZV9GaXJzdFByZXNzLi4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48L2c+PC9nPjxnIGRhdGEtY2VsbC1pZD0iMyI+PGc+PHBhdGggZD0iTSAxNDAgNTAgTCAxNDAgNzMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3R5bGU9InN0cm9rZTogbGlnaHQtZGFyayhyZ2IoMCwgMCwgMCksIHJnYigyNTUsIDI1NSwgMjU1KSk7IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0MCA3OC44OCBMIDEzNi41IDcxLjg4IEwgMTQwIDczLjYzIEwgMTQzLjUgNzEuODggWiIgZmlsbD0iIzAwMDAwMCIgc3R5bGU9ImZpbGw6IGxpZ2h0LWRhcmsocmdiKDAsIDAsIDApLCByZ2IoMjU1LCAyNTUsIDI1NSkpOyBzdHJva2U6IGxpZ2h0LWRhcmsocmdiKDAsIDAsIDApLCByZ2IoMjU1LCAyNTUsIDI1NSkpOyIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9nPjxnIGRhdGEtY2VsbC1pZD0iNCI+PGc+PHJlY3QgeD0iMCIgeT0iODAiIHdpZHRoPSIyODAiIGhlaWdodD0iNTAiIHJ4PSI3LjUiIHJ5PSI3LjUiIGZpbGw9IiNkYWU4ZmMiIHN0eWxlPSJmaWxsOiBsaWdodC1kYXJrKHJnYigyMTgsIDIzMiwgMjUyKSwgcmdiKDI5LCA0MSwgNTkpKTsgc3Ryb2tlOiBsaWdodC1kYXJrKHJnYigxMDgsIDE0MiwgMTkxKSwgcmdiKDkyLCAxMjEsIDE2MykpOyIgc3Ryb2tlPSIjNmM4ZWJmIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjxnPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxzd2l0Y2g+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyNzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDVweDsgbWFyZ2luLWxlZnQ6IDFweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyBjb2xvcjogIzAwMDAwMDsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6ICZxdW90O0hlbHZldGljYSZxdW90OzsgY29sb3I6IGxpZ2h0LWRhcmsoIzAwMDAwMCwgI2ZmZmZmZik7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPklucHV0RXZlbnRUeXBlX1JlcGVhdDxiciAvPihXaGVuIGhvbGRpbmcgdGhlIGJ1dHRvbik8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTQwIiB5PSIxMDkiIGZpbGw9ImxpZ2h0LWRhcmsoIzAwMDAwMCwgI2ZmZmZmZikiIGZvbnQtZmFtaWx5PSImcXVvdDtIZWx2ZXRpY2EmcXVvdDsiIGZvbnQtc2l6ZT0iMTJweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+SW5wdXRFdmVudFR5cGVfUmVwZWF0Li4uPC90ZXh0Pjwvc3dpdGNoPjwvZz48L2c+PC9nPjxnIGRhdGEtY2VsbC1pZD0iNSI+PGc+PHJlY3QgeD0iMCIgeT0iMTYwIiB3aWR0aD0iMjgwIiBoZWlnaHQ9IjUwIiByeD0iNy41IiByeT0iNy41IiBmaWxsPSIjZGFlOGZjIiBzdHlsZT0iZmlsbDogbGlnaHQtZGFyayhyZ2IoMjE4LCAyMzIsIDI1MiksIHJnYigyOSwgNDEsIDU5KSk7IHN0cm9rZTogbGlnaHQtZGFyayhyZ2IoMTA4LCAxNDIsIDE5MSksIHJnYig5MiwgMTIxLCAxNjMpKTsiIHN0cm9rZT0iIzZjOGViZiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48Zz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTg1cHg7IG1hcmdpbi1sZWZ0OiAxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgY29sb3I6ICMwMDAwMDA7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiAmcXVvdDtIZWx2ZXRpY2EmcXVvdDs7IGNvbG9yOiBsaWdodC1kYXJrKCMwMDAwMDAsICNmZmZmZmYpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5JbnB1dEV2ZW50VHlwZV9SZWxlYXNlPGJyIC8+KFdoZW4gbGlmdGluZyB0aGUgYnV0dG9uIGZyb20gYmVpbmcgcHJlc3NlZCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PHRleHQgeD0iMTQwIiB5PSIxODkiIGZpbGw9ImxpZ2h0LWRhcmsoIzAwMDAwMCwgI2ZmZmZmZikiIGZvbnQtZmFtaWx5PSImcXVvdDtIZWx2ZXRpY2EmcXVvdDsiIGZvbnQtc2l6ZT0iMTJweCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+SW5wdXRFdmVudFR5cGVfUmVsZWFzZS4uLjwvdGV4dD48L3N3aXRjaD48L2c+PC9nPjwvZz48ZyBkYXRhLWNlbGwtaWQ9IjYiPjxnPjxwYXRoIGQ9Ik0gMTQwIDEzMCBMIDE0MCAxNTMuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3R5bGU9InN0cm9rZTogbGlnaHQtZGFyayhyZ2IoMCwgMCwgMCksIHJnYigyNTUsIDI1NSwgMjU1KSk7IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0MCAxNTguODggTCAxMzYuNSAxNTEuODggTCAxNDAgMTUzLjYzIEwgMTQzLjUgMTUxLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0eWxlPSJmaWxsOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsgc3Ryb2tlOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjwvZz48L2c+PC9nPjwvZz48c3dpdGNoPjxnIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSIvPjxhIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAsLTUpIiB4bGluazpocmVmPSJodHRwczovL3d3dy5kcmF3aW8uY29tL2RvYy9mYXEvc3ZnLWV4cG9ydC10ZXh0LXByb2JsZW1zIiB0YXJnZXQ9Il9ibGFuayI+PHRleHQgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMHB4IiB4PSI1MCUiIHk9IjEwMCUiPlRleHQgaXMgbm90IFNWRyAtIGNhbm5vdCBkaXNwbGF5PC90ZXh0PjwvYT48L3N3aXRjaD48L3N2Zz4=
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