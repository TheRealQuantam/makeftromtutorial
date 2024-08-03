# Basic Use

Now that we've got everything set up, we can get to actually using it. makeftrom was designed to be easy to use and has many shortcuts to minimize the amount that must be done by the user, but it is not something that can be easily learned purely by trial and error without any explanation.

## Create the Project File

The workflow of makeftrom is probably not something the average Windows user today is familiar with, though it would probably be comfortable for the average Unix user (or those old enough to have been proficient with DOS). 

The makeftrom "interface" consists of the user creating a project file in a text editor. This project file specifies the input ROM, music to import, etc. While makeftrom is a command line utility, this design allows it to be run in Explorer by simply dragging and dropping the project file onto `makeftrom.exe` and it will then use the settings in the project file to do what is desired. Additionally, the use of project files makes the process easily reproducible, so the ROM can be trivially recreated should changes to the input ROM or music be made.

Project files use the JSON5 format, an extension of the JSON format used behind the scenes of most web pages but not familiar to the average person. It is an ugly format to be sure, but it allows for complex file structures to be written with far less typing than more familiar formats like XML.

### 1. The Header

First of all, create the file `tutorial\tutorial.json5` and open it in a text editor. The filename doesn't actually matter, but in the tutorial it will be referred to by this name or simply as "the project file".

Start by putting the following into it:
```json5
{
}
```

In JSON5, braces enclose an "object" (a better name would be "dictionary"): a set of unordered key/value pairs of the form `"key": value,` or `key: value,` (the latter requires that the key be 1 word plus some other constraints). The rest of the file will go inside these braces.

Next, add the line
```json5
    ftcfg: "mm2ft/mm2ft.ftcfg",
```

It doesn't look like much, but this is where the magic happens. This tells makeftrom where to get all the information it needs to import the music. ftcfg files are supplied with the conversion and should be treated as version-specific as the contents may change with different versions of the conversion. The `mm2ft.ftcfg` and `rm2ft.ftcfg` files are *not* interchangeable and are used with Mega Man 2 US and Rockman 2 Japan, respectively, though for some games the same ftcfg may be used for both versions.

Next, add
```json5
    input_rom: "mm2ft/mm2ft.nes",
    output_rom: "tutorial.nes",
```

You can probably figure out that these specify the input ROM (the one we made in prerequisites by applying `mm2ft.bps` to the Mega Man 2 ROM) and output ROM (what makeftrom will generate with the imported music).

**IMPORTANT**: makeftrom output ROMs *cannot* be used as the input to makeftrom. *Always* retain your input ROM, as that is what you will have to use for further hacking or if you change your mind about what music should go in it.

This is the minimum required header. These things can all be specified on the command line, but when run through Explorer `ftcfg`, `input_rom`, and `output_rom` must be present in all project files.

Finally, add
```json5
    track_dir: "tracks",
```

This is optional, but allows for less typing when specifying track paths. Note that the path specified here, if not absolute (not e.g. `C:\...`), is relative to *the directory the project file is in*. In our case, the project file is `tutorial\tutorial.json5`, so `tracks` refers to `tutorial\tracks`. Track paths specified later will then be relative to that directory rather than `tutorial`.

So far, the file should look like this:
```json5
{
    ftcfg: "mm2ft/mm2ft.ftcfg",
    input_rom: "mm2ft/mm2ft.nes",
    output_rom: "tutorial.nes",
    track_dir: "tracks",
}
```

For those wondering, JSON5 allows trailing commas, so it's convenient to put a comma after each item in a list or dictionary.

### 2. The ft_files Section

Now we're getting to the interesting stuff.

Add the lines:
```json5
    ft_files: [
    ],
```

The `ft_files` section specifies the FT format files to be imported. Note that `[...]` brackets are used because this is a list, not a dictionary. A list consists of ordered items (not key/value pairs), though in this case the order of files doesn't matter.

Add our first item to the list:
```json5
        {AirMan2: "airman.ftm"},
```

Yes, that is a dictionary inside a list inside a dictionary. This tells makeftrom to import the track `tutorial\tracks\airman.ftm` and name it `AirMan2`. This name will be used later in the project file to specify where this track will be used in-game.

The reason we don't call it `AirMan` is because there already is a track named AirMan: the original Air Man music. Existing game tracks are given names by the ftcfg file, and the list of possible names for the conversion should be given in the conversion's readme. Now, it *is* possible to assign one of your tracks to a pre-existing name; this is not an error, but means that it will no longer be possible to refer to the original game track later in the project file. It is, however, an error to give 2 of your tracks the same name.

### 3. The c2_files Section

While all conversions support the use of native format music in addition to FT music, makeftrom can only import native format tracks for formats that have self-contained tracks; formats like Capcom 2, which is used by Mega Man 1 and 2.

Add the following to the project file (outside the existing `ft_files` section):
```json5
    c2_files: [
        // Mega Man: The New Lands - Boss (King Kong 2 and/or Wai Wai World - Boss)
        {KingKong2WaiWaiWorldBoss: [0x8000, "KingKong2WaiWaiWorldBoss.bin"]},
    ],
```

This is the Capcom 2 abbreviated form, which differs a bit because it requires a value that wasn't required for FT files. Here, `tutorial\tracks\KingKong2WaiWaiWorldBoss.bin` contains the track data in either binary or hexadecimal format, and `0x8000` is the track starting address. Track data contains raw addresses for different things embedded in it that makeftrom must change when it places the track at a different location in your ROM. Thus makeftrom needs to know the address the track was ripped from in the *original* ROM (the origin of the track in quest), so it can figure out how much to adjust the addresses by when it places the track in *your* ROM.

You can also see that JSON5 supports comments, which are *not* used by makeftrom and are for your eyes only.

### 4. The track_map Section

Now that we have the tracks added, it's time to define how the tracks will be used. This is accomplished through the `track_map` section of the project file.

Add the following to the project file:
```json5
    track_map: {
        Intro: "Ending",
        FlashMan: "AirMan2",
    },
```

This specifies
1. Use the track named `Ending` for the intro. In this case, both of these are predefined track names, so `Ending` refers to the original ending music.
2. Use the track named `AirMan2` for Flash Man's stage.

Once again, this list of track names can be found in the conversion readme.

### 5. The boss_track_map Section

Some conversions provide value-added features that are not present in the original game. If we had assigned a track to `Boss` in `track_map` that would have been used as the default boss track. However, one of the value-added features of the Mega Man series of conversions is that they support unique music for every boss fight. 

Let's show this off by adding the following to the project file:
```json5
    boss_track_map: {
        FlashMan: "KingKong2WaiWaiWorldBoss",
    },
```

And with that, the Flash Man boss - but no others - will have custom music.

As with track names, see the conversion's readme for the list of boss names.

### 6. ...Profit!

And with that, we're done with the project file! If any issues are encountered, you can look at [the full project file](./tutorial.json5).

Save your project file, then go to the `tutorial` directory in Explorer and drag and drop the `tutorial.json5` file onto `makeftrom.exe`. After several seconds, you should see...
```

Press enter to continue...
```

...not a heck of a lot. makeftrom follows the Unix philosophy of "no news is good news". Thus, the fact that no error was displayed means everything worked fine. Press enter to close the window.

Now you have `tutorial.nes`. Open it up in your favorite emulator/flash cart and you should get something like this:

[![Result Video](https://img.youtube.com/vi/N5dGr8Rry9U/0.jpg)](https://www.youtube.com/watch?v=N5dGr8Rry9U)

Next up is discussion of the less basic features in [Part 3](./features.md)