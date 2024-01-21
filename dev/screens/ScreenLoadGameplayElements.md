---
title: ScreenDebugOverlay
description: 
published: true
date: 2024-01-21T22:46:06.091Z
tags: 
editor: markdown
dateCreated: 2024-01-21T22:46:06.091Z
---

The debug overlay is one of the Overlay Screens run by the game. It is reponsible for access to several utilities in the case of theme debugging, logic testing, and arcade operation.

![screendebugoverlay-showcase.png](/dev/screens/screendebugoverlay/screendebugoverlay-showcase.png)

This screen does not feature any Lua commands, as it is meant for direct interaction for debugging other actors in the game.

# Customizing the debug overlay

The debug overlay is composed of 3 main objects:
- `Background`: The actual background that will be drawn behind the screen. Often semi-transparent.
- `HeaderText`: A [BitmapText](/en/dev/actors/actortypes/bitmaptext) actor that displays the "Debug Menu" text.
- `LineTexts`: A collection of Bitmap text actors that visually represent the actors. This is not an ActorScroller, but instead an ActorFrame that fixes the item positions on the screen. Controlling these is explained in: [Controlling the ines](#controlling-the-lines).
- `PageText`: The section that manages each tab of the overlay (with the Function keys) on the top of the screen.

# Controlling the lines

Both the PageText and Line texts are basic ActorFrames that are controlled via different sets of commands. Below are the metrics and actions of each.

## Tabs {.tabset}
### Line Texts

Each action line is composed of two [BitmapText](/en/dev/actors/actortypes/bitmaptext) actors:
- `ButtonText`: Displays what key is used to toggle this function.
- `FunctionText`: What the function does.

![screendebugoverlay-linebreakdown.png](/dev/screens/screendebugoverlay/screendebugoverlay-linebreakdown.png)

These are controlled via Commands.
```ini
ButtonTextOnCommand=NoStroke;zoom,0.8
ButtonTextToggledCommand=accelerate,0.025;glow,color("1,0,0,1");sleep,0.125;decelerate,0.2;glow,color("1,0,0,0");
FunctionTextOnCommand=NoStroke;zoom,0.8
```

To modify the spacing or position of all items, the following metrics are used:
```ini
LineOnColor=color("1,1,1,1")
LineOffColor=color("0.6,0.6,0.6,1")
LineStartY=SCREEN_TOP+50
LineSpacing=16
LineButtonX=SCREEN_CENTER_X-50
LineFunctionX=SCREEN_CENTER_X-30
```

### Page Text

Each tab is just a single [BitmapText](/en/dev/actors/actortypes/bitmaptext) actor that denotes the current tab.

These pages are controlled via commands called by the screen.
```ini
PageTextOnCommand=NoStroke;zoom,0.75
PageTextGainFocusCommand=diffuse,color("1,1,1,1")
PageTextLoseFocusCommand=diffuse,color("0.6,0.6,0.6,1")
```

To modify the spacing or position of the tabs, the following metrics are used:
```ini
PageStartX=SCREEN_CENTER_X-100
PageSpacingX=120
```