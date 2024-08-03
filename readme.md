# makeftrom and FamiTracker Conversion Tutorial

The problem: music composition for romhacks is a cryptic, laborious, error-prone, and generally painful process.

With few exceptions, each NES game company uses at least one of their own proprietary music formats for their games, each with their own capabilities and binary format. Both the playback code and composition software are proprietary and not publicly available, and few formats even have composition tools available written by romhackers. As such, the development of romhacks usually requires painstaking manual conversion to the game's music format by hand with a hex editor, if someone's even reverse-engineered and documented the format to begin with.

The FamiTracker conversion project seeks to solve this problem once and for all by allowing direct use of FamiTracker music in hacks. Not only is FT the de facto industry standard NES chiptune music format and composition software based on the tracker paradigm that has been popular in electronic music since the 80s, it is also generally much more powerful than proprietary game music formats.

There are two parts to this:
1. The **conversion** is a patch for the game ROM that adds the ability to play FT tracks in the game in question. As these conversions are extensively tied to the game's own code and architecture, the exact features they offer vary by game.
2. **makeftrom** is the standard tool for importing music into a romhack that is based on a conversion for that game. While the exact features it provides are limited by the specific conversion, the use of makeftrom is nearly identical across conversions, and once you know how to use it for one game, you basically know how to use it for other games. This is possible because makeftrom relies on `ftcfg` files provided by the conversion to tell it what capabilities the conversion has and how to import the music into the ROM.

## The Tutorial

Now that we've gone over what makeftrom and FamiTracker conversions even are, let's get to the tutorial itself.

[Part 1: Prerequisites](./prerequisites.md)

[Part 2: Basic Use](./basic-use.md)

[Part 3: More Advanced Features](./features.md)

[Part 4: Music Selection and Issues](./music-selection.md)

[Part 5: Other Games](./other-games.md)

## Linking and Translations

While this tutorial is open source, I would very much prefer if references to it linked to it rather than making copies of it. This ensures that there aren't multiple different versions and everyone always sees the latest version.

That said, I strongly encourage translations into other languages. If you have the skills, feel free to help by translating it to other languages so the greatest number of people can benefit from it. At a minimum, I would like to get Japanese and Chinese translations, as that's where the majority of non-English romhackers are, but others are also welcome.
