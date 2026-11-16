# How nekozame-emu-frontend works

nekozame-emu, nekozame os's emulation tool, sets the frontend up and keeps it updated. This guide covers how the frontend works. For setting up a library (a NAS share, saves, Steam), see nekozame os's [emulation guide](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md).

## File names are the game names

Whatever a file is named is what shows, in the frontend and in Steam. Scraping still fills in art, descriptions and dates, but it doesn't change the names: nekozame-emu turns off "Scrape actual game names".

### Why

- A scraper gives every version of a game the same name. With several versions of a game (regions, revisions, translations, hacks), you'd get a list of identical "Sonic the Hedgehog" entries and no way to tell which one you're starting.
- The file names already say which version it is:

```
Sonic the Hedgehog (USA, Europe).md
Sonic the Hedgehog (Japan, Korea).md
Sonic the Hedgehog (USA, Europe) (Rev 1).md
Sonic the Hedgehog (Japan) (Translated En).md
```

- Scraped names depend on what the database matched, so they can be the wrong game or in another language. File names only change when you change them.
- The region flags come from the file names too.

### What kind of library it's for

Libraries named the way No-Intro and Redump (and TOSEC) name their sets: one folder per system, and file names with the game, its region and its version.

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

- The folder names are ES-DE's system names (`megadrive`, `megadrivejp`, `genesis`, `psx`...).
- Games with more than one disc: the discs and an `.m3u` playlist listing them, in a folder named after the game. The folder shows as one game.
- It works best when you keep several versions of games: full sets, games from different regions, translations, hacks.

If your files have names like `sonic.bin` or `game1.iso`, use scraped names instead: `"names": "scraped"` in `~/.config/nekozame/emulation.json`, and turn "Scrape actual game names" back on in the scraper settings.

### Good to know

- The name shown is the file name without its extension, brackets included.
- The region is the first bracket that names regions, like `(Japan)` or `(USA, Europe)`.
- Hidden files (starting with a dot, like the `._` files macOS leaves on network shares) are skipped.
- Renaming a file makes it a new game. Its art, favorites and play time stay with the old name, so rename before scraping or adding games to Steam.

## Region flags

- Shown in the corner of the game's data box: one flag for `(Japan)`, two for `(USA, Europe)`.
- Known regions: Japan, USA, Europe, Korea, Brazil, Australia, Canada, China, Taiwan, Hong Kong, the European countries, Russia, Mexico and India.
- `(World)`, `(Asia)`, `(Scandinavia)` and `(Latin America)` don't get a flag.
- The flags are public domain, from Wikimedia Commons. Themes can place them with the `flag` and `flag2` image types (see the [README](../README.md)).

## System order

By maker, then by year. A console's regional versions stay together, in the order they came out, with the region next to the name:

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

- A family stays together under its first release.
- nekozame-emu writes the order to `~/ES-DE/custom_systems/es_systems_sorting.xml`.
- UI Settings → Systems sorting stays on "Full names or custom" to use it.

## The nekozame theme

Each system is a page in the style of an ocean-themed 90s Japanese magazine. nekozame-emu prints the pages on your machine, from public-domain NOAA photos and your games' screenshots.

- Each page: a text about the console (English, or Japanese in UI Settings → Theme language), its maker, release date and number of games, screenshots, and its name on the spine.
- Above the text: a shark or ray painted by Kawahara Keiga (1820s), a photo of the console, or both (`"drawings"` in nekozame-emu's settings).
- Color schemes (UI Settings → Color scheme): nekozame, lilac, sakura, ocean, sunset.
- Layouts (UI Settings → Theme variant): game list, cover grid, review page, filmstrip, contents. Each comes with screenshot, title screen, cover, 3D box, disc or cartridge, or video.
- Menu colors (UI Settings → Menu color scheme): nekozame and nekozame light.

After adding games, `nekozame-emu esde on --again` prints the pages again with the new counts and screenshots.

## Playing

Each system's first emulator is nekozame's launcher (`nekozame-emu launch`):

- Saves sync before the game starts and after it ends (nekozame-saves).
- Disc games (PS1, Saturn, PC Engine CD, PS2, PSP) are read into memory before starting, so reading from a network share doesn't interrupt them.

ES-DE's other emulators are still available per game (the game's options → Alternative emulator).

## 3D boxes

- Each game with a cover gets a 3D box made from it.
- They're made on their own: after `nekozame-emu art`, and within 10 minutes of scraping new covers. `nekozame-emu boxes` makes them right away.
- The case follows the system: cardboard, clamshell, jewel case or keep case.
- Scraped boxes stay as they are.
- They show in the "3D box" layouts.

## Ports

- The Ports system lists the ports, decomps and recomps installed on that machine with `nekozame-ports`.
- Each one has a launcher script in `~/.local/share/nekozame/ports/launchers`.

## Music and the screensaver

- Music: "dolphin sanctuary" by [purplekairi1312](https://passedrecordings.bandcamp.com/track/dolphin-sanctuary), an ocean-themed ambient track released by Passed Recordings, plays while you browse. It pauses during games and the screensaver, and `"music": false` turns it off. Buy it on [Bandcamp](https://passedrecordings.bandcamp.com/track/dolphin-sanctuary) or [Ampwall](https://ampwall.com/a/passedrecordings/album/passed-oceans), or listen on [YouTube](https://www.youtube.com/watch?v=-QDAa7hzcGU&t=7730s). © 2026 purplekairi1312, all rights reserved; it comes with nekozame os, not with this repo.
- The screensaver is a slideshow of screenshots. The video screensaver can freeze the frontend on a network share, so it isn't used.

## Where things are

| | |
|---|---|
| `~/ES-DE/settings/es_settings.xml` | The frontend's settings |
| `~/ES-DE/custom_systems/` | nekozame's system list (its launcher first) and the system order |
| `~/ES-DE/themes/nekozame/` | The theme and its pages |
| `~/ES-DE/gamelists/` | Game lists: scraped info, favorites, play counts |
| `~/ES-DE/scripts/` | The music's scripts |
| `~/.config/nekozame/emulation.json` | nekozame-emu's settings: where your games are, drawings, music, load to RAM |
