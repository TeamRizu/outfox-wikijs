---
title: ScreenHowToPlay
description: A screen meant to showcase players how to play the game.
published: true
date: 2026-01-13T22:49:09.075Z
tags: screen, howtoplay
editor: markdown
dateCreated: 2026-01-13T22:49:09.075Z
---

The HowToPlay screen is a screen meant to showcase players how to play the game. This is presented with a [NoteField]() with a hand-made chart that contains just the necessary notes to teach each type.

> This is different from some themes where they use `ScreenDemonstration2`, a custom user-made screen where it reuses the normal ScreenDemonstration to teach the basic ropes.
{.is-info}

## Available Metrics
| Name | Default Value | Description |
| --- | --- | --- |
NumW2 | 4 | How many Excelents (W2) should be made during the tutorial?
NumMisses | 6 | How many misses should be made during the tutorial?
UseCharacter | true | Adds a 3D character into the tutorial.
UsePad | true | Adds a 3D dance pad into the tutorial.
UsePlayer | true | Adds a [Player]() instance, which includes a lifebar, notefield and judgment calculation.
CharacterName | "" | Specify if a specific character should be used in the tutorial, instead of a random character.

## Judgment calculation

ScreenHowToPlay uses the judgment metrics (`NumW2`, `NumMisses`) to count how much it needs to actually press buttons before ignoring every note afterwards.

## 3D Models in the screen

This screen supports using any [Characters]() installed in your game, and a DancePad model that must be provided and installed in the same folder as the [Characters](). The filename for the pad has to be named `DancePad.txt` and `DancePads.txt` for doubles.

> The game calls for `DancePads.txt` to be loaded, but it isn't used on this screen.
{.is-info}

The animations used for the [Characters]() in this screen are the following:

- BeginnerHelper_step-up.bones.txt
- BeginnerHelper_step-down.bones.txt
- BeginnerHelper_step-left.bones.txt
- BeginnerHelper_step-right.bones.txt
- BeginnerHelper_step-jumplr.bones.txt
- The "rest" animation set for your character.
