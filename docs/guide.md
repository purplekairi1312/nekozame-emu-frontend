# How nekozame-emu-frontend works

nekozame-emu-frontend is set up and kept up to date by `nekozame-emu`, nekozame os's emulation tool. This guide covers how the frontend itself works. For setting up a library (a NAS share, saves, Steam), see nekozame os's [emulation guide](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md).

## Your file names are the games' names

Everything works from your file names, so name your files the way you want them shown. No-Intro and Redump names work best:

```
Sonic the Hedgehog (USA, Europe).md
Sonic the Hedgehog (Japan, Korea).md
Super Mario World (USA) (Rev 1).sfc
Beat Mania (Japan)/Beat Mania (Japan).m3u
```

- **The name shown** is the file name without its extension, brackets included. Versions stay apart: a scraper would call both of the Sonic files above "Sonic the Hedgehog".
- **The scraper never renames games.** nekozame-emu turns off "Scrape actual game names", so scraping fills in art, descriptions and dates and leaves the names alone.
- **The region** comes from the first bracket that names regions: `(Japan)`, `(USA, Europe)`, `(Korea)`... It gives the game its flags (below), and it's what tells the versions apart in Steam too.
- **Games on several discs** go in an `.m3u` playlist next to their discs, in a folder named after the game. The frontend shows that folder as the game.
- **Hidden files** (starting with a dot, like the `._` files macOS leaves on network shares) are skipped.
- **Renaming a file** makes it a new game: its art, favorites and play time stay with the old name. Rename before you scrape or add games to Steam.

## Region flags

Each game's flags are shown in the corner of its data box: one flag for `(Japan)`, two for `(USA, Europe)`. The frontend knows the usual No-Intro and Redump region names: Japan, USA, Europe, Korea, Brazil, Australia, Canada, China, Taiwan, Hong Kong, the European countries, Russia, Mexico and India. `(World)`, `(Asia)`, `(Scandinavia)` and `(Latin America)` show no flag.

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

A family stays together under its first release, even when another console came out between its regions. nekozame-emu writes this order to `~/ES-DE/custom_systems/es_systems_sorting.xml`, and UI Settings → Systems sorting stays on "Full names or custom" to use it.

## The nekozame theme

Every system is a page from a 90s Japanese game magazine. nekozame-emu prints the pages on your machine, from public-domain NOAA photographs and your own games' screenshots, so each library gets its own.

- **On each page**: the headline 深く、青く。あの夏の海へ, a museum-style text about the console (in English, or Japanese: UI Settings → Theme language), its data (maker, release date, number of games), screenshots from your games, and the console's name moving down the spine.
- **Above the text**: one of Kawahara Keiga's 1820s paintings of sharks and rays, a museum photo of the console itself (the right region's model), or both. Set with `"drawings"` in nekozame-emu's settings.
- **Color schemes** (UI Settings → Color scheme): nekozame, lilac, sakura, ocean, sunset.
- **Layouts** (UI Settings → Theme variant): game list, cover grid, review page, filmstrip, contents. Each comes in six versions for the picture beside the list: screenshot, title screen, cover, 3D box, disc or cartridge, or video.
- **Menu colors** (UI Settings → Menu color scheme): nekozame and nekozame light, beside ES-DE's own.

After adding games, `nekozame-emu esde on --again` prints the pages again with the new counts and screenshots.

## Playing a game

Every system's first emulator is nekozame's launcher, `nekozame-emu launch`:

- **Saves** are synced before the game starts and after it ends (nekozame-saves), so the newest save is there on every machine.
- **Disc games** (PS1, Saturn, PC Engine CD, PS2, PSP) are read into memory before they start, so a game on a network share never stalls on a disc read.

ES-DE's other emulators stay available per game (the game's options → alternative emulator).

## 3D boxes

`nekozame-emu boxes` makes a 3D box for every game that has a cover but no box: the cover on the front, a spine in the colors of the cover's edge, in perspective. The case follows the system (cardboard, a clamshell, a jewel case, a keep case in the console's plastic color), and the shape follows the cover. Boxes from the scraper are never replaced. They show in the layouts' "3D box" versions.

## Ports

The **Ports** system lists the ports, decomps and recomps installed on this machine with `nekozame-ports` (Ship of Harkinian, the Zelda 64 recomps, GZDoom...). Each one is a small launcher script in `~/.local/share/nekozame/ports/launchers`. The ports themselves are installed per machine, so each machine shows its own.

## Music and the screensaver

- **Music**: "dolphin sanctuary" by purplekairi1312 plays quietly while you browse, and pauses during games and the screensaver (`"music": false` turns it off). The track is © 2026 purplekairi1312, all rights reserved; it's part of nekozame os, not of this repo.
- **The screensaver** is a slideshow of your games' screenshots. The video screensaver searches game after game for a video, and over a network share that freezes the frontend.

## Where things are

| | |
|---|---|
| `~/ES-DE/settings/es_settings.xml` | The frontend's settings |
| `~/ES-DE/custom_systems/` | nekozame's system list (its launcher first) and system order |
| `~/ES-DE/themes/nekozame/` | The theme and its printed pages |
| `~/ES-DE/gamelists/` | Game lists: scraped details, favorites, play counts |
| `~/ES-DE/scripts/` | The music's event scripts |
| `~/.config/nekozame/emulation.json` | nekozame-emu's settings: where your games are, drawings, music, load to RAM |
