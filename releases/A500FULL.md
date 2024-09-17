---
title: Alpha V Play Test 000 Build Full History
description: 
published: true
date: 2024-09-17T22:47:51.288Z
tags: releases
editor: markdown
dateCreated: 2024-09-17T22:35:23.701Z
---

## Release Date: From 2022
## "Full Alpha V Changelog"

---
# Upcoming Alpha V Play Test Build pre043 - October 2024

---

## Last 'Stable' Release Date: December 25th 2023
## Alpha V Playtest Public Build pre042 

#### (Incorporates Internal Builds 0.5.0-000 to 0.5.0-041)
#### (Incorporates Internal Builds alpha5-silver A0 to A19)

These builds continue to stabilise and work on fixes we had begun to work on in 040, which was our last update. Sorry the release took over 2 months! We were working hard all that time!

Thank you for all the reports, and the playing time guys, it is really appreciated, it's allowed us to push on with newer parts of the project that would have been delayed a bit longer if we didn't have you kind folks playing this work-in-progress game.

The ChangeLog is a bit vast for this month, I hope you take a moment to sift through it, but if you have questions, either ping us in discord or leave us a message!

We have fixed the OS issues on Linux and MacOS 12.6.x and 13.x, sorry this update took a while!

We didn't want to patch up all the tiny bits on Steam so we felt it better to just get a big update done - but we won't do that again, it's a bit too hairy for us!

Thank you to all the Mac and Linux users that reported the issues for us to fix, and to you guys for continuing to support our little project, as well as the players signing up to the playtest - we will be opening this up for you all very very soon!

This change list is pretty long, as we have several mini updates in it! I hope you enjoy reading through these, do let us know if there are things we can do to improve this experience for you guys!

---
---

# OutFox 043 is in progress!

Please be patient while we work on this new build for you all!

---

---

## OutFox 0.5.0 Pre-Release Candidate 042-a38 SSE3 (Main PRETEST PlayTest Build) December 24th 2023 - FINAL 042

* ❕✅ Fixed chartlength on songs on default theme
* ❕✅ Fixed odd pause menu counting where it was counted twice instead of once
* ❕✅ Added SortOrderCourse, to add course sorting to the wheel for course modes
* ❕✅ Fixed crash on some Linux distros with our ALSA driver on 0 indexed cards
* ❕✅ Fixed crash on Linux systems with HDMI only sound outputs
* ❕✅ Fixed crash with ALSA initialisation on newer kernels
* ❕✅ Fixed crash with ALSA buffer handling on newer kernels
* ❕✅ Fixed crash with ALSA playback on newer kernels
* ❕✅ Fixed crash with ALSA HW detection on newer kernels
* ❕✅ Fixed crash with ALSA SongPosition() on newer kernels
This bugset was in here from 2003... 


---

## OutFox 0.5.0 Pre-Release Candidate 042-a37 SSE3 (Main PRETEST PlayTest Build) December 23rd 2023

* ❕✅ Fixed crash with noteskins on 32bit/ARM systems due to old fashioned Enum cast
* ❕✅ Fixed crash when generating courses
* ❕✅ Fixed compile warnings and optimised build on windows 32/64bit
* ❕✅ Fixed 2005 bug crash with courses for non-dance modes being generated on music wheel
* ❕✅ Fixed 2004 bug causing crash when beginning screen gameplay on endless
* ❕✅ Fixed 2005 bug causing crash when moving through courses on music wheel on endless
* ❕✅ Fixed 2007 bug with Endless timer freezing after the first song
* ❕✅ Fixed 2005 bug with sorting on endless mode
* ❕✅ New splash for 042... This should be the last build!
* ❕✅ Fixed crash with opening bad/missing ALSA card indexes

---

## OutFox 0.5.0 Pre-Release Candidate 042-a36 SSE3 (Main PRETEST PlayTest Build) December 19th 2023

The OpenGL renderer is now considered deprecated as of this pre-alpha, and OutFox will try to use GLAD first. If that fails, it will fall back to the legacy renderer. This is due to performance and modernisation code we've added the last 2 builds, which gives the game a better usage and speed on systems. You need a GPU from newer than 2005 to support GLAD, or RPi 2+

* ❕✅ Fixed imagecache predefined settings at start
* ❕✅ Set imagecache to resize above 512px by default
* ❕✅ ensure we cache jackets, banners and backgrounds by default
* ❕✅ Fixed invalid bones in characters
* ❕✅ Fixed DancingCharacter loading
* ❕✅ Fixed character bone loading
* ❕✅ Reverted StepsType Change to give notice of the upcoming changes. This will now happen in 044
* ❕✅ Fixed legacy drivers for now on sound
* ❕✅ Fixed sound latency on RPi and SteamDeck/ROG Ally
* ❕✅ Fixed crash with missing stepstypes


Theme Updates:

- Fixed null or 0 profile fitness goals from invoking the resume screen
- Added support for SongSampleModes
(Just like in Soundwaves, you can select the mode in the Experimental settings)
- Added option to toggle Jackets from the music wheel
- Fixed last played text displaying wrong information
- Fix difficulty change not updating high score grade
- Fix style graphics being broken in Evaluation and Edit mode

---

## OutFox 0.5.0 Pre-Release Candidate 042-a35 SSE3 (Main PRETEST PlayTest Build) December 14th 2023

* ❕✅ Fixed step error on ScreenSelectMusic in legacy theme
* ❕✅ Fixed math on linestrip drawing on GLAD
* ❕✅ Fixed scaling on linestrip drawing on GLAD
* ❕✅ Fixed rtaudio buffer generation on rtAudio
* ❕✅ Fixed device selection and probing on rtAudio
* ❕✅ Fixed buffer initialisation on rtAudio
* ❕✅ Fixed sanity checking on ImageCache
* ❕✅ Added newer board support to InputHandler_LXIO
* ❕✅ Fixed debug build missing types
* ❕✅ Fixed missing legacy openGL pipe calls that we added to GLAD
* ❕✅ Fixed calculation of fake lift notes in player
* ❕✅ Fixed crash on recursive folders greater than 4
* ❕✅ Added new recursive search/song folder support! This allows for ese/tjadb packs, osu packs, other mode folder support. There is no grouping yet, this will be coming. The folder the chart/map is in will be the group that shows in the wheel, so bear in mind.
* ❕✅ Fixed courses not showing up on SelectCourse
* ❕✅ Fixed extension checking on new recursive
* ❕✅ Added new driver system for MacOS and Linux that adds stability to device detection, if you do not see SDL2 if stats are showing, delete whatever InputDrivers= has in it in your prefs
* ❕✅ Fixed linux detection on Fedora 33+
* ❕✅ Fixed missing information when using /event on screen stats
* ❕✅ Added LYRICS stub for tja, which will be done shortly
* ❕✅ Fixed unnecessary copy in music play
* ❕✅ Fixed arm compiler warnings for armv8
* ❕✅ Fixed LXIO class variable being shadowed
* ❕✅ Synched alpha v dance theme to 1187
* ❕✅ Fixed sound crunchy buffer sizes for linux and MacOS
* ❕✅ Fixed missing length and tap notes from not being parsed in curly brackets
* ❕✅ Fixed taiko balloons needing the head to be hit first
* ❕✅ Fixed taiko drum rolls needing the head to be hit first
* ❕✅ Fixed smx holdcounts needing the head to be hit first
* ❕✅ Fixed GLAD crash on 14.04
* ❕✅ Deprecated OpenGL renderer as GLAD is out of beta and stable

---

## OutFox 0.5.0 Pre-Release Candidate 042-a34 SSE3 (Main PRETEST PlayTest Build) December 10th 2023

* ❕✅ Fixed ARM/RPi build and compile
* ❕✅ Fixed BGA skewing/corruption on videos
* ❕✅ Fixed lag with textures for now on GLAD
* ❕✅ Fixed bad audio on MacOS 14 Sonoma when using the RTAudio driver
* ❕✅ Fixed lua hook issues with MacOS 14 and newer GCC (11+) builds
* ❕✅ Added new PandaEnum system to simplify old enumeration system used in SM5
* ❕✅ Fixed PandaEnum when using Localised Strings
* ❕✅ Fixed SMA file parser module compile
* ❕✅ po-mu: Fixed Extended Channel support, we are fully nanasi compliant.
* ❕✅ po-mu: Fixed missing transform channels
* ❕✅ po-mu: Fixed occasional missing POOR BGA trigger on MacOS 12+
* ❕✅ po-mu/be-mu: Added new header fixes which now show the titles and extra information on the wheel, and speed up the title generation.
* ❕✅ po-mu/be-mu: Fixed legacy SM3.9 language for the modes, as we don't need to use bm/pnm anymore on OutFox
* ❕✅ Fixed odd discrepancies in naming in our mode system
* ❕✅ Added new main/sub/title settings for multi-chart modes
* ❕✅ Fixed EnumToString to be simpler and use the new system
* ❕✅ po-mu: Fixed mode strings on graphics
* ❕✅ po-mu: Added new chart genre support
* ❕✅ po-mu/be-mu: added new log output for bad channel calls/unsupported channel calls
* ❕✅ po-mu: Fixed a few tweaks for Krazy notskin
* ❕✅ Fixed crash when loading bad fileobjects
* ❕✅ Fixed crash with sound loader on empty/bad audio files
* ❕✅ Fixed crash with unhandled bad UTF16 / BOM files
* ❕✅ Fixed crash with filedb
* ❕✅ Optimised textbanners
* ❕✅ Added new getchartartist lua command
* ❕✅ Changed cache variation to OutFox.cache to no longer clash with SM/ITGM
* ❕✅ Optimised BMSHeader, and removed its pref from the game.

### Theme Updates: 

Dance Alpha V:

- Redone the Fitness menu to have a better display for one player
interaction, specifically with touch users.
- You can now select a goal to start a fitness session.
- Graphs in DetailedStats are now properly reset when in Course mode.
- Reworked FadeSlide module for more understandable implementation.
This now allows for precise application of actors and smoother motion
as it is no longer tied to tweens. This new version is stored in
Text.NewFadeSlide.lua, and the original one will be deprecated.

- Join button during attract now goes to Select Profile.
- TotalTimer now updates when changing a song.
- Added options to go to the wiki and the OutFox discord server.
- OptionList now supports URLs.
- Removed approximate difficulties from DiffSelector.
While they're neat looking to see what difficulties are ahead, I can't
deny that they can be disorienting; specially when both areas were
implemented, so I scrapped it and made the parts where you cannot
scroll more obvious.

- SongInfoBox's Title now updates like a scroller.
Given the new updated I did for FadeSlide, this now has better control
when scrolling through songs with long titles, even groups.

- Discord module now just says Attract Screen if its in demonstration.
- Discord module can now track when the player has paused the game,
and show how long have they paused the game, and reapply the remaining
time when resuming.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a33 SSE3 (Main PRETEST PlayTest Build) December 3rd 2023

* ❕✅ Fixed AFT creation on MacOS on GLAD
* ❕✅ Fixed Missing Chinese support on installer
* ❕✅ Fixed gimmick settings
* ❕✅ Added new AFT/AST clipping and depth support for GLAD
* ❕✅ Fixed Geometry draw modes in GLAD

---

## OutFox 0.5.0 Pre-Release Candidate 042-a32 SSE3 (Main PRETEST PlayTest Build) December 2nd 2023

* ❕✅ Fixed compiler guards for discord, so it doesn't crash on linux now
* ❕✅ Fixed gcc issues on newer versions
* ❕✅ Fixed NSIS languages
* ❕✅ Fixed issue with nsis
* ❕✅ Update GLAD Rendering pipe by forcing opengl 2.1, but opening it to mac and linux as well
* ❕✅ Optimise GLAD Rendering pipe functions
* ❕✅ Fix MESA 22.2.x+ support

---

## OutFox 0.5.0 Pre-Release Candidate 042-a31 SSE3 (Main PRETEST PlayTest Build) November 25th 2023

* ❕✅ Use Foxclock for Sound Position
* ❕✅ Fix a few errors in mutex locking
* ❕✅ Add new mainloop limiter
* ❕✅ Fix single argument tweens in pandatemplate
* ❕✅ Fix linking issue in GCC
* ❕✅ Added new Populate Message function for actors
* ❕✅ Added new Actor:AddMessage()
* ❕✅ Fix optimised math no longer being optimised on CLang/MSVC
* ❕✅ Added new Version of the pandaTemplate for gimmicks (V1.2)

---

## OutFox 0.5.0 Pre-Release Candidate 042-a30 SSE3 (Main PRETEST PlayTest Build) November 17th 2023

* ❕✅ Use a better buffer setup for rtAudio on Linux and Mac
* ❕✅ Fix 2007 era Memory heap corruption
* ❕✅ Fix gcc slowdowns
* ❕✅ Fixed rtAudio device creation, stops RPi crashes
* ❕✅ Removed workaround for sound drivers
* ❕✅ Updated docker with new cmake rules
* ❕✅ Added new channel types for BMS
* ❕✅ Added new Modern Mode (22.04+ build for linux)
* ❕✅ Lets not set non-interleaved on audio just yet... fixes garbage audio noise on Linux and Mac
* ❕✅ Break StdString.h and RageUtil circular dependencies
* ❕✅ New namespaces for RageUtil/RageMath
* ❕✅ Fix dead code in PosMap
* ❕✅ Remove inputloop to be redone in individual handlers
* ❕✅ New NoteSkin mod fixes and changes

---

## OutFox 0.5.0 Pre-Release Candidate 042-a29HF SSE3 (Main PRETEST PlayTest Build) November 13th 2023

* ❕✅ Fixed Device initialisation for rtAudio for Mac/Linux
* ❕✅ Fixed buffer sizes on Mac so no more crackles
* ❕✅ Fixed underflow on some older legacy audio systems
* ❕✅ Fixed Handle generation for rtAudio
* ❕✅ Added new by DeviceID for rtAudio
* ❕✅ Fixed buffer sizes and workaround lagging pre-2014 systems
* ❕✅ Fixed docker builds for our linux and steam environments

---

## OutFox 0.5.0 Pre-Release Candidate 042-a29 SSE3 (Main PRETEST PlayTest Build) November 13th 2023

