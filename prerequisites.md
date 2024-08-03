# Prerequisites

There are 6 things you will need before we can continue with the tutorial.

1. The game
1. The conversion
1. The patcher
1. makeftrom
1. FamiTracker
1. The music files

First of all, create a directory called `tutorial`. It doesn't actually matter what you call it, but this tutorial will refer to it as `tutorial`.

## 1. The Game

For this tutorial, we will be using Mega Man 2, specifically one of the following versions (any of the listed file versions will do):

Mega Man 2 (USA):
- PRG-ROM CRC32 0FCFC04D / MD5 0527A0EE512F69E08B8DB6DC97964632
- File CRC32 5E268761 / MD5 8E4BC5B03FFBD4EF91400E92E50DD294
- File CRC32 80E08660 / MD5 302761A666AC89C21F185052D02127D3
- File CRC32 A9BD44BC / MD5 CAAEB9EE3B52839DE261FD16F93103E6

## 2. The Conversion

[mm2ft](https://archive.org/details/mm2ft) is the Mega Man 2 FamiTracker conversion.

Download it and unzip the files into a new directory `tutorial\mm2ft` for future use. Note the `readme.txt` file, which will be a valuable reference in the future. Note also the 4 `.bps` files that will be used to patch the game ROM. Those beginning with `mm2` are for Mega Man 2 US, those with `rm2` are for Rockman 2 Japan; the ones with `demo` in them are the mm2ft patch plus music files that form a playable demo of mm2ft that is the base game with a new soundtrack.

## 3. The Patcher

The mm2ft patches are in BPS format and require a patcher capable of applying that format. Any such patcher will do, but if you don't already have one and know how to use it, the following is one way of doing it.

1. Download [Beat](https://archive.org/details/beat_v1) and run beat.exe
1. Select `Apply Patch`
1. For its `Step 1` select `tutorial\mm2ft\mm2ft.bps` as the patch to apply
1. For its `Step 2` select your Mega Man 2 ROM as the original file
1. For its `Step 3` select `tutorial\mm2ft\mm2ft.nes` as the modified file.
1. Click `Apply` to perform the patch.

## 4. makeftrom

Download [makeftrom](https://archive.org/details/makeftrom) and extract all the files into `tutorial`.

## 5. Dn-FamiTracker

Dn-FamiTracker is the de facto current version of FamiTracker after the original version and several derivatives went dormant. It has numerous tracker improvements and a command-line export interface that makeftrom uses to convert FTM/0CC/DNM modules to the much smaller and optimized binary form directly used by the FT conversions.

Download [Dn-FamiTracker](https://github.com/Dn-Programming-Core-Management/Dn-FamiTracker) (go to [Releases](https://github.com/Dn-Programming-Core-Management/Dn-FamiTracker/releases)) and extract it into a new directory `tutorial\Dn-FamiTracker`.

## 6. The Music

Finally, download all the files in [tracks](./tracks) and place them in the directory `tutorial\tracks`. While a majority of FamiTracker tracks that don't use expansion chips will work, not *all* features of FamiTracker are supported by the conversions, so some tracks may not play back correctly.

## ...is in Another Castle

Now that we've gotten everything necessary, on to actually using it in [part 2](./part2.md).