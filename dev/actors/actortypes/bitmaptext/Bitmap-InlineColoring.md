---
title: Inline-Text manipulation
description: 
published: true
date: 2023-05-19T23:17:25.007Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:14:27.288Z
---

Starting from SM5 Preview 1, [BitmapText](/en/dev/actors/actortypes/bitmaptext/_index) actors can include special instructions to manipulate separate glyphs with things like color. Operations from this use the `AddAttribute` function to insert these instructions.

```lua
-- This adds an attribute to the BitmapText. These are stacked.
self:AddAttribute( [starting point], {[attribute to add]} )

-- This removes all attributes applied on the BitmapText.
self:ClearAttributes()
```

> Any time the [BitmapText](/en/dev/actors/actortypes/bitmaptext/_index) calls `settext` or its own text changes, all attributes assigned to it will be cleared and will need to be reapplied.
{.is-warning}

# The Attributes table
The following are the attributes available via the `AddAttribute` function.
| Name | Type | Action |
| :--- | :--- | :----- |
Diffuse | color | Color for the attribute segment. This applies for all the coloring of the glyph.
Length | int | How long is the attribute going to be (size is in number of glyphs)
Diffuses | table | Table version of the Diffuse attribute, iterates through them all to give different corner colors for the glyph. An example is [shown below](#utilizing-the-diffuses-attribute).
Glow | color | Color to apply as additional color for the attribute segment.

# Examples

## Squared-Bracketed string conversion
The following example converts a string that includes square brackets into red colored sections.

```Lua
local function ConvertText( child )
	local str = child:GetText()

	-- This will contain all possible changes to change the color method.
	local charindex = 0
	-- Here we'll store the  all the possible matches to color.
	local ColoringProcess = {}

	-- Let's use gmatch to get all matches where a string is enclosed on square brackets.
	-- A trick being used here are the empty parenthesis, as gmatch doesn't provide a general index value
	-- when there's a proper match found. However, if you include parenthesis before or after a successful match,
	-- you'll get the index value of the the start and the end of the match relative to the entire string, which is 
	-- useful to get the position to apply each attribute.
	for p1,m,p2 in str:gmatch("()(%[.-%])()" ) do
		ColoringProcess[#ColoringProcess+1] = {
			-- The attributes need the value to be 0-indexed, hence the -1, as Lua provides all results starting with 1.
			Start = p1-1,
			Attr = {
				Diffuse = Color.Red,
				Length = m:len()
			}
		}
	end
	
	-- We're done. Apply the resulting table's atributes to the text.
	for k,v in pairs( ColoringProcess ) do
		child:AddAttribute( v.Start, v.Attr )
	end
end

return Def.BitmapText{
	Font = "Common Normal",
	Text = "I'm [Text]",
	OnCommand = function(self)
		self:Center() -- Center the BitmapText so it's visible
		-- Call the function above.
		ConvertText(self)
	end
}
```

The result of this example, makes the `Text` segment of the BitmapText's Text attribute red.

![colorattrexample.png](/resources/actors/bitmaptext/colorattrexample.png){.align-center}

## Utilizing the Diffuses attribute

This attribute is a special case, as it requires a table to go through them all, and each will apply to the glyphs corners.
Given this, it has a limit of 4 on the table, any other diffuse in the table past that will be ignored. If there are less than 4 on the table, the rest will be filled with `#ffffff`.

```lua
OnCommand = function(self)
	local myColors = {
		Color.Red,
		Color.Blue,
		Color.Blue,
		Color.Red,
	}

	-- Apply the diffuses to all characters in the text.
	self:AddAttribute( 0, { Diffuses = myColors, Length = -1 } )
end
```

The result ends up being that each glyph has red on the top left and bottom right corner, while having blue on the top right and bottom left corners.

![colordiffusesexample.png](/resources/actors/bitmaptext/colordiffusesexample.png){.align-center}
