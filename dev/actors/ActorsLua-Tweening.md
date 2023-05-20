---
title: Tweening
description: 
published: true
date: 2023-05-20T00:40:01.065Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:13:26.901Z
---

Actors have the ability to transition from point A to point B using [Tweening](https://en.wikipedia.org/wiki/Inbetweening).

It allows for queueing up movements & transitions on position, size, color and other attributes as well as commands and messages.

## Queueing-style tweens

These help with queueing actions after a certain amount of time.

### Sleep

The actor waits for a given amount of seconds before performing the next command.

### hibernate

Like sleep, but the actor is also hidden for the duration of the hibernate.

## Tween manipulation

These functions manipulate the flow of the tweening

### stoptweening

### finishtweening

### hurrytweening

## SM3.95-era tweens

These tweens are what most people would be familiar to those who work with ITG and SM3.95

<!-- We should probably create images for each variant... -->

### linear

The actor transitions at a constant rate.

![linear.png](/resources/actors/tweens/linear.png){.align-center}

### accelerate

![accelerate.png](/resources/actors/tweens/accelerate.png){.align-center}

### decelerate

![decelerate.png](/resources/actors/tweens/decelerate.png){.align-center}

### bouncebegin

It's done in Lua in SM5 for some reason.

![bouncebegin.png](/resources/actors/tweens/bouncebegin.png){.align-center}

### bounceend

It's done in Lua in SM5 for some reason.

![bounceend.png](/resources/actors/tweens/bounceend.png){.align-center}

### spring

![spring.png](/resources/actors/tweens/spring.png){.align-center}

### tween (NotITG only)

Takes a string that references a global function

## SM5-era tweens

These tween functions were added in SM5.

<!-- We should probably create images for each variant... -->

### "ease"

### smooth

![smooth.png](/resources/actors/tweens/smooth.png){.align-center}

### drop

![drop.png](/resources/actors/tweens/drop.png){.align-center}

### bezier

A 2D or 3D bezier curve can be passed into the function to allow for extra tweening options.

## OutFox-era tweens

OutFox added all of the standard easing functions. All of these are prefixed with `ease` and `in`/`out`/`inout`

![of-tweens.png](/resources/actors/tweens/of-tweens.png){.align-center}

<!-- We should probably create images for each variant... -->

### sine

in: easeinsine, out: easeoutsine, inOut: easeinoutsine

### quad

in: easeinquad, out: easeoutquad, inOut: easeinoutquad

### cubic

in: easeincubic, out: easeoutcubic, inOut: easeinoutcubic

### quart

in: easeinquart, out: easeoutquart, inOut: easeinoutquart

### quint

in: easeinquint, out: easeoutquint, inOut: easeinoutquint

### expo

in: easeinexpo, out: easeoutexpo, inOut: easeinoutexpo

### back

in: easeinback, out: easeoutback, inOut: easeinoutback

### circle

in: easeincircle, out: easeoutcircle, inOut: easeinoutcircle

### elastic

in: easeinelastic, out: easeoutelastic, inOut: easeinoutelastic

### bounce

in: easeinbounce, out: easeoutbounce, inOut: easeinoutbounce
