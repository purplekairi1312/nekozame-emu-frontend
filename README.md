# nekozame-emu-frontend

<p align="center"><img src="nekozame/preview.png" alt="The Mega Drive's page in nekozame-emu-frontend on a Steam Deck, in nekozame's magazine theme"></p>

nekozame's emulation frontend: a fork of [ES-DE](https://es-de.org) with nekozame's theme and new functions. It's what `nekozame-emu esde on` installs on [nekozame os](https://github.com/purplekairi1312/nekozame-os).

## What's different from ES-DE

It's built around your file names: the name you give a file is the name shown, the scraper never replaces it, and the region in it (`(Japan)`, `(USA, Europe)`) decides the game's flags.

In the frontend itself:

- Region flags for each game, read from its file name the way No-Intro and Redump write them; themes can show them.
- Two more menu color schemes, nekozame and nekozame light, from [nekozame-theme](https://github.com/purplekairi1312/nekozame-theme)'s palette. nekozame is the default.
- nekozame's loading screen and icon.
- ES-DE's own update check is off; nekozame-emu updates it from this repo's releases.

Set up by nekozame-emu on nekozame os:

- The nekozame theme: every system a page from a 90s Japanese game magazine, printed from your own library, in five color schemes and five layouts.
- Systems ordered by maker and year, a console's regional versions together (Mega Drive | Japan, Genesis | North America, Mega Drive | Europe).
- Games launched through nekozame-emu: saves synced before and after, disc games read into memory first.
- 3D boxes made from your covers, a Ports system for ports, decomps and recomps, and music while you browse.

[docs/guide.md](docs/guide.md) explains how all of it works.

## Install

On nekozame os:

```sh
nekozame-emu esde on
```

On other Linux systems, download `nekozame-emu-frontend_x64.AppImage` (or `nekozame-emu-frontend_x64_SteamDeck.AppImage` on a Steam Deck) from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases), make it executable and run it. It uses `~/ES-DE` for its settings, like ES-DE.

## Region flags in themes

Two extra values for an `image` element's `imageType`:

| `imageType` | Shows |
|---|---|
| `flag` | The flag of the first region in the game's file name |
| `flag2` | The flag of the second, for games like `(USA, Europe)` |

```xml
<image name="flag">
    <pos>0.9 0.8</pos>
    <origin>1 1</origin>
    <maxSize>0.04 0.034</maxSize>
    <imageType>flag</imageType>
</image>
```

Regions without a flag of their own (World, Asia, Scandinavia, Latin America) show none. Everything else works as in ES-DE's [theme documentation](https://gitlab.com/es-de/emulationstation-de/-/blob/master/THEMES.md).

## Building

GitHub builds both AppImages on every push with `tools/create_AppImage_SteamDeck.sh` and `tools/create_AppImage.sh`, and publishes them when a version is tagged.

## License

GPL-3.0-or-later ([LICENSE](LICENSE)). ES-DE's code keeps its MIT license and copyright notice ([LICENSE-ES-DE](LICENSE-ES-DE)); the libraries' licenses are in [licenses](licenses), and [CREDITS.md](CREDITS.md) is ES-DE's list of the people behind it. The flags are public domain, from Wikimedia Commons ([resources/flags/CREDITS.txt](resources/flags/CREDITS.txt)).
