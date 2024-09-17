---
title: Defining Timing Data
description: 
published: true
date: 2023-11-04T05:05:26.351Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:16:43.233Z
---

when playing a song, several aspects of the chart will be used for timing information. These are essential to have
a nicely timed chart that people can enjoy.

### Beat 0 offset
This determines the starting point of the audio file to begin counting beats. This should be on the very start of any indication of audio
in the song. It is important that you consider changing this value if you notice your chart is off-sync, chances are the beat 0 offset is off.

### BPM
Beats per Minute, or BPM are the measurement for how many beats will amount on 60 seconds. This is used to calculate the speed of the chart
at a given point in time. A chart can contain many BPM segments, that can vary the speed.

### Stops
Stops will pause the chart for the given amount of time. Scrolling resumes once the time assigned has passed.

### Delays (SSC)
Delays will also pause the chart for the given amount of time. Scrolling resumes once the time has passed.

### Difference between Stops and Delays
Given the previous descriptions of Stops and Delays, they do seem to behave the exact same, and they do; the difference is how notes
interact on their start and end segments.
Stops let you hit notes at the very start of the segment, while Delays let you hit notes at the very end of the segment.
This is important to note in case you'd want to create segments that stop the chart for a given amount of time, to then
make the player hit a note to the timing of the song picking back up to then resume scrolling.

### Time Signatures
Currently only a visual aspect in the game for the editor, 

### Label
Labels can be used to mark segments of notes with notes, that will be shown on the editor on the right side of the notefield

<!--
Hold Checkpoints
Combo Checkpoints
Warps
Speed (Percentage)
	Speed (Length)
	Speed (Mode)
Scroll Factor
Fake segment

-->