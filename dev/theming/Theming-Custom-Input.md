---
title: Custom Input
description: 
published: true
date: 2025-05-07T06:10:26.749Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:19:01.100Z
---

OutFox allows custom input to be managed by the theme itself. This allows you full sandboxed control of the game for the purposes of the theme.

---

# Implementing Input

There are a few ways to implement input, but the general action is to call `Screen:AddInputCallback( input function )` to the [ActorFrame](/en/dev/actors/actortypes/actorframe) responsible for the input. This can be either a function or a module that will deal with listening and sending instructions back to the engine, that actors can then pick up to provide feedback.

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
PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHN0eWxlPSJiYWNrZ3JvdW5kOiB0cmFuc3BhcmVudDsgYmFja2dyb3VuZC1jb2xvcjogdHJhbnNwYXJlbnQ7IGNvbG9yLXNjaGVtZTogbGlnaHQgZGFyazsiIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIyODFweCIgaGVpZ2h0PSIyMTFweCIgdmlld0JveD0iLTAuNSAtMC41IDI4MSAyMTEiIGNvbnRlbnQ9IiZsdDtteGZpbGUgaG9zdD0mcXVvdDtlbWJlZC5kaWFncmFtcy5uZXQmcXVvdDsgYWdlbnQ9JnF1b3Q7TW96aWxsYS81LjAgKE1hY2ludG9zaDsgSW50ZWwgTWFjIE9TIFggMTAuMTU7IHJ2OjEzOC4wKSBHZWNrby8yMDEwMDEwMSBGaXJlZm94LzEzOC4wJnF1b3Q7IHZlcnNpb249JnF1b3Q7MjYuMi4xNCZxdW90OyZndDsmbHQ7ZGlhZ3JhbSBpZD0mcXVvdDtTN2RiaS1zZHdqZXJoRDE5UmtPbCZxdW90OyBuYW1lPSZxdW90O1DDoWdpbmEtMSZxdW90OyZndDszVmJkYjlNd0VQOXJJckVYMURacDE5ZlJkb01IcElraGpUMGhONzRrRm80ZE9VNlQ4dGR6cnUxOHRqQUJtbUI5cUh5Lys3THZkM2RLRUc3eTVrNlJJdnNvS2ZCZ01hTk5FRzZEQmY0aS9EZkEwUUx6NjlBQ3FXTFVRUjN3d0w2REEyY09yUmlGY21Db3BlU2FGVU13bGtKQXJBY1lVVXJXUTdORThtSFdncVF3QVI1aXdxZm9JNk02cytoNk9ldnc5OERTekdlZXo1d21KOTdZQVdWR3FLeDdVTGdMd28yU1V0dFQzbXlBbTlyNXVsaS8yd3ZhOW1JS2hINk93OEk2SEFpdjNOdUN4WXFqNnp2S0RuaE16ZkdES0NxOU8yREl6OGNDdnQ0eVZlcDdCV1hwYlRGK3oveE1oRGVQR1Foek1lUEZSR29JeXdELzk1WFdVcHc0VUMyWW1BUkdZamxjK1doN05ZNC96bnFxcHo1NmtwU3NCQVh6emptcTY0eHBlQ2hJYkxRMWRpVmltYzY1VXllTTg0M2tlQW5qRzFJQzZ5Ukd2TlJLZm9PZVpoV3ZZWiswK2ZxVmRzVS9nTkxROUNCWCtUdVFPV2gxUkJNL0I3NHQzQmlFWHE2N3BscXNIWmIxR3NvM0duRjluTGFoTzZyeDROZyt6M3g0aHZsUkJVSFFHek10S01XY0lISHhzR2hkaFdjb1FjUDBGM04rdTNUU2s3TXo1MjNUTTlzZXZTRHcxajBuSXo3MWRaM2JTZkorQ1pmMWpXQTRUZ3k3eDJhNVNFZ3BLeFhEb044MVVTazRLN2VMZ0E1bWZrcGFqNVRsVHpoUndQRldoK0dtT0VlVXkzQXZtZEJkVDBUam5oaHpiVi9qdlBxVFBRb1VSc05BYldBZnlOWmdFdWpVTisyem45VkswYVNWUmh2akV4UkE5SFNTL1ZySWNBRlB0OExWYXhqcDlRdU85UExYUEhBZ0pWd21nck5FbjEvUFN1WkdCcXM5N1hHZ3I0R2hhUFdDREszKzU2WGJmcXY4MFFhT3BodDQrVTl0NEhiaitoRysvdDBOUEFvVXpmL1dCa2F4KzBTMDV0MTNkcmo3QVE9PSZsdDsvZGlhZ3JhbSZndDsmbHQ7L214ZmlsZSZndDsiPjxkZWZzPjxzdHlsZT5Aa2V5ZnJhbWVzIGdlLWZsb3ctYW5pbWF0aW9uLWtDZnExbk5RNVY5MWZRQ1QwRWhFIHsmI3hhOyAgdG8geyYjeGE7ICAgIHN0cm9rZS1kYXNob2Zmc2V0OiAwOyYjeGE7ICB9JiN4YTt9PC9zdHlsZT48L2RlZnM+PGc+PGcgZGF0YS1jZWxsLWlkPSIwIj48ZyBkYXRhLWNlbGwtaWQ9IjEiPjxnIGRhdGEtY2VsbC1pZD0iMiI+PGc+PHJlY3QgeD0iMCIgeT0iMCIgd2lkdGg9IjI4MCIgaGVpZ2h0PSI1MCIgcng9IjcuNSIgcnk9IjcuNSIgZmlsbD0iI2RhZThmYyIgc3R5bGU9ImZpbGw6IGxpZ2h0LWRhcmsocmdiKDIxOCwgMjMyLCAyNTIpLCByZ2IoMjksIDQxLCA1OSkpOyBzdHJva2U6IGxpZ2h0LWRhcmsocmdiKDEwOCwgMTQyLCAxOTEpLCByZ2IoOTIsIDEyMSwgMTYzKSk7IiBzdHJva2U9IiM2YzhlYmYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PGc+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI1cHg7IG1hcmdpbi1sZWZ0OiAxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgY29sb3I6ICMwMDAwMDA7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiAmcXVvdDtIZWx2ZXRpY2EmcXVvdDs7IGNvbG9yOiBsaWdodC1kYXJrKCMwMDAwMDAsICNmZmZmZmYpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PklucHV0RXZlbnRUeXBlX0ZpcnN0UHJlc3M8L2Rpdj48ZGl2PihXaGVuIHByZXNzaW5nIHRoZSBidXR0b24gZm9yIHRoZSBmaXJzdCB0aW1lKTxiciAvPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48dGV4dCB4PSIxNDAiIHk9IjI5IiBmaWxsPSJsaWdodC1kYXJrKCMwMDAwMDAsICNmZmZmZmYpIiBmb250LWZhbWlseT0iJnF1b3Q7SGVsdmV0aWNhJnF1b3Q7IiBmb250LXNpemU9IjEycHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPklucHV0RXZlbnRUeXBlX0ZpcnN0UHJlc3MuLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjwvZz48L2c+PGcgZGF0YS1jZWxsLWlkPSIzIj48Zz48cGF0aCBkPSJNIDE0MCA1MCBMIDE0MCA3My42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHlsZT0ic3Ryb2tlOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsgYW5pbWF0aW9uOiA1MDBtcyBsaW5lYXIgaW5maW5pdGUgZ2UtZmxvdy1hbmltYXRpb24ta0NmcTFuTlE1VjkxZlFDVDBFaEU7IHN0cm9rZS1kYXNob2Zmc2V0OiAxNnB4OyIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIiBzdHJva2UtZGFzaGFycmF5PSI4Ii8+PHBhdGggZD0iTSAxNDAgNzguODggTCAxMzYuNSA3MS44OCBMIDE0MCA3My42MyBMIDE0My41IDcxLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0eWxlPSJmaWxsOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsgc3Ryb2tlOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjwvZz48ZyBkYXRhLWNlbGwtaWQ9IjQiPjxnPjxyZWN0IHg9IjAiIHk9IjgwIiB3aWR0aD0iMjgwIiBoZWlnaHQ9IjUwIiByeD0iNy41IiByeT0iNy41IiBmaWxsPSIjZGFlOGZjIiBzdHlsZT0iZmlsbDogbGlnaHQtZGFyayhyZ2IoMjE4LCAyMzIsIDI1MiksIHJnYigyOSwgNDEsIDU5KSk7IHN0cm9rZTogbGlnaHQtZGFyayhyZ2IoMTA4LCAxNDIsIDE5MSksIHJnYig5MiwgMTIxLCAxNjMpKTsiIHN0cm9rZT0iIzZjOGViZiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48Zz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48c3dpdGNoPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIiByZXF1aXJlZEZlYXR1cmVzPSJodHRwOi8vd3d3LnczLm9yZy9UUi9TVkcxMS9mZWF0dXJlI0V4dGVuc2liaWxpdHkiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1cHg7IG1hcmdpbi1sZWZ0OiAxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgY29sb3I6ICMwMDAwMDA7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiAmcXVvdDtIZWx2ZXRpY2EmcXVvdDs7IGNvbG9yOiBsaWdodC1kYXJrKCMwMDAwMDAsICNmZmZmZmYpOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5JbnB1dEV2ZW50VHlwZV9SZXBlYXQ8YnIgLz4oV2hlbiBob2xkaW5nIHRoZSBidXR0b24pPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE0MCIgeT0iMTA5IiBmaWxsPSJsaWdodC1kYXJrKCMwMDAwMDAsICNmZmZmZmYpIiBmb250LWZhbWlseT0iJnF1b3Q7SGVsdmV0aWNhJnF1b3Q7IiBmb250LXNpemU9IjEycHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPklucHV0RXZlbnRUeXBlX1JlcGVhdC4uLjwvdGV4dD48L3N3aXRjaD48L2c+PC9nPjwvZz48ZyBkYXRhLWNlbGwtaWQ9IjUiPjxnPjxyZWN0IHg9IjAiIHk9IjE2MCIgd2lkdGg9IjI4MCIgaGVpZ2h0PSI1MCIgcng9IjcuNSIgcnk9IjcuNSIgZmlsbD0iI2RhZThmYyIgc3R5bGU9ImZpbGw6IGxpZ2h0LWRhcmsocmdiKDIxOCwgMjMyLCAyNTIpLCByZ2IoMjksIDQxLCA1OSkpOyBzdHJva2U6IGxpZ2h0LWRhcmsocmdiKDEwOCwgMTQyLCAxOTEpLCByZ2IoOTIsIDEyMSwgMTYzKSk7IiBzdHJva2U9IiM2YzhlYmYiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PGc+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PHN3aXRjaD48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSIgcmVxdWlyZWRGZWF0dXJlcz0iaHR0cDovL3d3dy53My5vcmcvVFIvU1ZHMTEvZmVhdHVyZSNFeHRlbnNpYmlsaXR5Ij48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4NXB4OyBtYXJnaW4tbGVmdDogMXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7IGNvbG9yOiAjMDAwMDAwOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogJnF1b3Q7SGVsdmV0aWNhJnF1b3Q7OyBjb2xvcjogbGlnaHQtZGFyaygjMDAwMDAwLCAjZmZmZmZmKTsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+SW5wdXRFdmVudFR5cGVfUmVsZWFzZTxiciAvPihXaGVuIGxpZnRpbmcgdGhlIGJ1dHRvbiBmcm9tIGJlaW5nIHByZXNzZWQpPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0Pjx0ZXh0IHg9IjE0MCIgeT0iMTg5IiBmaWxsPSJsaWdodC1kYXJrKCMwMDAwMDAsICNmZmZmZmYpIiBmb250LWZhbWlseT0iJnF1b3Q7SGVsdmV0aWNhJnF1b3Q7IiBmb250LXNpemU9IjEycHgiIHRleHQtYW5jaG9yPSJtaWRkbGUiPklucHV0RXZlbnRUeXBlX1JlbGVhc2UuLi48L3RleHQ+PC9zd2l0Y2g+PC9nPjwvZz48L2c+PGcgZGF0YS1jZWxsLWlkPSI2Ij48Zz48cGF0aCBkPSJNIDE0MCAxMzAgTCAxNDAgMTUzLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0eWxlPSJzdHJva2U6IGxpZ2h0LWRhcmsocmdiKDAsIDAsIDApLCByZ2IoMjU1LCAyNTUsIDI1NSkpOyBhbmltYXRpb246IDUwMG1zIGxpbmVhciBpbmZpbml0ZSBnZS1mbG93LWFuaW1hdGlvbi1rQ2ZxMW5OUTVWOTFmUUNUMEVoRTsgc3Ryb2tlLWRhc2hvZmZzZXQ6IDE2cHg7IiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiIHN0cm9rZS1kYXNoYXJyYXk9IjgiLz48cGF0aCBkPSJNIDE0MCAxNTguODggTCAxMzYuNSAxNTEuODggTCAxNDAgMTUzLjYzIEwgMTQzLjUgMTUxLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0eWxlPSJmaWxsOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsgc3Ryb2tlOiBsaWdodC1kYXJrKHJnYigwLCAwLCAwKSwgcmdiKDI1NSwgMjU1LCAyNTUpKTsiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PC9nPjwvZz48L2c+PC9nPjwvZz48c3dpdGNoPjxnIHJlcXVpcmVkRmVhdHVyZXM9Imh0dHA6Ly93d3cudzMub3JnL1RSL1NWRzExL2ZlYXR1cmUjRXh0ZW5zaWJpbGl0eSIvPjxhIHRyYW5zZm9ybT0idHJhbnNsYXRlKDAsLTUpIiB4bGluazpocmVmPSJodHRwczovL3d3dy5kcmF3aW8uY29tL2RvYy9mYXEvc3ZnLWV4cG9ydC10ZXh0LXByb2JsZW1zIiB0YXJnZXQ9Il9ibGFuayI+PHRleHQgdGV4dC1hbmNob3I9Im1pZGRsZSIgZm9udC1zaXplPSIxMHB4IiB4PSI1MCUiIHk9IjEwMCUiPlRleHQgaXMgbm90IFNWRyAtIGNhbm5vdCBkaXNwbGF5PC90ZXh0PjwvYT48L3N3aXRjaD48L3N2Zz4=
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