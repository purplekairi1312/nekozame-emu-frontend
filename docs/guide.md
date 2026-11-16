# how nekozame-emu-frontend works

nekozame-emu (nekozame os's emulation tool) sets the frontend up and keeps it updated. this is about how the frontend works. for setting up a library (a nas share, saves, steam) see nekozame os's [emulation guide](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md).

## file names are the game names

whatever a file is named is what shows, in the frontend and in steam. scraping still fills in art, descriptions and dates, but it doesn't touch the names (nekozame-emu turns off "scrape actual game names").

### why

a scraper gives every version of a game the same name. if you keep more than one version of a game (regions, revisions, translations, hacks), you end up with a bunch of entries all called "Sonic the Hedgehog" and no way to tell which one you're starting. the file names already say it:

```
Sonic the Hedgehog (USA, Europe).md
Sonic the Hedgehog (Japan, Korea).md
Sonic the Hedgehog (USA, Europe) (Rev 1).md
Sonic the Hedgehog (Japan) (Translated En).md
```

scraped names also depend on what the database matched, so sometimes it's the wrong game, or the name is in another language. file names are what you chose, and they don't change unless you change them. the region flags come from them too.

### what kind of library it's for

libraries named the way No-Intro and Redump (and TOSEC) name their sets: one folder per system, and file names with the game, its region and its version.

```
roms/
├── megadrive/
│   ├── Sonic the Hedgehog (USA, Europe).md
│   └── Sonic the Hedgehog (Japan, Korea).md
├── megadrivejp/
│   └── Puyo Puyo (Japan).md
└── psx/
    ├── Beat Mania (Japan)/
    │   ├── Beat Mania (Japan).m3u
    │   ├── Beat Mania (Japan) (Disc 1).chd
    │   └── Beat Mania (Japan) (Disc 2).chd
    └── Beatmania (Europe).chd
```

the folder names are ES-DE's system names (`megadrive`, `megadrivejp`, `genesis`, `psx`...)

games with more than one disc: the discs and an `.m3u` playlist listing them, in a folder named after the game. the folder shows as one game

it works best when you keep several versions of games: full sets, games from different regions, translations, hacks

if your files have names like `sonic.bin` or `game1.iso`, it's not for you: use scraped names instead (`"names": "scraped"` in `~/.config/nekozame/emulation.json`, and turn "scrape actual game names" back on in the scraper settings).

### good to know

the name shown is the file name without its extension, brackets and all

the region is the first bracket that names regions, like `(Japan)` or `(USA, Europe)`

hidden files (starting with a dot, like the `._` files macos leaves on network shares) are skipped

renaming a file makes it a new game: its art, favorites and play time stay with the old name, so it's better to rename before scraping or adding games to steam

## region flags

the flags show in the corner of the game's data box: one for `(Japan)`, two for `(USA, Europe)`. it knows the usual No-Intro and Redump region names: Japan, USA, Europe, Korea, Brazil, Australia, Canada, China, Taiwan, Hong Kong, the european countries, Russia, Mexico and India. `(World)`, `(Asia)`, `(Scandinavia)` and `(Latin America)` don't get one.

the flags are public domain, from wikimedia commons. themes can place them with the `flag` and `flag2` image types (see the [readme](../README.md)).

## the order of the systems

by maker, then by year. a console's regional versions stay together, in the order they came out, with the region next to the name:

```
Sega
  SG-1000                 1983
  Master System           1986
  Mega Drive | Japan      1988
  Genesis | North America 1989
  Mega Drive | Europe     1990
  Game Gear               1990
  Mega-CD | Japan         1991
  ...
```

a family stays together under its first release. nekozame-emu writes the order to `~/ES-DE/custom_systems/es_systems_sorting.xml`; ui settings → systems sorting stays on "full names or custom" to use it.

## the nekozame theme

each system is a page like from a 90s japanese game magazine. nekozame-emu prints the pages on your machine, from public-domain NOAA photos and your games' screenshots.

on each page: a text about the console (english, or japanese in ui settings → theme language), its maker, release date and how many games you have, screenshots, and its name on the spine

above the text: a shark or ray painted by Kawahara Keiga (1820s), a photo of the console, or both (`"drawings"` in nekozame-emu's settings)

color schemes (ui settings → color scheme): nekozame, lilac, sakura, ocean, sunset

layouts (ui settings → theme variant): game list, cover grid, review page, filmstrip, contents. each one comes with screenshot, title screen, cover, 3D box, disc or cartridge, or video

menu colors (ui settings → menu color scheme): nekozame and nekozame light

after adding games, `nekozame-emu esde on --again` prints the pages again with the new counts and screenshots.

## playing

each system's first emulator is nekozame's launcher (`nekozame-emu launch`):

saves sync before the game starts and after it ends (nekozame-saves)

disc games (ps1, saturn, pc engine cd, ps2, psp) get read into memory before starting, so reading from a network share doesn't interrupt them

ES-DE's other emulators are still there per game (the game's options → alternative emulator).

## 3D boxes

`nekozame-emu boxes` makes a 3D box from the cover, for each game that doesn't have one. the case follows the system (cardboard, clamshell, jewel case, keep case). scraped boxes stay as they are. they show in the "3D box" layouts.

## ports

the ports system lists the ports, decomps and recomps installed on that machine with `nekozame-ports`. each one has a launcher script in `~/.local/share/nekozame/ports/launchers`.

## music and the screensaver

music: "dolphin sanctuary" by purplekairi1312 plays while you browse and pauses during games and the screensaver (`"music": false` turns it off). © 2026 purplekairi1312, all rights reserved; it comes with nekozame os, not this repo

the screensaver is a slideshow of screenshots. the video one can freeze the frontend on a network share, so it's not used

## where things are

| | |
|---|---|
| `~/ES-DE/settings/es_settings.xml` | the frontend's settings |
| `~/ES-DE/custom_systems/` | nekozame's system list (its launcher first) and the system order |
| `~/ES-DE/themes/nekozame/` | the theme and its pages |
| `~/ES-DE/gamelists/` | game lists: scraped info, favorites, play counts |
| `~/ES-DE/scripts/` | the music's scripts |
| `~/.config/nekozame/emulation.json` | nekozame-emu's settings: where your games are, drawings, music, load to ram |
