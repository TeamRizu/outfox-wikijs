---
title: Rotation
description: 
published: true
date: 2023-11-04T05:06:31.882Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:18:18.678Z
---

Rotation modifiers rotate the notes on the x, y or z axis, and can also rotate the receptors in some cases.

Some noteskins may affect how the effect looks due to how rotation and zoom interact in the notefield.

OutFox and Open/NotITG act the same way, while earlier versions of SM5 may act differently.

## Dizzy
Desc: Notes spin as they reach the receptor, with more rotationz added the farther away from the receptor a note is.

Common values involve multiples of PI to make some amount of rotation happen per beat.

For example, 628% means the notes do a full rotation every beat before hitting the receptor.

Quirks: Unlike Twirl & Roll, the rotation is based on beat distance and not physical distance. Hold heads aren't affected unless DizzyHolds is used.

PlayerOptions format: Dizzy(\<magnitude\>, \<approach rate\>)

Example: `Dizzy(3.14, 2)`

Modstring format: *\<approach rate\> \<magnitude\> dizzy

Example: `*2 314% dizzy`

<video class="normal-scale-video" src="/resources/guide-to-modifiers/rotation/dizzy.webm" controls="">Dizzy video example</video>

### Available sub modifiers:
## DizzyHolds
Desc: Enables Dizzy to affect hold heads. When used in 5.1, hold heads will still turn while held.

PlayerOptions format: DizzyHolds(\<enable\>)

Modstring format: \<enable\> dizzyholds


## Twirl
Desc: Notes twirl as they reach the receptor, with more rotationy added the farther away from the receptor a note is.

Values can go from -200 to 200% and beyond.

Quirks: Also affects holds in their entirety. Single-sided noteskins may result in invisible notes sometimes (As seen in the video example).

PlayerOptions format: Twirl(\<magnitude\>, \<approach rate\>)

Example: `Twirl(2.2, 3)`

Modstring format: *\<approach rate\> \<magnitude\> twirl

Example: `*3 220% twirl`

<video class="normal-scale-video" src="/resources/guide-to-modifiers/rotation/twirl.webm" controls="">Twirl video example</video>

## Roll
Desc: Notes roll as they reach the receptor, with more rotationx added the farther away from the receptor a note is.

Values can go from -200 to 200% and beyond.

Quirks: Single-sided noteskins may result in invisible notes sometimes (As seen in the video example). Does not affect hold heads.

PlayerOptions format: Roll(\<magnitude\>, \<approach rate\>)

Example: `Roll(1.7, 3.4)`

Modstring format: *\<approach rate\> \<magnitude\> roll

Example: `*3.4 170% roll`

<video class="normal-scale-video" src="/resources/guide-to-modifiers/rotation/roll.webm" controls="">Roll video example</video>

## Confusion
Desc: The notes and receptors spin constantly. Has X, Y and Z variants available.
Not commonly used in modfiles compared to its' Offset sub-modifier.
100% usually works as a magnitude.

Quirks: The effect is beat-based, with the magnitude being a multiplier. 100% means a full rotation every ~6.28 (2*PI) beats

Available Variants: Confusion, ConfusionX, ConfusionY

Available Variants (modstring): confusion, confusionx, confusiony, confusionz (NotITG alias for confusion)

PlayerOptions format: \<Confusion variant\>(\<magnitude\>, \<approach rate\>)

Example: `Confusion(0.5, 2)`

Modstring format: *\<approach rate\> \<magnitude\> \<modstring variant\>

Example: `*2 50% confusion`

<video class="normal-scale-video" src="/resources/guide-to-modifiers/rotation/confusion.webm" controls="">Confusion video example</video>

### Available sub modifiers:
## ConfusionOffset
Desc: Allows one to rotate the notes and receptors by a static amount. Good for keeping the notes & receptors oriented properly while rotating the Player. Note that the magnitude is in radians.

628.3185% is enough for a full rotation. (Another way to put it is `PI * 200` if used in modstrings and `PI * 2` if using PlayerOptions.)

Available Variants: ConfusionOffset, ConfusionXOffset, ConfusionYOffset

Available Variants (Column-Specific): ConfusionOffsetCol, ConfusionXOffsetCol, ConfusionYOffsetCol

Available Variants (modstring): confusionoffset, confusionoffset\<column\>, confusionxoffset, confusionxoffset\<column\>, confusionyoffset, confusionyoffset\<column\>, confusionzoffset (NotITG alias for confusionoffset), confusionzoffset\<column\> (NotITG alias for confusionoffset\<column\>)

PlayerOptions format: \<ConfusionOffset variant\>(\<magnitude\>, \<approach rate\>)

Column-specific format: \<Column-specific variant\>(\<column\>, \<magnitude\>, \<approach rate\>)

Modstring format: *\<approach rate\> \<magnitude\> \<modstring variant\>


## Orient
Desc: Orient rotates the notes and receptors based on their travel direction. That means other mods, like Drunk, can influence this modifier.

Often 50% to 100% is good enough for an effect, as too much may make notes unreadable.

Quirks: When a column is Reversed, 314% ConfusionOffset may be desired for the column (or field if the whole field is reversed)

PlayerOptions format: Orient(\<magnitude\>, \<approach rate\>)

Example: `Orient(1, 0.25)`

Modstring format: *\<approach rate\> \<magnitude\> orient

Example: `*0.25 100% orient`

<video class="normal-scale-video" src="/resources/guide-to-modifiers/rotation/orient.webm" controls="">Orient video example</video>
