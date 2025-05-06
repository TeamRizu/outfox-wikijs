---
title: The Structure of folders
description: 
published: true
date: 2025-05-06T02:16:45.782Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:18:46.002Z
---

A theme can consist of the following folders. All of them are optional, but needed to perform certain operations on how to load / fetch files.

It is important to understand that themes in newer versions of StepMania/OutFox rely on `_fallback`, a special theme folder located on `Appearance/Themes/` which contains all of the information neccessary to run any kind of theme. Earlier in the day, since there was no such thing, every theme distributed had to contain the same information in order to run, which in term would lead to a lot of repeated code for something that was never used.

You can create more/less folders than this and call them in your theme by fetching the location of your theme's folder
and then accessing the data that you need, but for the purposes of this guide, we'll stick to these folders.

<div style="display: flex;">
  <div style="display: flex; justify-content: space-around; flex-direction: row; flex-wrap: wrap;">
    <div style="display: flex; flex-direction: column; margin: 10px; max-width: 512px;">
      <h1>BGAnimations</h1>
      <p>Contains the lua scripts that control the visual elements of screens.</p>
    </div>
    <div style="display: flex; flex-direction: column; margin: 10px; width: 45%;">
      <h1>Fonts</h1>
      <p>Text and images containing individual glyphs, or graphical representations of each character on a font.</p>
    </div>
    <div style="display: flex; flex-direction: column; margin: 10px; width: 45%;">
      <h1>Graphics</h1>
      <p>Contains images of gameplay objects.</p>
    </div>
    <div style="display: flex; flex-direction: column; margin: 10px; width: 45%;">
      <h1>Language</h1>
      <p>Contains INI files that with the transliterated strings. For more information, visit <a href="/en/dev/translation">the Translation guide</a></p>
    </div>
    <div style="display: flex; flex-direction: column; margin: 10px; width: 45%;">
      <h1><a href="/en/dev/theming/Theming-Modules">Modules</a></h1>
      <p>An optional folder that contains Lua files with simple functions or tables that can be called on demand, rather than
storing the file on memory all the time.</p>
    </div>
    <div style="display: flex; flex-direction: column; margin: 10px; width: 45%;">
      <h1>Other</h1>
      <p>An optional folder that contains special files, but also can contain other kinds of files that don't have a particular folder to reside in.</p>
    </div>
    <div style="display: flex; flex-direction: column; margin: 10px; width: 45%;">
      <h1><a href="/en/dev/theming/Theming-Scripts">Scripts</a></h1>
      <p>Lua files that will be loaded into memory, that can be accessed at any time.</p>
    </div>
  </div>
</div>

Once you created these folders (mind you, all are optional, and the guide will tell you when each one is going to be created), let's discuss about screens.

- [Next: What are screens? *A brief overview of what screens are.*](/en/dev/theming/myfirstbga)
{.links-list}