* ❕✅ NEW!! PandaTemplate Time based Gimmicks
* ❕✅ Updated FromString for PandaTemplate
* ❕✅ Sync AlphaV Dance theme to 1178 Fixes Include:
- The In-Game Profile switcher
    You can now change profiles in the middle of a session!
    Just open the options menu like usual, and head to the Switch Profiles options at the bottom
    of the list, select a profile and presto!
    Modifiers, scores and online connections are taken care of when switching.

    For themers: The switcher is very easy to implement. You just need to obtain the local profile ID
    you want to switch with, and define which player it will be done on. This local ID can be obtained
    using the PROFILEMAN:GetLocalProfileIDFromIndex() function.
    GAMESTATE:ChangeProfileForPlayer(player, asssignedID)

    For more information, please check the LuaDocs.

- Add cursor position reset upon selecting a profile on the in-game profile switcher
- Started adding more options on SystemOptions
    The theme switcher now works again, just select a theme and press enter to confirm.
    All sound effect volume options are now present
    Connectivity toggles for OutFox Online and Discord are present

- Add support for descriptions
    If an option has a description, it will be shown.

- Fix title screen buttons sending people to the exit button
- Fix search through the prompt screen.
    Thanks to Moneko for pointing out this search methodology.
- More announcer support
* ❕✅ NEW!! Added LoopModsAllPoptions()
* ❕✅ Fixed issue with reference in sound chain
* ❕✅ Updated rtMIDI to version 6.0.0 in preparation for new updated input and output driver
* ❕✅ Updated rtAudio to version 6.0.1 in preparation for new audio subsystem driver
* ❕✅ Fixed compile for VS2022
* ❕✅ Fixed 2007 era memory heap corruption, better performance for low end machines!
* ❕✅ Fixed GCC/MSVC slowdowns
* ❕✅ Fixed loading times on screens

---

## OutFox 0.5.0 Pre-Release Candidate 042-a28 SSE3 (Main PRETEST PlayTest Build) November 4th 2023

* ❕✅ Fixed some arrow effects math
* ❕✅ Fixed compiler warnings on GCC/MSVC
* ❕✅ Fixed scaling issues on Mac 13+
* ❕✅ NEW!! Added new GetWinWidth() and GetWinHeight() commands for gimmick authors
* ❕✅ NEW!! Added new GetWinScale() for gimmick authors
* ❕✅ NEW!! Added new GetAspectRatio() for gimmick authors to know their environment
* ❕✅ Fixed case sensitivity with Enum functions
* ❕✅ NEW!! Adjusted and modernised enum functions within playeroptions
* ❕✅ Fixed GCC complaining about missing forward declarations
* ❕✅ Fixed mutex error in polyphasefilter
* ❕✅ Fixed columnmods and modernised practices in playeroptions
* ❕✅ Fixed missing console when ShowLogOutput=1
* ❕✅ NEW!! We gave in an enabled ONE-PLAYER gimmicks on KBX mode... sigh desu
* ❕✅ Fixed typos with shuffle
* ❕✅ NEW!! PandaTemplate LuaFunc for gimmicks
* ❕✅ NEW!! GameState::ChangeProfileForPlayer - needs theme updating though!
* ❕✅ Fixed headers in RageDisplay
* ❕✅ Fixed PandaUpdate for V1 version
* ❕✅ NEW!! PandaTemplate SetUpdateSleep() function


## OutFox 0.5.0 Pre-Release Candidate 042-a27 SSE3 (Main PRETEST PlayTest Build) - October 29th 2023

* ❕✅ Fixed gimmickmode pref for groove mode
* ❕✅ Added new secret gimmick pandatemplate testing 
* ❕✅ Improved mod/gimmick performance in pandatemplate
* ❕✅ Fixed crash on files with never-ending holds
* ❕✅ Added debug output to rtaudio
* ❕✅ Improved thread closing
* ❕✅ Fixed infinite overflow in boomerang
* ❕✅ Added the defines for ZeroMEM as clean or dirty for upcoming macos 15 updates
* ❕✅ Fixed some options in AudioVisualiser
* ❕✅ Added new jack-less build for the increasing number of linux distros without it
* ❕✅ Fixed force deletion in our AFT/AMV pipelines
* ❕✅ Fixed backplates from crashing
* ❕✅ Fixed portaudio from pulling in Jack Daemon when turned off
* ❕✅ Fixed crash on linux gameplay
* ❕✅ Fixed missing songs on songwheel
* ❕✅ Fixed most unparsed songs in additional folders
* ❕✅ Fixed missing BMx/PMS/DTX/TJA charts that were not parsed

### a29 HotFix -
* ❕✅ Fixed overflow in musicwheel tween, this lessens wheel stutter
* ❕✅ Fixed pointless divide in musicwheel tween, also reduces stutter on infinitessimal
* ❕✅ Fixed (some) overshooting in infinitessimals and alpha V theme wheels

---

## OutFox 0.5.0 Pre-Release Candidate 042-a26 SSE3 (Main PRETEST PlayTest Build) - October 17th 2023

* ❕✅ Fixed Crash with launching a song in KBX mode
* ❕✅ Fixed missing language strings on installer, but these need fixing
* ❕✅ Editor: Fixed PlayerOptions state resetting full preview
* ❕✅ New!! Added preference to enable or disable Gimmicks support on any mode. If you disable gimmicks, you will be put on the more optimised pathway for rendering if you play stamina or accuracy game modes. This option also lowers latency with keysounded modes, at the expense of disabling mod support.
* ❕✅ Fixed loads of stuff with theme

---

## OutFox 0.5.0 Pre-Release Candidate 042-a25 SSE3 (Main PRETEST PlayTest Build) - October 15th 2023

* ❕✅ Fixed issue where FoxClock would shadow another system clock on Windows vista/7/8.x/10 32bit
* ❕✅ Fixed crash with 2004 BMS/PMS/BML files with oddly encoded BMPs 
* ❕✅ Optimised notefield board drawing
* ❕✅ Fixed drawing in editor
* ❕✅ Fixed FFMPEG shader math so the green single frame is no more
* ❕✅ Fixed FFMPEG buffer stack
* ❕✅ Reverted Pixel pipeline adjustment as it needed more work on BMS/PMS files
* ❕✅ Fixed renderboard initial state
* ❕✅ Fixed crash in editor when attacks load on doubles
* ❕✅ Fixed screen_centre math
* ❕✅ Started to modernise our Enum system within the game
* ❕✅ Fixed missing includeplayer in network highscores
* ❕✅ Enum Modernise: FileType
* ❕✅ Enum Modernise: Animation
* ❕✅ Enum Modernise: Type
* ❕✅ Enum Modernise: BGEffect
* ❕✅ Enum Modernise: Code
* ❕✅ Enum Modernise: ControllerStateButton
* ❕✅ Enum Modernise: Songsort
* ❕✅ Enum Modernise: AnimationStates2d
* ❕✅ Enum Modernise: Month
* ❕✅ Enum Modernise: Difficulty
* ❕✅ Enum Modernise: EditMenuRow
* ❕✅ Enum Modernise: EditMenuAction
* ❕✅ Enum Modernise: SockState
* ❕✅ Enum Modernise: EzSocketsProtocol
* ❕✅ Fixed bad casts in render pipeline
* ❕✅ Fixed some issues in minimap
* ❕✅ NEW! Allowed Def.NoteField to use PlayerOptions Approach System for gimmicks
* ❕✅ Fixed compiler over optimised sorting issues on windows
* ❕✅ Fixed scroll issues with PIU charts
* ❕✅ Fixed pointer on musicwheeldata
* ❕✅ Fixed crash on invalid track numbers on old charts.

---

### OutFox 0.5.0 Pre-Release Candidate 042-a24 SSE3 (Main PRETEST PlayTest Build) - September 27th 2023

* ❕✅ Fixed one of the course generation issues
* ❕✅ Temporarily Fixed crash on RemoveAllButOneOfEachName()
* ❕✅ Fixed crash with bad DWI era .LRC files
* ❕✅ Optimise Pixel Encode/Decode (Thanks RAvenGEr)
* ❕✅ Fixed a small typo with playeroptions

---

### OutFox 0.5.0 Pre-Release Candidate 042-a23 SSE3 (Main PRETEST PlayTest Build) - September 24th 2023

* ❕✅ Fixed crash with piuio initialisation on linux
* ❕✅ Fixed freezes with some load elements
* ❕✅ Fixed and optimised some bugs in Def.Visualiser
* ❕✅ Fixed memory leaks from our framebuffers
* ❕✅ Added ScreenTextEntry:GetText() (see lua docs for more information)
* ❕✅ Added self:GetSound to editor
* ❕✅ Editor: Fixed mouse cursor selection
* ❕✅ Editor: Fixed mouse drag states
* ❕✅ Editor: Fixed misplaced input cycles
* ❕✅ Editor: Fixed mouse cycles and updates
* ❕✅ Editor: Added new Mouse X/Y functions that are correctly scaled for legacy themes/content
* ❕✅ Editor: Fixed issue with speed mods, now the system uses ArbitrarySpeedMods() on options
* ❕✅ Fixed ancient issue with automatically translated DWI songs overwriting song titles
* ❕✅ Sync up the Dance theme with our upstream
* ❕✅ Fixed logo for theme being the playtest
* ❕✅ Fixed mute actions not working after first press
* ❕✅ Fixed couples on pump layout
* ❕✅ Fixed couples on smx layout
* ❕✅ Renamed the new userspace PIUIO driver to mk6piuio

---

### OutFox 0.5.0 Pre-Release Candidate 042-a22 SSE3 (Main PRETEST PlayTest Build) - September 10th 2023

* ❕✅ Fixed bug with #LASTBEATHINT ending songs early due to StepMania 3.x editor shenanigans.
* ❕✅ Added "PacDriveLightOrdering=" preference to select lighting system wiring via PacDrive (Thanks jsirex)
* ❕✅ Added "original" legacy wiring layouts on PacDrive Linux and Windows 32/64
* ❕✅ Added "lumenar"/"openitg" layout for PacDrive Linux and Windows 32/64
* ❕✅ Added "minimaid" wiring layout for PacDrive Linux and Windows 32/64
* ❕✅ Fixed casts in DebugTimer
* ❕✅ Fixed overengineered fix in gameloop
* ❕✅ Fixed missing Halt/Slow debug functions
* ❕✅ Fixed TapNote init msvc compiler warnings
* ❕✅ Fix and optimise DebugTimer
* ❕✅ Fixed missing cast lua_num in togglesongs
* ❕✅ Fixed type method in FailCombo
* ❕✅ Fixed EffectColours map to vector
* ❕✅ Fixed compile with Win32 / Linux UserSpace MK6PIUIO driver (it needs light init fixing)
* ❕✅ Fixed legacy LibUSB calls for MK6PIUIO
* ❕✅ Added legacy SM4 DebugTimer functions and features for gimmicks and drivers
* ❕✅ Added new EffectColoursMap for effects in actor
* ❕✅ Fixed axisfix being on all the time on SDL driver
* ❕✅ Allow RandomMovie picker to get from song group
* ❕✅ Fixed missing backplates for KBX
* ❕✅ Fixed parser optimisation warning
* ❕✅ Fixed missing banners
* ❕✅ Fixed NetworkServices: Disconnect
* ❕✅ Fixed background changes
* ❕✅ Fixed docker environment builds as canonical has broken gcc
* ❕✅ Fixed intel compiler derp in zlib
* ❕✅ Added data pass to arroweffects
* ❕✅ Added HoldLetGoGrayPercent for SimpleHolds
* ❕✅ Added GetNumCoOpPlayers for pump
* ❕✅ Fixed Missing steps lookup in ScreenDemonstration/Jukebox
* ❕✅ Added allow Profile to create Song folder for customsongs
* ❕✅ Optimised ShaderMan use and calling methods
* ❕✅ Added shaders to notepath
* ❕✅ Fixed ProcessBPMs in PIU parsers
* ❕✅ Added Player.SetMineSound()
* ❕✅ Fixed edge case PIU file loading crash
* ❕✅ Editor: Fixed options menu from crashing on course exit
* ❕✅ Editor: Added option to toggle Minimap and classic info
* ❕✅ Editor: Fixed backgrounds not displaying/saving
* ❕✅ Editor: Fixed Edit Menu - Set last edited steps when entering
* ❕✅ Editor: Fixed legacy .edit chart loading
* ❕✅ Editor: Send text info during preview mode
* ❕✅ LuaConsole: Add support for paste, help text
* ❕✅ Editor: Minimap: Draw Warp Areas
* ❕✅ Editor: Minimap: Support for mouse drag
* ❕✅ Editor: Minimap: Support for reverse
* ❕✅ Editor: Minimap: Scrollable area set
* ❕✅ Editor: Minimap: Optimise draw calls
* ❕✅ Editor: Minimap: Set to own class for performance
* ❕✅ Editor: Minimap: Initialise and set up new platform
* ❕✅ Editor: Allow keysounds to play on Preview
* ❕✅ Editor: Fixed misses not being generated on play
* ❕✅ Editor: Fixed marathon charts not being loaded

### a22 HotFix:

* ❕✅ Fixed bad math with Stop calculations in piu parser
* ❕✅ Fixed bad math with bpm changes in piu parser
* ❕✅ Fixed underflow in piu parser

---

## OutFox 0.5.0 Pre-Release Candidate 042-a21 SSE3 (Main PRETEST PlayTest Build) - August 23rd 2023

* ❕✅ Fixed crash with PIU 0.81 StepF2 files
* ❕✅ Added new internal PIUIO Driver stubs to RageInputDevice
* ❕✅ Added new bitwise helpers for future PIUIO/ITGIO drivers for cabs
* ❕✅ Added new Mk5PIUIO Driver for Windows 32
* ❕✅ Fixed tapnotes for non co-op charts displaying as P4
* ❕✅ Fixed 'dumb' compiler notes for Python23IO so it doesn't mess up Linux/Mac compiling
* ❕✅ Added new Linux_PIUIO driver, Thanks D. Pohly
* ❕✅ Added new Linux SextetStream Support, Thanks Peter s. May
* ❕✅ Added Linux_TTY keyboard driver from SM4
* ❕✅ Fixed buffer underrun in SteamDeck driver on Windows
* ❕✅ Modernised BPMsAndStops() in PIU Parser
* ❕✅ Fixed MSVC compiler warnings in our parsers with a small performance boost
* ❕✅ Fixed version stub on MacOSX as we were showing 5.3 from our legacy days

