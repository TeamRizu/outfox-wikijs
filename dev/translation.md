---
title: Translation
description: Guide on translating themes for Project OutFox.
published: true
date: 2024-09-17T22:55:59.708Z
tags: 
editor: markdown
dateCreated: 2023-05-16T06:19:22.684Z
---

Are you translating a theme to another language? Reading this might help you.

## Where are language files stored

Inside every theme, there'll be a `Languages` folder. Inside that folder is where language files are stored. Example:

```
Languages/
    en.ini
    ja.ini
```

Here we can see 2 language files: **en** for English and **ja** for Japanese. It's a standard to name language files in that format (language-COUNTRY.ini). For example: In this case, there's a Portuguese translation, but since there's also Portuguese from Portugal, the file was named **pt-BR** (BR = Brazil).

### Fallback

You probably already noticed a `_fallback` theme in the themes folder, but in case you didn't: it's where things that are necessary for every theme gets stored, so when someone is making a theme the game doesn't blow up. The same goes for Languages: it's important to also translate the fallback for your language because the theme you're translating might not have every string that it uses on its folder.

## Starting a translation

To start your work, create a new file for your language(-COUNTRY, if needed), and don't forget to use the .ini extension. You can do this on Notepad with no problem but it's recommended to use an editor like Visual Studio Code or Notepad++.

Now open en.ini and your new language file, then copy all the content from en.ini to your language file. You can close en.ini now.

### Language file name standard

The language code used for your language file should follow [ISO-1 Language codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes), while the COUNTRY CODE should follow [ISO 3166-1 Alpha-2 code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements).

