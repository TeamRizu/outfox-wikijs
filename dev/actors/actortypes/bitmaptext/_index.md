---
title: BitmapText
description: 
published: true
date: 2023-05-19T23:07:50.343Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:34.817Z
---

The BitmapText actor allows you to insert text into the theme, with any font that has been created and located on the Fonts folder from either your theme or `_fallback`.

```lua
Def.BitmapText{
	Font = "Common Normal", -- Alias of the default font
	Text = "Hello!"
}
```

## Table of Contents

- [Ensuring string compatibility](/en/dev/actors/actortypes/bitmaptext/Bitmap-EnsuringStringComp)
- [Inline-Text manipulation](/en/dev/actors/actortypes/bitmaptext/Bitmap-InlineColoring)
- [Segments of a BitmapText](/en/dev/actors/actortypes/bitmaptext/Bitmap-Segments)

## Attributes

| Name | Type | Action |
| :--- | :--- | :----- |
Font | string | The font to be utilized for this BitmapText. If it's not available, `Common Normal` will be utilized instead.
File | string | Alternative alias to `Font`.
Text | string | The text to show to the BitmapText.
AltText | string | An alternative version of `Text` that will be used if there's a missing glyph (or a glyph that the game doesn't recognize or can't render) in `Text`. For more information, see [Ensuring string compatibility](/en/dev/actors/actortypes/bitmaptext/Bitmap-EnsuringStringComp).