---

## OutFox 0.5.0 Pre-Release Candidate 042-a20 SSE3 (Main PRETEST PlayTest Build) - August 20th 2023

(Win32 driver test build)

* ❕✅ Fixed F4 causing crashes in editor
* ❕✅ Fixed Warp Marker for SM parser
* ❕✅ Fixed Parsing iterator initialisation
* ❕✅ We had to move our minimum supported MacOS to 10.13, this was an apple thing sadly :(
* ❕✅ Fixed Python 2/3 Driver for windows 7 32bit - PLEASE TEST

---

## OutFox 0.5.0 Pre-Release Candidate 042-a19 SSE3 (Main PRETEST PlayTest Build) - August 18th 2023

* ❕✅ Fixed build env for legacy systems as we're using newer libraries
* ❕✅ Fixed dual input on def.optionslist
* ❕✅ Fixed missing playernumber on def.optionslist
* ❕✅ NEW!! Working SteamDeck standalone driver! This driver allows the game to properly work with the deck's controls, which allows for extra joystick/pads/controllers to be plugged in, without Steam overwriting the input causing some of those buttons to be lost when pressed. it requires a different driver setup.

You need to use:
InputDrivers=sdeck,SDL

or if you're using midi as well,
InputDrivers=portmidi,sdeck,SDL

or just the deck:
InputDrivers=sdeck,minisdl

This driver works on windows and linux - it's not complete, I need to disable the mouse/keyboard emulation, but once that is done, we're golden.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a18 SSE3 (Main PRETEST PlayTest Build) - August 18th 2023

Compiling sucks as half past midnight... Pump Bros...

* ❕✅ Fixed crash with people that had .mid files included in 2004-2008 dance packs from ziv...
* ❕✅ Fixed cringe rounding error in screen width math
* ❕✅ Fixed method in how CopyTexture works in returning references
* ❕✅ Fixed ASTs to work with the new system
* ❕✅ Fixed placement of test input screen so it shows more button
* ❕✅ Fixed Def.OptionsList bugs preventing it working properly

Editor Fixes
* ❕✅ Added Save and load last edited song. (Needs tweaks to get the steps as well, already saving the diff and
style for this!)
* ❕✅ Rewrote XMod/CMod scrolling for editor preview.
* ❕✅ Fixed render distance to not be ridiculous.
* ❕✅ Allow notefield to hit notes in-between warp areas.
* ❕✅ Made transition from XMod to CMod instant.
* ❕✅ Fixed render distance for Stop block areas, as they kept drawing outside of the intended area.
* ❕✅ Fixed CMod editor scrolling being offset by the global offset from the player.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a17b SSE3 (Main PRETEST PlayTest Build) - August 15th 2023

Windows Addenda - 

* ❕✅ Fixed Judgement folder being wiped on uninstall, so custom judgements will not be wiped anymore.
* ❕✅ New Build process. Those of you on Windows, if you have time, please try between Option A and Option B for performance/feel so we can choose a suitable development path for the future.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a17 SSE3 (Main PRETEST PlayTest Build) - August 13th 2023

* ❕✅ Fixed frame limiter system - if you have an unstable vsync, you can now force a frame rate using the UpdateDrawLoopSeconds pref, which will give you a set FPS update! 

NOTE: If you have an ASUS/Alienware/ACER Gaming/DELL Gaming/MSI Gaming/Medion Gaming/Sapphire Gaming/Sammsung Gaming/HP Gaming system and are running Windows 11 - it will try to throttle your machine to reduce your 'carbon footprint' check your control centre, and your GPU/Controlpanel settings. My own Laptop was throttled to 30FPS on 'office mode' but when switched to gaming mode, this was unlimited FPS! This update has been pushed out over the past 6 weeks, but it is affecting Outfox and many other games as well.

* ❕✅ Fixed DIV0 exploits in the loop
* ❕✅ Added new Reset() command to Timer
* ❕✅ Fixed stuck keys on MacOS
* ❕✅ Fixed stuck key repeat on input
* ❕✅ Fixed Tab not speeding up the game on some systems
* ❕✅ "Fixed" Lyric display for faster and slower rates, it's a workaround, not a permanent fix, we plan to rewrite the whole system in time.
* ❕✅ Fixed lyrics not showing when the rate was below 0.5 on pi and linux systems

---

## OutFox 0.5.0 Pre-Release Candidate 042-a16 SSE3 (Main PRETEST PlayTest Build) - August 12th 2023

* ❕✅ Fixed SetActiveFrame() animation
* ❕✅ Fixed missing arch specifc MacOS cmake options
* ❕✅ Fixed missing templating for SetActiveFrame()
* ❕✅ Removed JACK support on MacOS as Apple have removed it from the OS
* ❕✅ Fixed SelectGameMode not allowing selection on MacOS
* ❕✅ Fixed GameMan Crash on MacOS
* ❕✅ Introducing MacOS 14 Sonoma Support!
* ❕✅ Fixed GAMEMAN init order
* ❕✅ Fixed Memory overflow in gameloop
* ❕✅ Fixed Small optimisation in gameloop
* ❕✅ Fixed crash on GH/RB parsing
* ❕✅ Fixed crash on TJA parsing
* ❕✅ Fixed crash on DTX parsing

---

## OutFox 0.5.0 Pre-Release Candidate 042-a15 SSE3 (Main PRETEST PlayTest Build) - August 11th 2023

* ❕✅ Updated gddm icon
* ❕✅ Fixed GetDuration on midi parser
* ❕✅ Added gh drum support in midi parser
* ❕✅ Added gh drum (normal5) style to playable options in rb
* ❕✅ Added new normal5 icon
* ❕✅ Fixed strum stutter on windows (please test)
* ❕✅ Fixed white dot in rb noteskin
* ❕✅ Optmised gh notedata, and set things to instrument
* ❕✅ Fixed crash on empty charts in midi parser
* ❕✅ Added TNS_W4 to pump miss for correct combo checking
* ❕✅ Added new cross code for gh to rb drum support in parser
* ❕✅ Added new combo support for pump: bad now breaks miss combo, good no longer increments combo, bad zeros hit combo - thanks to andrey for bitching at us to fix it
* ❕✅ Fixed errors in gameplay.lua to ensure the combocontinue and combomaintain function correctly in pump

---

## OutFox 0.5.0 Pre-Release Candidate 042-a14 SSE3 (Main PRETEST PlayTest Build) - August 8th 2023

* ❕✅ NEW!! Introducing support for OutFox's 19th Game Mode - Boxing! This mode is designed to be set up at a gym and played with joy-cons or a similar setup. It's great fun and has a variety of punch styles. We are working on gyro/VRK support so you can play this with those controllers.

* ❕✅ NEW!! Introducing support for OutFox's 20th Game Mode - rb! This mode compliments our gh mode and is based on the familiar chart format .mid The game supports. the mode is made up of rb-easy, which is the normal 4 drum lane without the kick, rb-normal, which is the usual 4 drum lane and supporting the kick, and rb-pro, which is 4 drums, 1 kick and 3 cymbals. You can utilise songs from gh which contain drum charts easily enough! 

.chart is going to be worked on later on, this is just the skeleton remember, so a theme and mode specification and changes will happen to improve the game module, as is done with all our supported games.

This mode also makes OutFox the only sim in the world to support 4 Different game drum modules: gddm, taiko, bongo, rb. We hope you'll be as hype as us for this milestone, and to continue improving our coverage and accuracy in the modules that we support.

rb supports PRO DRUMS out of the box, again the theme is lacking as we need to stop developing crap and focus on it in Q3/4 of this year. This mode also supports our MIDI drivers for eDrum kits! you can now use your eDrums on more than one drum mode!

* ❕✅ NEW!! drum, pro-drum lane support for the mid parser! This required a major rewrite of the parsing system to match one similar to gddm/gdgf so the game knew which part of the chart was drum and such. Please test and let us know if there are any MIDI songs that have issues. Remember .chart hasn't been adjusted yet!

* ❕✅ Fixed quirk with LXIO hanging on Windows 11
* ❕✅ Fixed some prefs being broken in the default metrics.ini file
* ❕✅ Fixed incorrect fret notes in midi parser
* ❕✅ Fixed multi-track support in midi parser
* ❕✅ Fixed songs with only 1 track being used incorrectly in midi parser
* ❕✅ Fixed lane allocation within midi parser
* ❕✅ Fixed missing note types in the midi parser
* ❕✅ Fixed detection of forced notes in the midi parser
* ❕✅ Fixed detection of pro-drums in midi parser
* ❕✅ Fixed missing expansion of notes needed for drum charts
* ❕✅ Fixed difficulty detection in midi parser
* ❕✅ Fixed missing event text support in midi parser
* ❕✅ Added new enums for difficulty and chart types in midi parser
* ❕✅ Added new opus support for songs in the midi parser
* ❕✅ Fixed missing backgrounds in the midi parser
* ❕✅ Added new guitar support: pro guitar, 6 fret guitar skeletons in midi parser
* ❕✅ Added new drum support: pro drums, easy drums, normal drums in midi parser
* ❕✅ Added new keys support: pro keys and normal keys skeletons in midi parser

### a14 HotFix (09-08-2023)

* ❕✅ Fixed missing graphics on new mode
* ❕✅ Fixed quirk with bad bpm calls on midi parser
* ❕✅ Fixed quirk with time signatures on midi parser
* ❕✅ New!! Added digital control driver for SteamDeck using HIDRAW. Analogue is to be finished. Ask squirrel if you have windows on your deck on how to test, i will build linux in the mornin as i'm dead.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a13 SSE3 (Main PRETEST PlayTest Build) - August 5th 2023

* ❕✅ Forced best guess pref on Linux to fix Kernel 5.13+ issues
* ❕✅ Added new #Metadata tag to the SSC specification.
* ❕✅ Added TNS_W5 to reset combo for pump
* ❕✅ Fixed crash with non existing driver being presented
* ❕✅ Fixed quirk with game mode resetting
* ❕✅ Fixed bug in lua not being reset correctly when changing game mode
* ❕✅ Fixed crash on some systems that do not present a loading window
* ❕✅ Fixed crash on rendertargets
* ❕✅ Fixed crash on screens which do not require notedata
* ❕✅ Fixed crash with lateplayerjoin() on some modes by rewriting the function completely

---

## OutFox 0.5.0 Pre-Release Candidate 042-a12 SSE3 (Main PRETEST PlayTest Build) - July 30th 2023
Two builds in one day edition!!

* ❕✅ Added FailPlayerInstantly when FailComboAt is reached (optional for pump)
* ❕✅ Fixed missing pushback for optionslists (for pump)
* ❕✅ Fixed Missing OptionsLists Clear (for pump)
* ❕✅ Fixed bug with erasing mods lists on the new modstring system
* ❕✅ Fixed crash with ShaderManger on some Linux/Mac versions
* ❕✅ Added 'AddCheckpointToHead' for pump holds, means hold heads no longer count as tap notes.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a11 SSE3 (Main PRETEST PlayTest Build) - July 30th 2023

* ❕✅ Added a PointSize() function for Actors to compliment Points Polygon Mode
* ❕✅ Added NoteCullMode, that lets you set culling for notes
* ❕✅ Added F&B cull mode option to Actors, for 3D Models
* ❕✅ Added Note-Specific WireFrame
* ❕✅ Added Column-Specific NotePathWidth
* ❕✅ Added Note-Specific ScrollSpeedMult
* ❕✅ Added Note-Specific ExtendHolds
* ❕✅ Added Def.OptionsList, For Pump themes, and other modes [Please Test]
* ❕✅ Fixed bug with MIDI parser not loading some older CH files
* ❕✅ Added Actor Matrix Rotation commands and lua hooks
* ❕✅ Fixed bug with 2003 code in DirectX matrix math rounding... we don't use DirectX anymore
* ❕✅ Fixed bug with slow loading on legacy/SD card systems
* ❕✅ Fixed bug with Screen hanging on Linux/Mac
* ❕✅ Fixed bug with the Garbage Collector hanging theme refreshes on reboots of the game
* ❕✅ Fixed bug with CLANG compiling on Mac
* ❕✅ PUMP: Added combo effects for good and boo judges
* ❕✅ PUMP: Added new FailType_MissCombo which will fail players for 51 misses in a row.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a10 SSE3 (Main PRETEST PlayTest Build) - July 28th 2023

* ❕✅ Fixed bug with 1bit and 2 bit bmp corruption on vintage (1998-2002) BMS files
* ❕✅ Updated stb to reduce memory leaks on texture loading
* ❕✅ Fixed ManageProfiles not running OnCommand functions
* ❕✅ Added a new screen: ScreenOptionsToggleSongs to allow operators to select what songs are available from the music wheel. This menu is available in 'Operator Options' in fallback.
* ❕✅ Fixed bug with ScreenEditMenu not being alphabetical
* ❕✅ Fixed bug with FFMPEG videos not working on Intel Macs
* ❕✅ Fixed bug with 2001 resolution math breaking theme layouts from SM4_beta and < SM 5.0.7, and some content from other forks. This resolves the framebuffer bugs added in 0.5.0-r021
* ❕✅ Fixed bug with width not being a flat number
* ❕✅ Added points support to Polygon Mode
* ❕✅ Fixed Profile Editor screen from removing the current profileID when restarting
* ❕✅ Fixed Mac compile in NoteTypes
* ❕✅ Added judgeable row condition on notefield autoplay to prevent hits on warp areas
* ❕✅ Added basic obj condition when loading a .obj file in a def.model()
* ❕✅ Added NoteGroupTypes to GetNoteData() and SaveToLua(): Mentioned in TeamRizu/OutFox#666, this adds the NoteGroupType to the Lua table result that indicates the kind of group. This is necessary for the hold types as we have included MineHolds and tail-end holds.

For tails, a special rule was added to only include it on the list if said tail was part of a Lift-Hold. If not, it will be reported as a standard note in the table.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a9 SSE3 (Main PRETEST PlayTest Build) - July 8th 2023

* ❕✅ AlphaV Dance Theme: Fixed player centre alignment
* ❕✅ AlphaV Dance Theme: Fixed longsong label
* ❕✅ AlphaV Dance Theme: Fixed cancel in EditProfile
* ❕✅ AlphaV Dance Theme: Notefield fixes
* ❕✅ AlphaV Dance Theme: Fixed bug with outer filter failing on Select Music
* ❕✅ Fixed compiler warnings
* ❕✅ Fixed TextEntry not being available via lua
* ❕✅ Removed legacy calls choking the glad renderer
* ❕✅ Fixed compile on mac/linux
* ❕✅ Fixed bug with rendertarget stack corruption
* ❕✅ Added new bg shader support - this is called via compilebg and compileimmediatebg and doesn't rely on songbeat or fmusicseconds
* ❕✅ Fixed crash with texture deletion calls on linux
* ❕✅ Fixed crash with texture free calls on linux
* ❕✅ Fixed offset player math in soundwaves
* ❕✅ Updated SDL to 2.28.2
* ❕✅ Fixed onemodstring narrowed math calls
* ❕✅ Fixed shadermanager quirks and edge case crash

---

## OutFox 0.5.0 Pre-Release Candidate 042-a8 SSE 3 TEST BUILD (Main PRETEST PlayTest Build) - July 7th 2023

* ❕✅ Fixed bug with text entry sound calls crashing
* ❕✅ Fixed a few bugs with math calls
* ❕✅ Added flat map
* ❕✅ Fixed crash with imagecache
* ❕✅ Fixed crash with oob animation remaining time
* ❕✅ Fixed crash with tapnotes
* ❕✅ Fixed static cast with luna numbers
* ❕✅ Fixed song loading crashes
* ❕✅ Fixed mutex lock on song loading causing a forever hang
* ❕✅ Fixed crash on render target stack with ARM boards
* ❕✅ Fixed crash with changing screen resolution
* ❕✅ Fixed missing controllers on MacOS
* ❕✅ Fixed missing controllers on *nix and ARM
* ❕✅ Optimised the game to support SSE3 intrinsics - test this for now so we can see how it behaves

---

## OutFox 0.5.0 Pre-Release Candidate 042-a7 (Main PRETEST PlayTest Build) - July 5th 2023

* ❕✅ AlphaV Dance Theme: Fixed instance when the user has not enough profiles to fill up
the entire list in SelectProfile.
* ❕✅ AlphaV Dance Theme: Fixed instance when there are no profiles at all on SelectProfile.
* ❕✅ AlphaV Dance Theme: Fix scrolling for SelectProfile
* ❕✅ AlphaV Dance Theme: Fixed the scrolling for items on the right side.
* ❕✅ AlphaV Dance Theme: Fixed items not being selectable when connecting to OutFox Online.
* ❕✅ AlphaV Dance Theme: Moved Link Account to Profile to a proper spot.
* ❕✅ AlphaV Dance Theme: Changed font for search to be monospaced.
To preserve the "SEARCH" label, it is kept as a static bitmapText.
* ❕✅ AlphaV Dance Theme: Changed design for next/prev buttons for OptionList.
* ❕✅ AlphaV Dance Theme: Set an "Off" label for Announcer picker. Will be useful for later
entries.
* ❕✅ AlphaV Dance Theme: Made dropdown transitions and movement faster.
* ❕✅ AlphaV Dance Theme: Avoid making Game Select dropdown set the game on the current one.
* ❕✅ AlphaV Dance Theme: Changed the Game Select dropdown icons with the StyleVector ones.
* ❕✅ AlphaV Dance Theme: Fixed mouse input when selecting profile in ScreenSelectProfile.
* ❕✅ AlphaV Dance Theme: Fixed movement for supplemental input modes in InitialSetup.
* ❕✅ AlphaV Dance Theme: Added "groove" to game mode listings.
* ❕✅ AlphaV Dance Theme: GridSystem: CheckBoundry now returns the cursor for quicker lookup.
* ❕✅ Fixed bug with missing paths on linux memory cards due to new kernels
* ❕✅ Fixed bug with attacklist eating resources
* ❕✅ Fixed bug with missing attack approach rate calculations
* ❕✅ Fixed bug with selectprofile screen
* ❕✅ Fixed bug with missing fScale boolean check causing a few quirks
* ❕✅ Added new client linking skeleton (Features to come soon!)
* ❕✅ Fixed bug with ScoreSave lua hook
* ❕✅ Fixed bug with lifeweights for itg timing
* ❕✅ Fixed edge crash with game changing

KNOWN BUGS: we are working on them!

* ❌ - Changing resolution will crash the game on some systems
* ❌ - Steam Deck Input issues with LTek pads, will be fixed soon, I just need to write the new driver
* ❌ - The crashes on Windows 7 we are investigating still
* ❌ - Let us know if you have other issues so they can be fixed!

---

## Note: Mods will be called Gimmicks in Project OutFox moving forward, as we have more modes that use this term, and 'mods' are used for speed, rather than snazzy arrow/object effects. Thanks for understanding! 


To play Gimmick Charts on this build of OutFox, you need to select the GROOVE mode. We have removed the main Gimmick lists and crazy sides from the Dance Mode for performance concerns for folks that play Acc/Stamina. 

Thanks for your support as always, and we hope you like these changes, I know it's a bit mad with all the new gimmicks, but these have been requested for some time.

---

## OutFox 0.5.0 Pre-Release Candidate 042-a6 (Main PRETEST PlayTest Build) - June 28th 2023

Poptions and AllTheMods (Part 2 of 2) build. MTK's Power Level is over 9000! - Squirrel

* ❕✅ Fixed bad boolean math with fScale narrowing 'close to zero'
* ❕✅ Fixed bug with EndOfSong from failing on FailCombo
* ❕✅ AlphaV Dance Theme: Fixed init screen 
* ❕✅ AlphaV Dance Theme: Fixed wheel favourites
* ❕✅ AlphaV Dance Theme: Fixed bug with minixoffset on screengameplay
* ❕✅ AlphaV Dance Theme: Fixed color change issues
* ❕✅ AlphaV Dance Theme: Added new screen avatar fixes
* ❕✅ AlphaV Dance Theme: Added new options and profile fixes
* ❕✅ AlphaV Dance Theme: Added new initial setup screens
* ❕✅ AlphaV Dance Theme: Fixed wheel items
* ❕✅ AlphaV Dance Theme: Added new click helper areas for mouse/touch panel users
* ❕✅ New! Added metric to themes to allow chart audio to be hidden for chart specific files - Closes TeamRizu/OutFox#645
* ❕✅ Added link to original SM credits screen in fallback for folks that requested it
* ❕✅ Fixed bad logarithmic transcription in tiny, we needed base10
* ❕✅ Fixed missing none image to be-mu/po-mu backplate
* ❕✅ Fixed cached images showing on jackets instead of HD versions
* ❕✅ Added new lua hooks for favourites
* ❕✅ Added new Profile:GetLastdifficulty
* ❕✅ Fixed invalid colours in ScreenOptionsManageProfiles
* ❕✅ Added Note Specific asymptote
* ❕✅ Added Note Specific attenuateX, attenuateY, attenuateZ
* ❕✅ Added Note Specific beat, beatY, beatZ
* ❕✅ Added Note Specific blink
* ❕✅ Added Note Specific blinkred, blinkgreen, blinkblue, blinkalpha
* ❕✅ Added Note Specific boost
* ❕✅ Added Note Specific boomerang
* ❕✅ Added Note Specific bounce, bounceZ
* ❕✅ Added Note Specific brake
* ❕✅ Added Note Specific bumpy, bumpyX, bumpyY
* ❕✅ Added Note Specific centered
* ❕✅ Added Note Specific confusion
* ❕✅ Added Note Specific confusionoffset
* ❕✅ Added Note Specific confusionX
* ❕✅ Added Note Specific confusionxoffset
* ❕✅ Added Note Specific confusionY
* ❕✅ Added Note Specific confusionyoffset
* ❕✅ Added Note Specific cubicX, cubicY, cubicZ
* ❕✅ Added Note Specific digital, digitalZ
* ❕✅ Added Note Specific dizzy
* ❕✅ Added Note Specific drunk, drunkY, drunkZ
* ❕✅ Added Note Specific expand
* ❕✅ Added Note Specific flip
* ❕✅ Added Note Specific hidden
* ❕✅ Added Note Specific hiddenred, hiddengreen, hiddenblue, hiddenalpha
* ❕✅ Added Note Specific hiddenoffset
* ❕✅ Added Note Specific hiddenoffsetred, hiddenoffsetgreen, hiddenoffsetblue, hiddenoffsetalpha
* ❕✅ Added Note Specific invert
* ❕✅ Added Note Specific moveX, moveY, moveZ
* ❕✅ Added Note Specific noteskewX, noteskewY, 
* ❕✅ Added Note Specific orient, orientX, orientY
* ❕✅ Added Note Specific parabolaX, parabolaY, parabolaZ
* ❕✅ Added Note Specific pulseinner, pulseouter
* ❕✅ Added Note Specific randomspeed
* ❕✅ Added Note Specific reverse
* ❕✅ Added Note Specific roll
* ❕✅ Added Note Specific sawtooth, sawtoothZ
* ❕✅ Added Note Specific shrinkmultX
* ❕✅ Added Note Specific shrinklinearX
* ❕✅ Added Note Specific shrinkmultY
* ❕✅ Added Note Specific shrinklinearY
* ❕✅ Added Note Specific shrinkmultZ
* ❕✅ Added Note Specific shrinklinearZ
* ❕✅ Added Note Specific spiralX
* ❕✅ Added Note Specific spiralXoffset
* ❕✅ Added Note Specific spiralXperiod
* ❕✅ Added Note Specific spiralY
* ❕✅ Added Note Specific spiralYoffset
* ❕✅ Added Note Specific spiralYperiod
* ❕✅ Added Note Specific spiralZ
* ❕✅ Added Note Specific spiralZoffset
* ❕✅ Added Note Specific spiralZperiod
* ❕✅ Added Note Specific stealth
* ❕✅ Added Note Specific stealthred, stealthgreen, stealthblue, stealthalpha
* ❕✅ Added Note Specific sudden
* ❕✅ Added Note Specific suddenred, suddengreen, suddenblue, suddenalpha
* ❕✅ Added Note Specific suddenoffset
* ❕✅ Added Note Specific suddenoffsetred, suddenoffsetgreen, suddenoffsetblue,suddenoffsetalpha
* ❕✅ Added Note Specific square, squareZ
* ❕✅ Added Note Specific tanbumpy, tanbumpyX, tanbumpyY
* ❕✅ Added Note Specific tandigital, tandigitalZ
* ❕✅ Added Note Specific tandrunk, tandrunkY, tandrunkZ
* ❕✅ Added Note Specific tanexpand
* ❕✅ Added Note Specific tanpulseinner, tanpulseouter
* ❕✅ Added Note Specific tantornado, tantornadoZ
* ❕✅ Added Note Specific tornado, tornadoZ
* ❕✅ Added Note Specific tiny, tinyX, tinyY, tinyZ
* ❕✅ Added Note Specific twirl
* ❕✅ Added Note Specific vanish
* ❕✅ Added Note Specific wave
* ❕✅ Added Note Specific xmode
* ❕✅ Added Note Specific zigzag, zigzagZ

---

## OutFox 5.0.0 Pre-Release Candidate 042-a5 (Main PRETEST PlayTest Build) - June 24th 2023

Poptions and AllTheMods (part 1) build. God help me writing this... - Squirrel

* ❕✅ Fixed crash with some modfiles due to wrong function
* ❕✅ Remove 2003 era float overruns from game
* ❕✅ Fixed bug with legacy GL1.1 calls being used instead of 2.0-> ones when available
* ❕✅ Added ModsMap to the game
* ❕✅ Added new lua binding to enable backwards compatibility to the new mods system
* ❕✅ Added new fast abs function (xabs(x)) to the game
* ❕✅ Added new ActiveModsCol to the game
* ❕✅ Optimised comparisons in ArrowEffects
* ❕✅ Fixed bug with non-combo highscores overflowing and being saved incorrectly
* ❕✅ Fixed bug with alpha being applied on the be-mu/po-mu miss layers
* ❕✅ Fixed float compares on critical approach functions
* ❕✅ Fixed bug with tan mods in ragedisplay
* ❕✅ Fixed crash with game mode switching
* ❕✅ Fixed crash with theme switching on some modes
* ❕✅ Fixed some file closure calls being in the wrong place due to squirrel oopsie
* ❕✅ Optimised Column Specific mod reading so they don't run like ass
* ❕✅ Fixed bug with duplicate variables being pushed into our stack
* ❕✅ Fixed fake judgements being added when there is no player stage
* ❕✅ Added a new 'GetNoteAmount' system to the game
* ❕✅ Added new tapnote enums to the game
* ❕✅ Added new NoteBeatAdj to the game
* ❕✅ Added new def.notefield update loops to the game
* ❕✅ Added new shader support to notes and receptors
* ❕✅ Added new playeroptionssimple to ensure no performance loss in modes that do not need modding support
* ❕✅ Added new imagecache compression system to the game
* ❕✅ Added new Networkservicemanager system to the game
* ❕✅ Added new score saving and new user registration to the game
* ❕✅ Added new 'rate' system to limit updates and frame changes for models
* ❕✅ Added new API token system to the game
* ❕✅ Fixed Matrix math for shaders
* ❕✅ Added SSL support for the networking system
* ❕✅ Fixed compiling and support for windows and mac for SSL, ensuring they sign correctly
* ❕✅ Added ThemeSoundModes to the game
* ❕✅ Added server send and receive for scores, timing, judgements and user attributes
* ❕✅ Fixed missing player profile saving items
* ❕✅ Added a new way to load a NSkin board, so it doesn't leak memory
* ❕✅ Added new notefield previews to the game to support song wheels
* ❕✅ Added new Poptions system
* ❕✅ Added new methods to simplify the player options used on performance critical modes
* ❕✅ Fixed crashes with imagecache on SimplyLove and A3/Starlight
* ❕✅ Fixed order of calls for luaglobals
* ❕✅ Added new music wheel sorting to leak less memory
* ❕✅ Fixed crash on older themes when a player late joins
* ❕✅ Added new method to call some mods that were not properly set
* ❕✅ Added new faster math operations for mods
* ❕✅ Added new column checks so the array does not overflow
* ❕✅ Raised stats.xml size
* ❕✅ Added new column mod system to the game
* ❕✅ Added new approach mod snap system
* ❕✅ Fixed bug with songgroup vector
* ❕✅ Added new GetLogsPath for win32, though it should have been there a long time before
* ❕✅ Fixed bugs with legacy hard coded paths
* ❕✅ Fixed bugs with speed mods in new poptions code
* ❕✅ Added new KBX system support
* ❕✅ Fixed tween endings sometimes being skipped
* ❕✅ Fixed bug with mod replay/call order
* ❕✅ Added new clock system for some calls
* ❕✅ Fixed a microstutter bug call from 2005
* ❕✅ Fixed spline issues
* ❕✅ Removed legacy asserts on button calls
* ❕✅ Added Actor VanishPoint to the game
* ❕✅ Added new favourites system to the game
* ❕✅ Fixed crash on miniholds
* ❕✅ Added new mod aliases
* ❕✅ Added new lua functions to properly affect ActiveMods
* ❕✅ Added new ActiveMods list
* ❕✅ Added new Hitsound system to reduce lag
* ❕✅ Added new FT_Sound fixes to work with the timing system
* ❕✅ Added new CAMOD for taitai mode
* ❕✅ Changed BGA to be chart based for SSC/SM chart systems, to allow for per chart backgrounds
* ❕✅ Added new osu based key/hitsound support
* ❕✅ Added support for steps in getbga()
* ❕✅ Added new sound mutexes 
* ❕✅ Added new SSC hold metric features
* ❕✅ Added new ArrowEffectsOriginal for backwards support
* ❕✅ Added fixes to SimpleMods
* ❕✅ Added new randomseed
* ❕✅ Added new Groove mode, designed for modding, to prevent the normal dance mode from running mod systems it doesn't always need.
* ❕✅ Fixed bug with tinyycol approach
* ❕✅ Added Drawholdsandtapsinsameloop pref
* ❕✅ Added XScrolls segment type
* ❕✅ Added playeroptions.getstring
* ❕✅ Added change with tiny, old behaviour is TinyPull
* ❕✅ Added HoldCullMode
* ❕✅ Added ApproachType Modifier
* ❕✅ Added Alpha channel variations for the visibility of mods
* ❕✅ Restored RandomVanish
* ❕✅ Added two new mods, Randomise and Vanish to split randomvanish
* ❕✅ Added OrientX and OrientY
* ❕✅ Added column specific Zigzag and ZigzagZ
* ❕✅ Added column specific Sawtooth and SawtoothZ
* ❕✅ Added new caching method to fix deadlocks
* ❕✅ Added column specific Dizzy
* ❕✅ Added column specific Twirl
* ❕✅ Added column specific Roll
* ❕✅ Added column specific (Tan)Drunk
* ❕✅ Added column specific (Tan)DrunkY
* ❕✅ Added column specific (Tan)DrunkZ
* ❕✅ Added column specific Beat, BeatY, BeatZ
* ❕✅ Added GetFirst/GetLast DisplayedBeat take a column
* ❕✅ Added column specific Boost
* ❕✅ Added column specific Brake
* ❕✅ Added column specific ScrollSpeedMult
* ❕✅ Added column specific Timespacing
* ❕✅ Added column specific StealthMines
* ❕✅ Added column specific StealthHolds
* ❕✅ Added column specific ExtendHolds
* ❕✅ Added column specific Orient, OrientX, OrientY
* ❕✅ Added column specific (Tan)Tornado and (Tan)TornadoZ
* ❕✅ Added column specific Square and SquareZ
* ❕✅ Added column specific SpiralX, SpiralY and SpiralZ
* ❕✅ Added column specific ParabolaX, ParabolaY and ParabolaZ
* ❕✅ Added column specific CubicX, CubicY and CubicZ
* ❕✅ Added column specific CenteredPath
* ❕✅ Added column specific (Tan)Tipsy
* ❕✅ Added SetCurrentBeat and SetcurrentMusicSeconds
* ❕✅ Added JudgeScale from oITG
* ❕✅ Added Player.SendFakeJudgment
* ❕✅ Fixed bug with redundant islua command
* ❕✅ Fixed bug with sound copying

---

## OutFox 5.0.0 Pre-Release Candidate 042-a4 (Main PRETEST PlayTest Build) - June 18th 2023

* ❕✅ Fixed string.format breaking with no integer form
* ❕✅ Fixed CVE in cpr lib so we can compile for older OSs
* ❕✅ Fixed legacy linux build support
* ❕✅ Fixed compiler guards for cpr lib so it works with our system
* ❕✅ Added new be-mu/po-mu miss threshold for how long the miss layer remains visible
* ❕✅ Removed 2 pointless ASSERT calls as they no longer are relevant
* ❕✅ Fixed background draw in po-mu layers
* ❕✅ Fixed mac compile
* ❕✅ Adjusted singleton system to assist with memory management
* ❕✅ Fixed but with conditional states on pandathread
* ❕✅ Fixed backup/fallback for the new 'groove' mode option
* ❕✅ Fixed thread calling order, as we run slightly differently now to SM
* ❕✅ Fixed quirk in sound driver that can cause a lock
* ❕✅ Fixed win compile and loading
* ❕✅ Fixed endless loop with unlockman
* ❕✅ Fixed shader calls so they now use memory cleaner
* ❕✅ Allowed shaders to have wide multitexture support
* ❕✅ Allowed our shader system to use 16 TUs for modding
* ❕✅ Added new gettuslots() call for modders to know how many units they have available
* ❕✅ Make drivers TU Alloc shader aware
* ❕✅ Fixed TU used in our ffmpeg driver to be RPi and legacy ATI/AMD/Nvidia friendly

---

## OutFox 5.0.0 Pre-Release Candidate 042-a3 (Main PRETEST PlayTest Build) - June 9th 2023

* ❕✅ Fixed leak in be-mu backgrounds
* ❕✅ Added Fe-Dora build environment to support 37->
* ❕✅ Fixed background data loading in be-mu and po-mu
* ❕✅ Fixed quirk with invalid background changes on older BMS/PMS files
* ❕✅ Added MISS/POOR support for be-mu / po-mu
* ❕✅ Fixed Mac sound issues
* ❕✅ Fixed bug in fileopen
* ❕✅ Fixed memory leaks in file loading
* ❕✅ Fixed memory leaks in song parsing
* ❕✅ Fixed fonts double loading
* ❕✅ Fixed LoadingWindow memory leaks
* ❕✅ Tidied up all our macros
* ❕✅ Fixed performance issues with the notefields

---

## OutFox 5.0.0 Pre-Release Candidate 042-a1 + a2 (Main PRETEST PlayTest Build) - May 13th 2023

* ❕✅ Fixed leaks with file handles
* ❕✅ Fixed leaks with bad pointers
* ❕✅ Fixed loading window double cast, fixes a lag issue when loading on pi
* ❕✅ Fixed macro calls and optimised methods for tweens
* ❕✅ Fixed bugs with c-style code not being optimised
* ❕✅ Sped up tween math for mods
* ❕✅ Added ASin Math
* ❕✅ Fixed crash in lua with math.random
* ❕✅ Poptions optimisations for A-C - cleaning up the games code
* ❕✅ Fixed crash on newer linux clients requesting higher than supported colour profiles
* ❕✅ Optimised parser code pathways 
* ❕✅ Fixed portaudio compile on linux
* ❕✅ Fixed getposition on portaudio
* ❕✅ Fixed wasapi link on rtaudio
* ❕✅ Sped up math calculations for sine based tweens
* ❕✅ Fixed missing posmap on audio optimisations
* ❕✅ Fixed wheelbase item data sorting for future options for non-dance modes
* ❕✅ Removed autoptr from the game
* ❕✅ Let math.random accept numbers
* ❕✅ Fixed cmd lua support for 5.4.6
* ❕✅ Updated lua to 5.4.6
* ❕✅ Fixed gamemode pointer system
* ❕✅ Added more debug options on windows
* ❕✅ Fixed taiko noteskin count rolls
* ❕✅ Fixed buffer issue with msdfile
* ❕✅ Cleaned up notedisplay destruction
* ❕✅ Fixed pointer issues with ragetexture

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a9 - April 29th 2023

* ❕✅ Synced updates with the alphav-theme
* ❕✅ NEW! return to the portal link if portal was selected
* ❕✅ Auto Resize ScreenDebugOverlay on low definition (480p) themes
* ❕✅ NEW! restore #LASTBEATHINT to .sm files
* ❕✅ Fixed a slew of parsing bugs in the .sm parser
* ❕✅ Fixed leaked memory in the .sm parser
* ❕✅ Fixed bad update call in DrawPrimitives breaking some mod calls
* ❕✅ Fixed bug with access calls on GameSoundManager
* ❕✅ Fixed potential crash/freeze with ImageCache

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a8 - April 25th 2023

* ❕✅ Fixed bug with favourites not being found sometimes on some systems
* ❕✅ Fixed crash with favourites folder
* ❕✅ Fixed FileWrite Call
* ❕✅ Replaced library used for ImageCache to improve stability and Memory use
* ❕✅ Fixed bug with MIDI buttons not being seen after being saved to keymaps.ini
* ❕✅ Fixed bug with MIDI buttons not being saved on the Map Controller screen for MIDI controllers
* ❕✅ Fixed missing entries on InputDevice
* ❕✅ Added Wii & Wii-U controller support to our HIDAPI Driver
* ❕✅ Fixed stuck buttons on MIDI drumkits due to Channel 09 varying non-zero values.
* ❕✅ Fixed bug with buffer underrun on some sound cards
* ❕✅ NEW! 2 Player ParaPara Mode support with official PS2 controllers!
* ❕✅ Fixed missing official PS2 ParaParaParadise controllers on Mac and Linux
* ❕✅ Fixed bug in ParaPara input driver by rewriting it
* ❕✅ Fixed bug with duplicate controllers on Mac/Linux/Steam

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a7 - April 22nd 2023

* ❕✅ Fixed bug with multiple loads of FGChanges
* ❕✅ Fixed bug with some lua definitions not quite being nil
* ❕✅ Fixed bug with BGChanges crashing on invalid Enums
* ❕✅ Fixed bug with CheckEnum corrupting the lua stack
* ❕✅ Brought over 1-4 player PS2 official parapara controller input driver from Dragons
* ❕✅ Fixed bug with some vectors not being correctly handled in the background calls
* ❕✅ Fixed crash with bad math calls in music wheel
* ❕✅ Fixed chartkey loading 3 times on every action on the music wheel
* ❕✅ Fixed PlayCopy() crash
* ❕✅ Fixed incorrect usage of pushnil in NETMAN
* ❕✅ Fixed crash with enum call in ActorUtil
* ❕✅ Fixed pointer crash on file closing on some modfile calls
* ❕✅ Made the OTO (osu) parser much more stable, and added samplesounds/hitsound support
* ❕✅ Fixed a few wry mutex issues now we are planning for lower latency
* ❕✅ Fixed a reported tickhold bug
* ❕✅ Fixed the reported GetBGChanges() 'bug' by rewriting the methods, as they are now chart specific
* ❕✅ Fixed bug with mod columns calling 88 instances when we don't plan to have piano mode moddable
* ❕✅ Fixed crash with updateholdnotes
* ❕✅ Fixed crash in GameSoundManager
* ❕✅ Re-implement SSC hold metric features - Penalise tap score none/Judge hold notes on same row together/checkpoints flash on hold/immediate hold let go/combo break on immediate hold let go/require step on hold heads/checkpoint taps separate judgement
* ❕✅ Fix issue with GetBGA, by rewriting it to support steps
* ❕✅ Fixed bug with no keysoundfile clearance
* ❕✅ Added new support for OTO (osu) keysounds
* ❕✅ Fixed bug with missing FGChanges calls
* ❕✅ Fixed weird draw issue with some themes and GLAD renderer
* ❕✅ Fixed crash in steps creation
* ❕✅ Changed BGA to be chart based for SSC/SM files
* ❕✅ Fixed crash with favourites affecting speed mods
* ❕✅ Updated Docker builds
* ❕✅ Fixed crashes with Python2/Python3 IO boards
* ❕✅ Fixed bug with ASIO support on win32
* ❕✅ Added pulseaudio to PortAudio in prep for new sound back end
* ❕✅ Fixed clocks for rtAudio on mac/linux
* ❕✅ Added more info for statsoverlay
* ❕✅ Fixed crash with some lower() command calls
* ❕✅ Fixed CODESET offset bug reported by Rythmlunatic

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a6 - April 08th 2023

* ❕✅ Fixed crash on refcount
* ❕✅ Fixed bug with pro-explosions not falling back when not provided
* ❕✅ Fixed bug with calories being default goal on the alpha-v theme
* ❕✅ Fixed def.notefield preview autoplay not reloading on looped audio
* ❕✅ Restore Add and Scale check to smart timing windows
* ❕✅ Fixed ddrio for 32bit machines
* ❕✅ Fixed lua errors on course and endless modes
* ❕✅ Added sound options to themes
* ❕✅ Fixed favourites not loading BGAs
* ❕✅ Added SongPreviewVolume
* ❕✅ Added additional song folder master folder for BMS file support
* ❕✅ Changed UpdateDrawLoopSeconds to take FPS values
* ❕✅ Added option to disable hotswap controller support for performance
* ❕✅ Added set loops per second to ease CPU usage
* ❕✅ Fixed bug with buffer type in rtaudio
* ❕✅ Fixed bug with rounding error on syncing machine
* ❕✅ Fixed FPS inaccuracies
* ❕✅ Fixed bug with misplaced drawloop
* ❕✅ Fixed bug with overflow on sound buffers
* ❕✅ Show shader compile errors onscreen
* ❕✅ Added themepref for NoteDataLimit
* ❕✅ Fixed cast with clock resolution
* ❕✅ Fixed bug with large size notedata loading
* ❕✅ Fixed cache miss

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a5 - April 08th 2023

* ❕✅ Fixed clock method in new audio back end for linux/mac
* ❕✅ Added new round method for sound buffer
* ❕✅ Restored legacy SM-5 driver options for those that requested it
* ❕✅ Fixed bug with repeated samplerate calls
* ❕✅ Fixed missing API support in the main sound driver
* ❕✅ Fixed linux compile with rtAudio
* ❕✅ Fixed correct flags on device initialisation
* ❕✅ Fixed bad code in ragesound
* ❕✅ Fixed panda logger creation
* ❕✅ Added new soundwaves links on main page

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a4 - March 27th 2023

* ❕✅ Fixed Linux builds compiling for modern systems
* ❕✅ Fixed bug with a temp patch for uniformtextures overriding each other
* ❕✅ Added new FBO status information
* ❕✅ NEW! rtAudio stub and skeleton
* ❕✅ Fixed latency with some of the internal audio code
* ❕✅ Fixed audio latency and compile
* ❕✅ Fixed bug in Mac/Linux steam variants by downgrading to 5.2 rtaudio
* ❕✅ Fixed logging and device detection in Linux
* ❕✅ Fixed stuttering on rt-pulseaudio
* ❕✅ Fixed preference information and buffer edits
* ❕✅ Fixed 3.0 era particle animation processes
* ❕✅ Fixed bug with pandalog not using correct loc when set
* ❕✅ Added a new sound logfile for the new systems
* ❕✅ Fixed internal streamtime polling for audio
* ❕✅ Fixed bug with unavailable streams not being available due to a windows quirk
* ❕✅ NEW!! rt-Asio Driver
* ❕✅ NEW!! rt-DirectSound Driver
* ❕✅ NEW!! rt-WASAPI Driver
* ❕✅ NEW!! rt-JACK Driver
* ❕✅ NEW!! rt-ALSA Driver
* ❕✅ NEW!! rt-Pulse Driver
* ❕✅ NEW!! rt-OSS (4+) Driver
* ❕✅ NEW!! rt-CoreAudio Driver
* ❕✅ Fixed bug with legacy SM drivers trying to set a rate that's not supported
* ❕✅ Fixed bug in accuracy of sound by removing SM 2.5x era cruft
* ❕✅ Added new sound driver selection in the debug stats
* ❕✅ Fixed bug with missing favourites folder stuff on soundwaves, you can now use this
* ❕✅ Fixed crash on Jack not available - do not use this driver unless you run jack for now, we need to code the path for it.

---

### THIS BUILD HAS A NEW SOUND BACK END!!


This build utilises a new back end and completely does away with the old SM5 drivers. It was super heavily requested by the community that we have something configurable that could be used to lower latency in the game for key-sounded and hit sounded modes, so we delayed this build to squeeze it in. There are still a couple of bugs which will be ironed out, but for 99% of users, this build will work fine.

LOW LATENCY AUDIO GET!

With lower latency, comes some compromises. It is super clear and sharp, you have better clarity, it obviously uses new drivers, which include some new preferences, see below.


We have discovered Discord does NOT like low latency based drivers... AT ALL. please bear this in mind if you decide to play with ASIO/set your CoreAudio below 1024, and ensure you have a secondary sound card Discord can use, so you aren't greeted with silence.

WINDOWS:
ASIO supports down to a blocksize of 32 in the internal driver, now while you can set this in the new preferences (see below) if you hear crackling or garbled audio, just raise this a bit. You can use anything from 32 to 4096 as your block size, higher values being higher latency.

WASAPI supports from 64 to 4096, and replaces waveout as the default driver. It has the benefit of not being legacy or using an old back end to output, and can have it's buffer lowered to suit the system.

Lastly we have DirectSound, mainly due to the fact it has been requested for older windows builds, but users should always try to see if WASAPI (which is Vista ->) is available. DirectSound is 512 ->

The new driver has had to be sample rate locked and hardcoded to 44.1kHz right now due to limitations in the back end, but we will be removing all the old legacy code in the coming months, so you will be able to enjoy 48kHz clarity really soon.

LINUX:
ALSA now uses a new back end, as well as no longer using a 15 year out of date code pathway, we no longer have to patch it for OutFox. It fully supports shared mode, so no more silence on calls when you're using it, and it also behaves better on the Raspberry Pi/SoC board for arm, fixing the 10+ year old bugs. If your kernel is pre 4.12, you may get a crash on the first run due to the old kernel code, but the game should find your system devices properly on the second run. We're looking into this atm.

PulseAudio now runs without the ALSA hook, and again isn't exclusive or forces weirdness. It can run with low latency as well, as well as sharing properly. At this release, it will likely use the ALSA device, but we will be adding the option to choose the device the specific APIs can use, so watch this space for that. There is also a quirk with Pulse where it reports the output and input devices back to front, so we have put in a workaround for this too.

JACK - Jack now is built in without the need for extra hooks or compiler options, and simply just... works. If you do not use this driver, do not add it to your preferences, as this can cause a crash right now, it will be fixed in the final version of 041. JACK is also available on MacOS, a bonus feature there.

BSD/CONSOLE:
OSS 4+ is available for BSD builds

MACOS:
CoreAudio now runs newer code as well, which also fixes the odd quirk in Ventura with the audio thread sometimes dropping out. We will also add code for audio device handover, as this new driver supports it, so no more crashing when your bluetooth headphones die and disconnect. Be warned, however, Bluetooth audio can not take a too low block setting, so experiment.


### New Preferences in this build

SextetStreamInputFilename=
Used for the new Sextet input handler I forgot to code in >.>

SoundrtAudioAPIName=
This selects the audio back end for your system. It will be self populated on first run with a safe default, but you can override it with a comma'ed list of inputs.

You have a choice of the following:

MacOS
core - Use for CoreAudio
jack - Use for JACK

Linux
alsa - Use for ALSA
jack - Use for Jack
pulse - Use for PulseAudio
oss - Use for the Linux OpenSoundSystem

Windows
asio - Use for ASIO
wasapi - Use for WASAPI
ds - Use for DirectSound

They can be used as a list with commas, so "wasapi,ds,asio"

SoundrtAudioLastUsedCard=
This is a pref to highlight the last used card, it's purely for the internal driver, like 'lastseenvideocard'

SoundrtAudioNumberofChannels=
This pref is for number of output channels/speakers your system supports. It will be up to 8 when the code is written, but for now, leave it at 2, due to the legacy code. It will be ignored if you add anything else!

SoundrtAudioPreferredSampleRate=
This pref is for the samplerate of your device, and will be settable in time. It will return the preferred rate your card wants, but will sadly be set to 44.1 due to the restrictions of the legacy code. Will be unlocked when we remove the rest of RageSound

SoundrtAudioSetBufferSize=
This pref is where you set your latency block size. It supports 32 frame to 4096 frames as per the ASIO/latency standards. If your audio crackles or glitches, remember to adjust this, it is not a bug in the game! With lower latency comes a bit more instability, so bear this in mind when you adjust this value.

Linux users will need a lowlatency compiled kernel and preferrably a kernel newer than 4.12 to take advantage of this. MacOS users need Big Sur to use < 256, and Windows 7+ for < 128

This driver is not enabled on windows yet due to some quirks with windows 10/11 which we are looking into.

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a3 - March 19th 2023

* ❕✅ Fixed bug with some windows versions crashing on boot with a weird waveout quirk
* ❕✅ Fixed misaligned pomu noteskin layouts on bun/cat/retro skins
* ❕✅ NEW! Be-mu/Po-mu backplate support - they run like gh/backplates
* ❕✅ Fixed crash with textbanner if steps are empty
* ❕✅ NEW! Actor Screen Textures!! These work similar to nitg AFTs
* ❕✅ Fixed transparency issues with opengl
* ❕✅ Fixed bug with AFTs not affecting FOV outside of itself
* ❕✅ Fixed triple sort call on musicwheel
* ❕✅ Fixed visible list on EffectModes
* ❕✅ Fixed FOV for AST/AFT so they are the same
* ❕✅ Fixed cache bugs with bannercache
* ❕✅ Fixed crash when taking screenshot
* ❕✅ Fixed hang when taking screenshot
* ❕✅ Fixed odd setlocale bug
* ❕✅ Fixed leegacy GL pipe for AFT/AST
* ❕✅ Fixed re-sorting stutter on musicwheel
* ❕✅ NEW! Added Din's DDRIO Driver adjusted for OF
* ❕✅ NEW! Added Din's ITGIO lights fixes
* ❕✅ NEW! Added Din's Lights Exports Fixes
* ❕✅ NEW! Added Din's PIUIO/LEDs/stac drivers and fixes
* ❕✅ Fixed sextetstream compiling
* ❕✅ NEW!! Input SextetStream driver
* ❕✅ Fixed bug with missing lights on sextetstream
* ❕✅ Fixed typo so pacdrive now works on 32 AND 64bit windows
* ❕✅ Fixed bug with density data so it's now done by engine
* ❕✅ Fixed lag with datagen from decompress
* ❕✅ Fixed crash with filedriver if the type isn't in map

---

## OutFox 5.0.0 Pre-Release Candidate 041 -a1+a2 - March 7th 2023

* ❕✅ Fixed crash with legacy arm builds
* ❕✅ Fixed crash on miniholds
* ❕✅ Fixed crash with ubuntu <= 17.10 users
* ❕✅ Fixed crash with arm + legacy builds
* ❕✅ Fixed crash with soundcards on Windows 8+ (Thanks EvieUwO for report)
* ❕✅ Fixed stuck buttons on rtMIDI input (Thanks LightHexagon for report)
* ❕✅ Fixed e-drums MIDI velocity channel quirk (Thanks LightHexagon for report)
* ❕✅ Fixed latency/lag in BMS/be-mu mode making it unplayable (Thanks Daniel Rotwind for report)
* ❕✅ Fixed latency/lag in PMS/po-mu mode making it unplayable (Thanks goodsun for report)
* ❕✅ Fixed latency/lag in DTX/gddm mode making it unplayable (Thanks goodsun for report)
* ❕✅ Fixed AMod/CAMod/AVMod speed mod issues
* ❕✅ NEW! FBO DoubleBuffer System for our render pipe
* ❕✅ Fixed bug with lack of stencil support on FBOs in MacOS
* ❕✅ Fixed FBO Transparency with modfiles
* ❕✅ NEW! Added new 'PowerOfTwo' variable for AFTs (Requested by our Modding community)
* ❕✅ Fixed GLAD FBO system for ARM systems
* ❕✅ Fixed bug with draw update with receptors and note flashes

---

## OutFox 5.0.0 Pre-Release Candidate 040 (Main + Steam Playtest Build) - March 7th 2023

* ❕✅ Fixed micro-stutter math overflow bugs in the approach code introduced in upstream in 2005
* ❕✅ Fixed math code-paths that caused a lag stall on Pre-2017 architecture
* ❕✅ Fixed order of draw for SimpleHolds BottomCap
* ❕✅ Fixed missing items on NSIS installer for our non-steam Windows builds
* ❕✅ Fixed winding order on our GL pipe - Raspberry Pi, and older systems should love us a bit more now
* ❕✅ Fixed bug with missing Fake notes writing to cache so they weren't miss on the first load
* ❕✅ NEW!! - Built in favourites system to the default (soundwaves 0.4.x) theme!
* ❕✅ Fixed bug with SaveMachineProfile... not saving on some newer Linux Builds
* ❕✅ NEW!! - Created a new ActorNoteFieldBoard metric to avoid legacy (StepMania 5.x) Noteskin problems/lua asserts
* ❕✅ Fixed bug in .TJA parser missing credits for #NOTEDESIGNER
* ❕✅ Fixed 21 year old bug in MenuTimer
* ❕✅ Fixed Accuracy in Player Options on the snapping options
* ❕✅ Fixed crash sometimes in profiles where the theme didn't support fitness/calories
* ❕✅ Fixed banner cache system on both themes
* ❕✅ Fixed bug with Auto generated chart loading on LuaWheel
* ❕✅ Fixed theme layout bugs

---

## OutFox 5.0.0 Pre-Release Candidate 039 (NON Steam Playtest Build) - February 24th 2023

* ❕✅ Fixed Linux building platform
* ❕✅ Updated Alpha V theme - should be less buggy now
* ❕✅ NEW!! - Use SoundDevice=0 (device number) to pick a sound card the game uses to output on the wave out sound driver on windows. (Thanks SenPi/Teej from ITGM, though we had to rewrite it for OF)
* ❕✅ Fixed crash on .osu/.osz files that were broken
* ❕✅ Fixed bug with approach mods occasionally skewing with a new snap feature
* ❕✅ Fixed bug with SongGroup vector causing leaks on the wheel
* ❕✅ Fixed edge crash on windows 7/10/11 with the logs folder when not using a portable.ini
* ❕✅ Fixed hardcoded logpath crashing non-mac OSs
* ❕✅ Fixed bug with KBX mode crashing on jukebox
* ❕✅ Fixed bug with some tween ending times being skipped
* ❕✅ Fixed bug in main loop with some 'modern' 2003 windows XP optimisations
* ❕✅ Fixed bug with 'framey' (slightly stuttery) files
* ❕✅ Fixed frame jitter bug added in 2005, that was causing fDelta to reverse
* ❕✅ Fixed bug with ready bar not clearing at the beginning of a song
* ❕✅ Fixed bug with group folder banners not loading
* ❕✅ Fixed bug with low quality banners not loading/being used

---

## OutFox 5.0.0 Pre-Release Candidate 038 (NON Steam Playtest Build) - February 21st 2023

* ❕✅ Fixed bug with mac bundle modules
* ❕✅ Add new PREIMAGE support for taiko tja file banners
* ❕✅ Fixed bug with windows compilation
* ❕✅ Fixed bugs with imagecache crashing
* ❕✅ Fixed some memory leaks in imagecache/musicwheel
* ❕✅ Fixed loading call for NSkin boards
* ❕✅ Fixed crash with AU on mac when external output sources are disconnected
* ❕✅ Fixed Def.Text not showing textures on macos
* ❕✅ Added lane colours to pomu noteskins
* ❕✅ Added new LyricLoader class which will support SRT/SSA/VTT files in time!
* ❕✅ Fixed bug with incorrect delete on music wheel
* ❕✅ Fixed crash with scrolling too quickly on music wheel
* ❕✅ Fixed loading of banners on music wheel causing a crash
* ❕✅ Fixed compiler being odd with zlib variables clashing
* ❕✅ Fixed bug with win32 locale
* ❕✅ Fixed slowdown in lua parsing
* ❕✅ Fixed glcontext creation
* ❕✅ Fixed bug with updateluaglobals not working on language change
* ❕✅ Added new math functions to reduce stutter on the SBC/Pi builds
* ❕✅ Fixed missing garbage collection on music wheel (reported by Dom)
* ❕✅ Fixed around 150 rounding issues in our math compilation causing slowdowns
* ❕✅ Added Editor support for TapNoteSource_Fake - to make the note a fake, use shift + n or shift + m, and remember if you use them! They will allow all things to be fakes. Requested by Mostly_Harmless
* ❕✅ Raised Stats.xml max size to 144MB
* ❕✅ Fixed crash with late joining on some systems and themes
* ❕✅ Fixed more bad math
* ❕✅ Fixed edge case crashing with creeping NaNs
* ❕✅ Fixed crash on column mods that were requesting values out of range

---

## OutFox 5.0.0 Pre-Release Candidate 037 (NON Steam Playtest Build) - January 24th 2023

* ❕✅ Fixed zlib compile that was blocking linux builds
* ❕✅ Fixed merger with SDL breaking some controllers on mac/linux
* ❕✅ Fixed duplicate definition in OF SDL patches breaking keypad enter
* ❕✅ Rewrote PacDrive to not use broken libUSB deps
* ❕✅ Fixed lua errors crashing the game on invalid enums, we can safely warn
* ❕✅ Added new Actor Screen Texture Skeleton WIP
* ❕✅ Fixed beginLine()/endLine() overflow on SSC/Pump parser/writer causing edited songs to sometimes be infinite
* ❕✅ NEW! Added OG-Classic be-mu noteskin
* ❕✅ NEW! Added TapNoteSource_Fake - now any note can be a fake; NO Editor Support yet, coming in later build!
* ❕✅ Fixed percentage done from directory to total songlist in the loading window
* ❕✅ Fixed some math overflows in RageDisplay
* ❕✅ Fixed hold rendering and checking due to overflow
* ❕✅ Fixed crash in RageFileManager locking up the cache
* ❕✅ Reset fDeltaTime correctly in the actor stack
* ❕✅ Fixed heap crash with discord...

---

## OutFox 5.0.0 Pre-Release Candidate 036 (NON Steam Playtest Build) - January 1st 2023

* ❕✅ Fixed bad call in linux build process
* ❕✅ Fixed USBDriver remaining calls left in unix and mac now they are gone.
* ❕✅ Fixed math overflow preventing the AxisFix working on windows 10 (win32 legacy input driver)
* ❕✅ Fixed math overflow on win32 legacy preventing the AxisFix pref working on Windows 7 and 8, thanks Microsoft
* ❕✅ NEW! Added Axis Fix support to Linux/Mac via SDL2 driver. If you have a pad and are on one of these operating systems, let me know so I can write up how to prepare and set up your fix.
* ❕✅ NEW! Added Axis Fix XInput support to windows 10/11 on the SDL Driver.
* ❕✅ Fixed bug with Para Para controller not being detected when some pad configurations were set.
* ❕✅ Fixed bug with HIDRAW on Windows and MacOs crashing when a controller was plugged in.
* ❕✅ NEW! Added new InputSet* Preferences to bring all the Input systems closer together than using odd settings. Do not use InputSetHIDAPI/InputSetRAWAPI at this time as it needs to be finished:

The new preferences are as follows:

Allows a player to specify if they are using arcade or custom controller hardware.
m_bInputSetArcade

Allows SDL to toggle the mapping method for joysticks via XInput.
m_bInputSetXInput

Allows SDL to toggle the mapping method for joysticks via DInput. (Windows Only)
m_bInputSetDInput

Allows SDL to toggle the mapping method for joysticks via HIDAPI.
m_bInputSetHIDAPI

Allows SDL to toggle the mapping method for joysticks via RAWINPUT.
m_bInputSetRAWAPI

Allows the user to set a DeadZone value. Useful for Axis Fixing and Configuring
m_iInputSetJSDeadzoneValue

Allows the user to set the desired input system on Linux, either /jsX or /eventX.
m_bInputSetLinuxJSEndpoint

* ❕✅ Removed m_bXInputUseOldJoyStickMapping, m_iJoystickDeadZone, m_bUsingArcadePads, m_bUseLinuxJS
* ❕✅ Added new CRC support to SDL driver for future use

---

## OutFox 5.0.0 Pre-Release Candidate 035 (NON Steam Playtest Build) - December 30th 2022

* ❕✅ Updated Taiko noteskins with the new features
* ❕✅ Began pipewire/wayland support on drivers
* ❕✅ Added missing climits header where required
* ❕✅ Add GameState:GetGoalPercentComplete functions
* ❕✅ Sync up changes in the alphav-dance theme
* ❕✅ Remove bad C code in RageUtil
* ❕✅ Update upstream SDL2 to 2.26.1
* ❕✅ Added SDL OutFox patches
* ❕✅ Fixed FreeType building
* ❕✅ Tried to fix corrupted iTrack which causes a crash on MacOSX
* ❕✅ Fixed crash on shitpost osu charts
* ❕✅ Fixed OTO scientific notation crashes
* ❕✅ Remove LibUSB - PLEASE TEST ON WINDOWS 7!!!!
* ❕✅ Added new VTT/SRT/SSA/LRC parser skeleton in prep for new lyric filetype support
* ❕✅ Added new .obj file loader - Thanks to Jewel from UKSRT for the help!

---

## OutFox 5.0.0 Pre-Release Candidate 034 (NON Steam Playtest Build) - December 28th 2022 (MACOS SPECIFIC UPDATES)

This build addresses issues related with the parser modules not loading on other Macs due to the linker process.

---

## OutFox 5.0.0 Pre-Release Candidate 033 (NON Steam Playtest Build) - December 27th 2022 (MACOS SPECIFIC UPDATES)

This addresses bugs related with crashes on macOS introduced on Ventura.
* ❕✅ Updated SDL to 2.26.1
* ❕✅ Remove bad C code from RageUtil
* ❕✅ Removed libUSB dependency causing crashes on macOS.

---

## OutFox 5.0.0 Pre-Release Candidate 032 (NON Steam Playtest Build) - December 22nd 2022 (LINUX SPECIFIC UPDATES)

* ❕✅ Fixed xrandr version mismatch preventing the game seeing it installed
* ❕✅ Fixed missing wayland compatibility (test if you like, probably still needs work)
* ❕✅ Fixed missing pulseaudio hooks on newer ubuntu 20->
* ❕✅ Fixed missing pipewire hooks on newer ubuntu 20->
* ❕✅ Fixed bug with XCB not initialising correctly
* ❕✅ Fixed missing XTST lib not being used causing a crash on newer ubuntu (21->)
* ❕✅ Fixed missing DRM support
* ❕✅ Fixed version mismatch on VA and X11 on newer ubuntu
* ❕✅ Fixed mismatch with sndio on newer ubuntu
* ❕✅ Added new build environment for Modern Ubuntu (20->)
if you use this on 18.04, you WILL need to ensure you have updated your system and have the -backports repositories for some of the newer libraries.

This is purely testing at the moment for linux users, but please let me know if there are any issues - Squirrel

---

## OutFox 5.0.0 Pre-Release Candidate 032 (NON Steam Playtest Build) - December 22nd 2022

* ❕✅ Fixed crash with empty string on TJA parsing
* ❕✅ Fix crash with Count Holds on TJA parsing
* ❕✅ Fixed missing BALLOON support on TJA parsing
* ❕✅ Fixed missing Counted Hit support on TJA parsing
* ❕✅ Added Taitai count hold support
* ❕✅ Fixed Audio Unit panics on macos 13+
* ❕✅ Fixed Audio Unit buffer allocation on macos 13+
* ❕✅ Fixed Audio Unit device selection on macos 13+
* ❕✅ Fixed Audio Unit log spam on macos 13+
* ❕✅ Fixed issue with no normals being sent on CompiledGeometry
* ❕✅ Added setting the rate of the animation of the material on a model
* ❕✅ Fixed crash with empty string on TJA parsing
* ❕✅ Fixed issue with double press on taiko drum inputs
* ❕✅ NEW! Changed options for Audio Volume in the debug menu.

Sounds can be assigned to either Attract/Effect/Sound, and can be controlled in the menu. The old 'Effect Menu' is gone, and allows you to set the type of audio you wish to edit. Attract volume works on the Jukebox/Attract screen, and can now also be set ABOVE 100%, to a maxium of 200%, for situations where audio lines are quiet and you need a boost for a cabinet.

PLEASE NOTE: This can cause the audio to clip/distort at high volumes, and we are not responsible for your use of this. It has been a very highly requested community feature and we are happy to be able to bring it to you in this build.

Use R to change the Sound Type, and T and Y to set the volume Down and Up respectively.
* ❕✅ Added matrix splitting options for CompiledGeometry
* ❕✅ Fixed oversight on SetSecondsIntoAnimation
* ❕✅ Fixed font reloading on resolution change
* ❕✅ Fixed font corruption on resolution change
* ❕✅ Added new sound types to be supported and run within the themes
* ❕✅ Fixed issue with missing hiddenregions and hold noteflashes
* ❕✅ Fixed issue with pump holds missing and not being able to be reclaimed
* ❕✅ Fixed crash with notepath vertex data
* ❕✅ Fixed offset on TJA files, causing skew on playback, thank you to tana. in the TJADB server for the assistance!
* ❕✅ Removed ancient HighScoreList::RemoveAllButOneOfEachName() for a newer function - Needs testing
* ❕✅ Fixed crash with 'phantom' BALLOONs in TJA files - Charts that do not specify a value for each BALLOON
* ❕✅ Added BALLOON default hit value of 5 to align with the expectations of the taiko community.
* ❕✅ Added SMA support back from LTS4 due to the number of community requests - please check them if you use this format
* ❕✅ Fixed crash with Windows XP era macros confusing the compiler on 32bit windows
* ❕✅ Fixed errors with SMA files being offset due to a math overflow
* ❕✅ Fixed crash with all parsers due to a legacy 2004 bug
* ❕✅ Fixed timeout bug with MEMCARDMAN preventing memory cards working in the game
* ❕✅ Fixed missing memory card support for cabinets - please test and let us know!

---

## OutFox 5.0.0 Pre-Release Candidate 031 (Steam Playtest Master) - November 26th 2022

* ❕✅ Fix crash with lxio on win32/linux 32bit operating systems
* ❕✅ Change behaviour of assist clap and metronome to continue even if player is dead at community request
* ❕✅ NEW! Added ImageCache 2022, with an improved system for GPU ready textures etc
* ❕✅ Fixed crash with notedata
* ❕✅ Fixed crash on first note press on some modes
* ❕✅ Fixed crash with music wheel freeze on para mode
* ❕✅ Fixed forever loop in legacy stepmaniaonline code
* ❕✅ Fixed system capabilities issue for windows 7
* ❕✅ Fixed issue with needless image preload system
* ❕✅ Fixed offsets for column renderer
* ❕✅ Fixed digitaloffset math
* ❕✅ Fixed missing techno graphics
* ❕✅ Fixed legacy FFMPEG code path breaking on slow loading systems - Themers need to be aware of tween times on loading charts on music wheels, these can still cause a crash if not set right due to a race condition. Tween waiting times should be around 0.4 to 0.8 if a user is scrolling so the wheel doesn't load resources the game doesn't need.
* ❕✅ Fixed compatibility issue with formatting pixel data
* ❕✅ Fixed TJA Measure commands 
* ❕✅ Fixed TJA BPM changes from making charts out of sync
* ❕✅ Fixed TJA Scroll commands making charts out of sync
* ❕✅ Fixed TJA fast scrolling - SET YOUR GAME TO CAMOD IN SONG OPTIONS
* ❕✅ Fixed TJA timing entries

---

## OutFox 5.0.0 Pre-Release Candidate 029 & 030 (Steam Playtest Master) - November 11th 2022

* ❕✅ Fix crash with Matrix generation on some older modfiles
* ❕✅ Added new game generation to cmake for windows api
* ❕✅ Fix crash with object deletion in draw pipe
* ❕✅ Add new boxing mode
* ❕✅ Fixed dynamic library loading for steam
* ❕✅ Fix missing failimmediate option being saved on KBX mode
* ❕✅ Fixed bug with missing thread mutex on song loading
* ❕✅ Fixed crash with missing stagemodel init
* ❕✅ Fixed crash with steam builds on linux
* ❕✅ NEW! Fixed legacy arm builds for embedded armv7 boards
* ❕✅ Fixed Opengl selection for linux builds should fix resolution issue
* ❕✅ Modernised build environment for new outfox specific options
* ❕✅ Fix mines on pump and dance
* ❕✅ Fixed type boolean
* ❕✅ Fixed be-mu/po-mu/gddm/gdgf preview sounds
* ❕✅ Fixed crashes with minimaid on linux, needs to be rebuilt
* ❕✅ NEW! Added new 80% pass failtype for be-mu/po-mu
* ❕✅ Fixed bug with DTX loadheader
* ❕✅ Fixed crash with hiddendata calls on editor
* ❕✅ Fixed offset support on Autokeysounds
* ❕✅ Added language functions for thememanager
* ❕✅ Fixed mac build chain and command scripts for XCode
* ❕✅ Fixed crash with legacy opengl on legacy linux distros (pre 2010)

---

## OutFox 5.0.0 Pre-Release Candidate 028 - November 8th 2022

* ❕✅ Fix crash with GLAD on ATI era cards
* ❕✅ Fix GameSelect
* ❕✅ NEW! Added new "Ex" versions of Back and Elastic tween eases for Actors
* ❕✅ Fixed bug with texture resolutions rounding incorrectly on some functions
* ❕✅ NEW! Added new SetUpdateFPS() function to set the desired FPS of the update loop for Actors
* ❕✅ Fixed ez2 real from crashing on Versus
* ❕✅ Fixed crash on deltatime on Actors
* ❕✅ Fixed crash with Def.Notefield() not getting a defined playernumber
* ❕✅ Widened autokeysound track allowance to 32 
* ❕✅ Added Beatin po-mu Judgement
* ❕✅ NEW! BMS-like parser override functions to bind and prevent duplication and bad code use
* ❕✅ Fixed upstream bug with keysounds ending early on BMS-like songs
* ❕✅ Fixed bug with sounds unloading not at EOF
* ❕✅ Fixed vorbis flags
* ❕✅ Restored PMS/BME extended hidden keysound channels
* ❕✅ Fixed hold keysound spam
* ❕✅ Fixed texture handle get functions
* ❕✅ NEW! Added Experimental Option & Pref: AutoKeySoundBMS. This preference changes how the keysounds play in be-mu/po-mu/gddm/gdgf, with the option of OutFox being usual behaviour, setting BMS plays the keysound when you hit the button, and FULL all the keysounds are set to BGM layer so you can miss without it affecting the melody of the song
* ❕✅ Fixed crash with bad GL detection, if you crash try re-running the game to set the pref correctly
* ❕✅ Cleaned up code in LLW
* ❕✅ Fixed bug where game would hang on musicwheel with high note/mine/etc counts over 9000 on NPS chart
* ❕✅ NEW! Added new BMSHeaderLoad pref to disable loading header files on older HDDs/Rpi/SteamDeck
* ❕✅ NEW! Added threaded songloader, with a preference m_NumSongLoadThreads to select the number of threads. Default is 2, but you can up this to a maximum of 8 on NVME/SSD drives
* ❕✅ NEW! Fixed MineFix from affecting other Modes
* ❕✅ NEW! NSIS installer
* ❕✅ Fixed DTX parsing difficulties

---

## OutFox 5.0.0 Pre-Release Candidate 027 - October 31st 2022

* ❕✅ Fix bongo notes sometimes clashing with taiko ones in the parser
* ❕✅ Fix mode graphics to allow players to use bongo
* ❕✅ Fix GameSelect.lua
* ❕✅ NEW! Initial ShaderManager skeleton
* ❕✅ Fix crash with needless commands in GLAD renderer
* ❕✅ Fix ShaderManager scope in the renderers
* ❕✅ Fix Branding for future builds
* ❕✅ Add Steam Playtest Code and API ready for approval from Valve
* ❕✅ Fix Steam build compilation for MacOS

---

## OutFox 5.0.0 Pre-Release Candidate 026 - October 25th 2022

* ❕✅ Fix Krazy noteskin crashing
* ❕✅ Fix NSIS code

---

## OutFox 5.0.0 Pre-Release Candidate 025 - October 25th 2022

* ❕✅ NEW! Bongo Mode!
* ❕✅ NEW! Bongo Autogen from TJA & Osu (though due to chart quality, osu can be sketchy)
* ❕✅ NEW! Krazy noteskin for bemu/kbx/pomu
* ❕✅ Fixed dynamic libs for ffmpeg base
* ❕✅ Fixed bug with non-shader ffmpeg not being used in some cases
* ❕✅ Fixed flags in ffmpeg causing slow decoding
* ❕✅ Fixed shader ffmpeg passing diffuse instead of alpha
* ❕✅ Fixed some floats
* ❕✅ Added new TextureModes: Decal, Replace, Blend, Invisible
* ❕✅ Removed old mipmap code that didn't do anything, to restore in later driver
* ❕✅ Fixed lirocode crash on bms
* ❕✅ Fixed mine check in bms parser so mine gimmick charts are parsed correctly
* ❕✅ Add 'DanceLegacyMode' to ensure disconnection from SM 'Everything is DDR' pathing
* ❕✅ Fixed BMS parser substrings, so difficulty and subtitles now show as they should
* ❕✅ Fixed BMS difficulty selection and titles, and add the proper number of difficulties
* ❕✅ Fixed BMS not having D6 and D7 for Hyper/Insane difficulty support
* ❕✅ Fixed BMS header data loading to speed up the game in general

---

## OutFox 5.0.0 Pre-Release Candidate 024 - October 17th 2022

THEME: (From Jose)

* ❕✅ Rewritten Judgement loading procedure.
This basically now lets the game record each judgment graphic per
timing window instead of a singular option to rule them all. This
would've become messy if we've kept it like that.
NOTE: This will run locally on the theme for now, to test if the
new functionality is stable to transfer to fallback.

* ❕✅ Music wheel is now dimmable when entering options
* ❕✅ Touch controls are now a toggle
Now looking back, I can see that this whole thing can become a mess
if we let everything be shown at once, so now the Touch controls are
part of a toggle located on the Options menu, which is off by default.
* ❕✅ Speed is now the main option on Player Options
* ❕✅ Fixed PrevScreen on KnownBugs (Reported by Moneko)
* ❕✅ Apply PlayMode upon entering the music wheel
* ❕✅ Hide menu timer from ScreenEvaluation for now.
* ❕✅ Fix last difficulty selection when returning the wheel
* ❕✅ Tweaked Song Info box to include a banner.
* ❕✅ Fixed video banners not respecting fading.
* ❕✅ Tweaked player information pane on select music
* ❕✅ Noteskin now applies when changing noteskins.
* ❕✅ Fix update for Measure Count display
* ❕✅ Cleanup debug messages

BMS/PMS/DTX/GDA
* ❕✅ Auto switch to HQ mp4 movie BGA if available
* ❕✅ Fixed title being overwritten resulting in the directory name being used
* ❕✅ Fixed regex causing title to be empty
* ❕✅ Removed SM3.9 era cruft from the parsers 
* ❕✅ Removed defunct Unicode conversion as we do it properly now
* ❕✅ Fixed commonsubstring overflows resulting in bad title/translit title
* ❕✅ Fixed bad SM4 code breaking some #subtitle entries
* ❕✅ Fixed multi-layer backgrounds not being initialised correctly
* ❕✅ Removed bad converting code for artist and genre
* ❕✅ Fixed bug causing cache generation lagging on initial parsing on first boot
* ❕✅ Fixed missing #subtitle support on BMS files
* ❕✅ Added subtitle options for BMS files
* ❕✅ Added new Chartsubtitle option for lua SSM
* ❕✅ Added new ChartTitle options for lua SSM
* ❕✅ Added new ScreenGameplay GetSound()
* ❕✅ Fixed sounds not ending
* ❕✅ Fixed Background Crash that was reported
* ❕✅ Fixed lag on loading window
* ❕✅ Added new Peaks for audio visualiser
* ❕✅ Added new def.AudioVisualiser

Def.AudioVisualizer Info:

It can be added to any existing actorframe, in themes, modfiles and noteskins!

To use it just use the following commands (UpdateRate is in seconds: 0.01s to 10s)

```
return Def.ActorFrame{
  Def.AudioVisualzer{
    Amount=128, -- The amount of colums, its from min of 16 to a max of 128.
    LinearPeaks=true, -- define if we want lenear peaks, as in a slow animation when it goes back to 0.
    PeakHeight=40, -- the hight of the columns,
    UpdateRate=0.01, -- the update rate of the columns, the lower the faster, between 10 and 0.01.
    OnCommand=function(self)
      self:SetSound(--[[ A RageSound to set--]])
     -- if SetSound is not set, it will fallback to the cur playing music, this does not work for screen gameplay, in screengameplay do
      self:SetSound(SCREENMAN:GetTopScreen():GetSound())
    end    
  }
}

```

---

## OutFox 5.0.0 Pre-Release Candidate 023 - October 12th 2022

---

## OutFox 5.0.0 Pre-Release Candidate 014 - August 26th 2022

* ❕✅ NEW! Added bongo note types and .tja/.osu parser support ready for implmentation
* ❕✅ Fixed bug with MIDI where there would be a crash when shutting down
* ❕✅ Fixed bug with crash when unplugging MIDI keyboards on Mac 12/13
* ❕✅ Added new method to generate notefields to fix crashes
* ❕✅ Fixed legacy bug with files being deleted twice
* ❕✅ Fixed bug with missing kickbox items
* ❕✅ Fixed SM5 era bug with glyphs disappearing
* ❕✅ Fixed bug with misinterpreted spheremapping
* ❕✅ Fixed crash with missing noteskins
* ❕✅ Added new TTFActor Prototype; documentation to come shortly
* ❕✅ Fixed bug with mutex unlocking when file get fails
* ❕✅ Fixed bug with limited inline on row resolution
* ❕✅ Fixed crash with unreleased threads
* ❕✅ Fixed bug with spheremapping in GLAD
* ❕✅ Fixed 'permanentlydeletechart'
* ❕✅ Fixed bug with race condition between file threads
* ❕✅ Fixed bug with renderstates being dereferenced in windows
* ❕✅ Fixed bug with scrolling BGAs
* ❕✅ Fixed scrolling actor bugs

---

## OutFox 5.0.0 Pre-Release Candidate 013 - August 16th 2022

* ❕✅ Fixed bug with windows derefs
* ❕✅ Fixed texture scroll overflowing onto the ui
* ❕✅ NEW! - Added FourV2Lane Pump Noteskins
* ❕✅ NEW! - Added Global Board Noteskin
* ❕✅ NEW! - Dynamic Mode Icons for Discord RPC
* ❕✅ NEW! - Darkfox icons for Discord RPC
* ❕✅ Fixed bug with long windows names on Discord RPC
* ❕✅ Fixed crash on new M2 chip Macs
* ❕✅ Fixed bug with no bit type returned on linux
* ❕✅ Fixed crassh on PIU loader
* ❕✅ NEW! - SteamAPI setup and init (not active on these builds ofc)
* ❕✅ Fixed bug with build deps on steam builds
* ❕✅ Updated steam libs to 155
* ❕✅ NEW! PandaLog
* ❕✅ NEW! Crashlog system

---

## OutFox 5.0.0 Pre-Release Candidate 012 - August 14th 2022

---

## OutFox 5.0.0 Pre-Release Candidate 011 - August 11th 2022

The Crash Dash Part III edition:
* ❕✅ Fixed bug with discord lib working preventing the core initialising
* ❕✅ Set finger id for 1 for now.
* ❕✅ Fixed bug with missing touch events
* ❕✅ Fixed missing finger events on actors
* ❕✅ Fixed cross platform touch support
* ❕✅ Fixed bug with FailImmediate not being saved to profile
* ❕✅ Fixed simpleholds bottomcap
* ❕✅ Fixed bug with texture translation
* ❕✅ Fixed colour buffers
* ❕✅ Fixed docker builds for linux alpha V
* ❕✅ Fixed refcount on model manager causing edge crashes
* ❕✅ Fixed bug with density generation
* ❕✅ Added GetWorstTapNoteScore()
* ❕✅ Added GetAbsoluteDest X/Y
* ❕✅ Added UpdateThemeLanguage()
* ❕✅ Added AVMod for pump
* ❕✅ Added NoMines for simplePO
* ❕✅ Added DebounceCoinInputTime() to ScreenOptionsMasterPrefs

---

## OutFox 5.0.0 Pre-Release Candidate 010 - August 8th 2022

---

## OutFox 5.0.0 Pre-Release Candidate 009 - August 6th 2022

The Crash Dash Part I edition:
* ❕✅ Fixed crash with windows input handler
* ❕✅ Fixed crash with resetting graphics mode
* ❕✅ Fixed crash with changing themes
* ❕✅ Fixed hang with changing themes to infinitessimal/starlight
* ❕✅ Fixed hang on some screen changes
* ❕✅ Fixed hang on screen gameplay with pump charts and dance mod-files
* ❕✅ Fixed crash with some mod-files
* ❕✅ Fixed hang with SL on main menu/profile screen
* ❕✅ Fixed crash on screen evaluation on non-default themes
* ❕✅ Fixed multiple crashes on game close 
* ❕✅ Fixed hang on adding or removing a controller on Windows
* ❕✅ Fixed crash on SMX pad initialisation on Windows
* ❕✅ Fixed crash with GameState calls being out of order on game shutdown
* ❕✅ Fixed crash on editor exit 
* ❕✅ Fixed crash with game being left on for longer than 62 minutes
* ❕✅ Fixed crash with game releasing devices on Windows
* ❕✅ Fixed crash in screengameplay
* ❕✅ Fixed crash when 'reloading songs' on any theme
* ❕✅ Fixed crash on alt-tab on non-default themes
* ❕✅ Fixed crash on some older (pre2013) GPUs crashing when using alt+enter
* ❕✅ Fixed crash with the sound buffer overflowing 
* ❕✅ Fixed crash with editing chart playback when stops/warps are used
* ❕✅ Fixed crash with sounds on keysound thread at evaluation screen on be-mu/po-mu ...sigh
* ❕✅ Fixed bug with missing 7key BMS not being parsed (Thanks Scrypts)
* ❕✅ Fixed bug with almost all charts from legacy (2007 and older) BME files spawning as pomu9
* ❕✅ Fixed registry issues in Windows 11
* ❕✅ Added 'dependonmusicthread' for those who must have the stepmania lockup experience. set it to false to get better performance, but the music will not block the main thread. 
* ❕✅ Added GetCaloriesBurnedByDate for calorie information on a specific day
* ❕✅ Fixed bug with kbx pump chart length
* ❕✅ Fixed bug with fonts reloading in the wrong order on theme change.

WE NEED SOMEONE TO TEST MIDI / LIGHTS ON THIS BUILD!!

---

## OutFox 5.0.0 Pre-Release Candidate 007 - August 5th 2022

* ❕✅ Fixed bug with modernffmpeg not being chosen correctly on supported systems
* ❕✅ Fixed bug with missing functions on ffmpegmodern driver
* ❕✅ Fixed bug with sound thread crashing
* ❕✅ Fixed bug with discord RPC crashing on game exit
* ❕✅ Set failtype default to 'EndOfSong'
* ❕✅ Added SongDisplayBPMModern
* ❕✅ Fixed bug with missing PIU loader flags
* ❕✅ Fixed bug with 'ForcePIU' hint not being loaded correctly
* ❕✅ Fixed Mac Modules not being compiled correctly
* ❕✅ Fixed bug with incomplete string support on MacOS
* ❕✅ Fixed bug with incorrect redir targets causing a crash
* ❕✅ Fixed bug with invalid scores being generated due to tickhold math logic
* ❕✅ Added Darkfox Icons and branding so it's different in the Taskbar.
* ❕✅ WINDOWS ONLY: Added new install location: Project OutFox V
* ❕✅ Fix be-mu parsing due to squirrel's oopsie

Known Issues:

* ❌❕ Win32 direct input crashing still happens a bit on some race conditions
* ❌❕ Crash on song select options due to non-foot noteskins/noteskins with not all the support

---