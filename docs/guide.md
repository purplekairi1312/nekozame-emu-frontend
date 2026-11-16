# How nekozame-emu-frontend works

nekozame-emu-frontend is set up and kept up to date by `nekozame-emu`, nekozame os's emulation tool. This guide covers how the frontend itself works. For setting up a library (a NAS share, saves, Steam), see nekozame os's [emulation guide](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md).

## Your file names are the games' names

Games are named by their file names. No-Intro and Redump names work best:

```
Sonic the Hedgehog (USA, Europe).md
Sonic the Hedgehog (Japan, Korea).md
Super Mario World (USA) (Rev 1).sfc
Beat Mania (Japan)/Beat Mania (Japan).m3u
```

- **The name shown** is the file name without its extension, brackets included, so versions stay apart.
- **The scraper doesn't rename games.** nekozame-emu turns off "Scrape actual game names"; scraping adds art, descriptions and dates.
- **The region** comes from the first bracket that names regions: `(Japan)`, `(USA, Europe)`, `(Korea)`. It sets the game's flags.
- **Games on several discs** go in an `.m3u` playlist next to their discs, in a folder named after the game. The frontend shows that folder as the game.
- **Hidden files** (starting with a dot, like the `._` files macOS leaves on network shares) are skipped.
- **Renaming a file** makes it a new game: its art, favorites and play time stay with the old name.

## Region flags

The flags are shown in the corner of the game's data box: one for `(Japan)`, two for `(USA, Europe)`. The frontend knows the usual No-Intro and Redump region names: Japan, USA, Europe, Korea, Brazil, Australia, Canada, China, Taiwan, Hong Kong, the European countries, Russia, Mexico and India. `(World)`, `(Asia)`, `(Scandinavia)` and `(Latin America)` show no flag.

The flags are public domain, from Wikimedia Commons. Themes can place them with the `flag` and `flag2` image types (see the [README](../README.md)).

## The systems, in order

Systems are listed by maker, then by year. A console's regional versions stay together, in the order they came out, with the region beside the name:

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

A family stays together under its first release. nekozame-emu writes this order to `~/ES-DE/custom_systems/es_systems_sorting.xml`, and UI Settings → Systems sorting stays on "Full names or custom" to use it.

## The nekozame theme

Each system is a page in the style of a 90s Japanese game magazine. nekozame-emu prints the pages on your machine, from public-domain NOAA photographs and your games' screenshots.

- **On each page**: a text about the console (English, or Japanese: UI Settings → Theme language), its maker, release date and number of games, screenshots, and the console's name on the spine.
- **Above the text**: a painting of a shark or ray by Kawahara Keiga (1820s), a photo of the console, or both (`"drawings"` in nekozame-emu's settings).
- **Color schemes** (UI Settings → Color scheme): nekozame, lilac, sakura, ocean, sunset.
- **Layouts** (UI Settings → Theme variant): game list, cover grid, review page, filmstrip, contents. Each comes in six versions for the picture beside the list: screenshot, title screen, cover, 3D box, disc or cartridge, or video.
- **Menu colors** (UI Settings → Menu color scheme): nekozame and nekozame light, beside ES-DE's own.

After adding games, `nekozame-emu esde on --again` prints the pages again with the new counts and screenshots.

## Playing a game

Each system's first emulator is nekozame's launcher, `nekozame-emu launch`:

- **Saves** are synced before the game starts and after it ends (nekozame-saves).
- **Disc games** (PS1, Saturn, PC Engine CD, PS2, PSP) are read into memory before they start, so reading from a network share doesn't interrupt them.

ES-DE's other emulators stay available per game (the game's options → alternative emulator).

## 3D boxes

`nekozame-emu boxes` makes a 3D box from the cover of each game that has no box. The case type follows the system (cardboard, clamshell, jewel case, keep case). Scraped boxes aren't replaced. They show in the "3D box" layouts.

## Ports

The **Ports** system lists the ports, decomps and recomps installed on this machine with `nekozame-ports`. Each one has a launcher script in `~/.local/share/nekozame/ports/launchers`.

## Music and the screensaver

- **Music**: "dolphin sanctuary" by purplekairi1312 plays while you browse, and pauses during games and the screensaver (`"music": false` turns it off). © 2026 purplekairi1312, all rights reserved; it comes with nekozame os, not this repo.
- **The screensaver** is a slideshow of screenshots. The video screensaver can freeze the frontend on a network share, so it isn't used.

## Where things are

| | |
|---|---|
| `~/ES-DE/settings/es_settings.xml` | The frontend's settings |
| `~/ES-DE/custom_systems/` | nekozame's system list (its launcher first) and system order |
| `~/ES-DE/themes/nekozame/` | The theme and its printed pages |
| `~/ES-DE/gamelists/` | Game lists: scraped details, favorites, play counts |
| `~/ES-DE/scripts/` | The music's event scripts |
| `~/.config/nekozame/emulation.json` | nekozame-emu's settings: where your games are, drawings, music, load to RAM |