> ⚠️ StepMania Engine doesn't have proper support for more than 2 letters language files: Both StepMania and OutFox, as the date of writing this document, do not follow ISO-1 and ISO 3166-1 standards, however, new languages should not abide by non-standards of StepMania Engine quirks. Your language will still be able to be selected and used, however, instead of showing the Language name, it will show the language code and users won't have the game auto-select the language for them. This will later be fixed at least for OutFox, [following this issue](https://github.com/TeamRizu/OutFox/issues/311).
{.is-danger}


### What you should translate

_This is a code example taken from the Soundwaves theme._

```ini
[Common]
WindowTitle=Project OutFox
StepMania=Project OutFox
# Dedicated Character Display strings
ModelLoadError=Model for %s (%s) Has a invalid model. Please check if the model.txt file is correctly named and formatted.
ModelAnimLoadError=An animation file for %s's model (%s) is invalid or non-existent. Please check the animation folders and see if there's any file missing.
LocationLoadError=Current Location (%s) is missing its location model. Please check if the model.txt file is correctly named and formatted.
SongLoaderSingleSong=Random Song Play: Current Folder only contains 1 song. OutFox might get confused when picking the song via random. Selecting to index 1.
SongLoaderNoSongs=Random Song Play: No songs were found in your OutFox install folder! Switching back to fallback music.
```

**Do not translate WindowTitle or StepMania keys. Do not translate the name "Project OutFox".**

You can see on this image and your file that every line has a Title=Value, and that's how translation works on OutFox, you need to translate the value of the titles and you're done. The theme does all the work of what string it should use.

Now, you can't just translate everything that you see. On ``ModelLoadError`` for example, there's a "%s" that means the theme or the game will put a string replacing that %s.

An example of that can be seen on the string ``%d Song Played`` that you'll see on the next image. 

```ini
[Screen]
HelpText=&BACK; Exit &START; Select &SELECT; Options &MENULEFT;&MENURIGHT;&MENUUP;&MENUDOWN; Move

[ScreenWithMenuElements]
HelpText=&BACK; Exit &START; Select &MENULEFT;&MENURIGHT; Move
StageCounter=%s Stage
EventStageCounter=Song %i
```

You'll also see lines like ``&START;``, ``&SELECT;`` etc. They're buttons that will be replaced once the game draws that string. Let's see one of those strings in action?

```ini
[ScreenSelectProfile]
SingularSongPlayed=%d Song Played
SeveralSongsPlayed=%d Songs Played
PressStart=Press &START; to join.
```

![profilesongsplayed.jpeg](/resources/translation/profilesongsplayed.jpeg){.align-center}

Here we can see that &START; gets replaced by a green square that represents the start button, and %d gets replaced by a number that's how many songs that profile played.

Another special string is ``\n``. It creates a line break. For example, ``First Line\nSecondLine`` would result in:

_First Line_

_Second Line_

Here's an example in action from `_fallback/en.ini`:

![cauntionwarning.png](/resources/translation/cauntionwarning.png){.align-center}

### Text Context

You might also want to translate the theme in a way that someone who has never played before will understand, instead of expecting everyone to already know what everything is. A new player might not understand what "holds" means if that word is translated to your language, but if it was kept as "holds" the user would know that it's the literal name of the thing and not something that should make sense in your language.

Another hard example is steps: in OutFox, there are 2 kinds of steps. The ones that you press in gameplay and the steps of the chart made by the author (easy steps, hard steps...). In English, it's easy to only say steps because it makes sense for both, but that isn't the case with every language. That's why it was decided to keep it named "steps" for the pt-BR translation of Soundwaves, for example.

### Community Translations for Soundwaves (OutFox default until Alpha V)

Many folks are already helping translate the new Soundwaves theme for various languages. As requested by one of our translators, we'll mention those projects below to give them some visibility and encourage more people to join and help.

° [Polish](https://github.com/Tiny-Foxes/OutFox-PL) - Done by [Moneko](https://github.com/JustMoneko)

° [Japanese](https://github.com/Tiny-Foxes/OutFox-ja) - Done by [はぬべき(hanubeki)](https://github.com/hanubeki)

° [Portuguese-Brazilian](https://github.com/Tiny-Foxes/OutfoxPTBR) - Done by [zerinho6](https://github.com/moruzerinho6), [SHRMP0](https://github.com/SHRMP0) and [SheepyChris](https://github.com/SheepyChris)

° [German](https://github.com/Tiny-Foxes/OutFox-DE) - Done by [DanielRotwind](https://github.com/DanielRotwind)

° [Hebrew](https://github.com/Tiny-Foxes/OutFox-he) - Done by [Snil4](https://github.com/snil4)

° [French](https://github.com/Tiny-Foxes/Outfox-fr) - Done by [Ksempac](https://github.com/Ksempac) and [Kaede573](https://github.com/Kaede573)

° [Español](https://github.com/Tiny-Foxes/OutFox-es) - Done by [JoseVarelaP](https://github.com/JoseVarelaP)

° [Hungarian](https://github.com/Tiny-Foxes/OutFox-hu) - Done by [KaZo75](https://github.com/Tiny-Foxes/OutFox-hu)

° [Italian](https://github.com/Tiny-Foxes/OutFox-IT) - Done by [Gabrimax](https://github.com/Gabrimax98)

° [Simplified Chinese](https://github.com/Tiny-Foxes/OutFox-zh-CN) - Done by [jerrymyx](https://github.com/jerrymxy)

° [Slovak](https://github.com/Tiny-Foxes/OutFox-sk) - Done by [jose1711](https://github.com/jose1711)

---

## Tools and Practices

Translating can be tedious. Sometimes it's hard to locate & remove lines that shouldn't be there or find missing ones. Because of that, translators themselves create tools to make our job easier and faster.

## Tools and Practices {.tabset}
### Translation Toolkit
[Translation Toolkit](https://github.com/Tiny-Foxes/Translation-Toolkit) is a tool made by [Ksempac](https://github.com/Ksempac) to help remove lines that are not needed anymore, warn about lines that are missing, check your progress, etc. It supports Linux, Mac, and Windows.

> _This project is intended as a small application to automate some tasks for translators._
>
>_It is able to parse, analyze and fix the OutFox translation files._

![translationtoolkit.png](/resources/translation/translationtoolkit.png){.align-center}
### Stepmania-TranslatorViewMaker
[Stepmania-TranslatorViewMaker](https://github.com/Tiny-Foxes/Stepmania-TranslatorViewMaker) is a tool made by [Snil4](https://github.com/snil4). It supports any OS that has Python 3 installed.

> _Have you ever tried to translate a program like OutFox and wondered "Hmm, now where can I find that line in the .ini?" Now there's no need to wonder! This program will make a translator view file for your translation .ini and make your translation job easier._

![translatorview.jpg](/resources/translation/translatorview.jpg){.align-center}
### fini
[fini](https://github.com/Tiny-Foxes/fini) is a tool made by [moruzerinho6](https://github.com/moruzerinho6)

> Adds a extra build process where you can additional features that are not available on default ini file. Use:
>
> - "Fini-" lines that allow you to specify another file to load it and expert a section/line/value from it. You can separate whole screens to specific files and only merger then together when building. You can make many lines depend on a specific file line, meaning you'll later only need to change that file and effect many others.
> - RTL variable to reverse the text only after you build the files.
> - Any valid ini file is supported, meaning you don't have to remake all your previous work

## End Tabset {.tabset}

### Best practices

#### Be constant with your words

When doing a mention of "Steps", ask yourself: is it clear which "type of Steps" you're referring to? We have the following "types of steps":

* Steps, which means the notes inside of the chart or the note count.
* StepDifficulty, which means the difficulty selected of the chart, such as Novice, Expert, Hard.
* Step, which means the action of stepping in the pad or a single note.
* StepType, which means the quantization (timing/color) of the note (e.g. 4th = red, an entire beat; 8th = blue, half a beat; etc).

**[Soundwaves](https://github.com/Tiny-Foxes/smtheme-soundwaves-community)** does not have this issue as it says "Taps" instead of Steps and directly says the difficulty.

![soundwavesmusicwheel.png](/resources/translation/soundwavesmusicwheel.png){.align-center}

#### Reload translations

![cauntionwarning.png](/resources/translation/cauntionwarning.png){.align-center}

Imagine you're editing the Soundwaves ScreenCaution and want to see how the translated string looks. You don't need to restart the entire game to see the changes, here's what you should do instead: Exit the screen you just translated, reload the metrics (`Shift + Insert`; or `Shift + F2` on older alpha versions) and enter the screen again.

Some themes might have a problem where not all strings are updated when metrics are reloaded due to how they are made. In that case, unfortunately, the only option is to restart the game.

---

## OutFox Releases

Now that you have translated the latest alpha, you need to send it to OutFox somehow. This tutorial explains how you can do it!

The first thing to keep in mind is that each OutFox translation is hosted inside [Tiny-Foxes](https://github.com/Tiny-Foxes) to easily maintain and keep track of updates, so contact Team Rizu through any of their available social media profiles to get invited into Tiny-Foxes.

It is also required to know how [git](https://git-scm.com/) and [Github](https://github.com/) work.

The exact steps are:

1. Create a [Github](https://github.com/) account
2. Download and learn basic [git](https://git-scm.com/) commands such as (git status, git push, git pull, git commit and git checkout)
3. Learn how GitHub organization works.

Having an editor such as [Visual Studio Code](https://code.visualstudio.com/) will make git interactions way easier as those commands are available by the interface.
### Repository

OutFox translation repositories adhere to a standard style. The repository title should be: 

"OutFox-[languageFileName[-COUNTRY]]"

_"-COUNTRY" should only be added in special cases (example: there's Portuguese from Portugal and Brazilian Portuguese, so the Portuguese-Brazilian language file is "pt-BR.ini")._

The description of the repository should be: 

"[Language Name] ([languageFileName]) Translation for Project OutFox""

Here's an example:

```
OutFox-ja

Japanese (ja) Translation for Project OutFox
```

#### Repository Format

The repository should have 2 folders: "_fallback" and "default". Inside the _fallback will be the _fallback translation and default translation inside the default folder.

Only the translation file is required to be inside the folders/repository.

#### Keep track

It's recommended that you include the version that the translation is targeting inside the files. Here's an example:

```ini
# Version: 4.9.7 Alpha

[Common]
WindowTitle=Project OutFox
StepMania=OutFox
```

### Submitting to OutFox

So you finished the translation for this alpha before the release? You can then **commit directly to master OR make a Pull Request** with your files to [OutFox-Translations](https://github.com/Tiny-Foxes/OutFox-Translations) so [Jose_Varela](https://github.com/JoseVarelaP) includes them in the next alpha release.

**This all assumes that you're already a member of Tiny-Foxes and the translator team.**

## Webmasters Project

Webmasters is an internal OutFox initiative to translate [OutFox Website](https://projectoutfox.com/). Being a webmaster means: 

- Partial access to the website backend to implement your translation files;
- Closer contact with the OutFox Community team for quick updates and help;
- Having a special role in our Discord Server.

The requirements to join Webmasters are having previous experience as a long-term OutFox translator, being a [Discord Server](https://discord.gg/cN4TjgQdcA) member, and receiving a special invitation from the OutFox Team.

_Written and Maintained by Moru Zerinho6_
