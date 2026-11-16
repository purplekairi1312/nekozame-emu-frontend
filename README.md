# nekozame-emu-frontend

<p align="center"><img src="nekozame/preview.png" alt="The Mega Drive's page in nekozame-emu-frontend on a Steam Deck, in nekozame's magazine theme"></p>

nekozame's emulation frontend: a fork of [ES-DE](https://es-de.org) with nekozame's theme and new functions. On [nekozame os](https://github.com/purplekairi1312/nekozame-os), `nekozame-emu esde on` installs it.

## What's different

- Your file names are the game names. Scraping doesn't rename them, so the versions of a game (regions, revisions, translations, hacks) don't all end up with the same name.
- Region flags for each game, read from the file name, like `(Japan)` or `(USA, Europe)`.
- The nekozame theme: each system is a page in the style of a 90s Japanese game magazine.
- Systems sorted by maker and year, with each console's regions together.
- Games launch through nekozame-emu, so saves sync between machines.
- 3D boxes made from your covers.
- A Ports system for ports, decomps and recomps.
- Music while browsing.
- nekozame and nekozame light menu colors, and nekozame's loading screen and icon.
- ES-DE's update check is off, since nekozame-emu keeps it updated.

The theme, system order, launching, boxes, ports and music are set up by `nekozame-emu esde on`. nekozame-emu comes with nekozame os, and also runs on any other Linux from a clone of nekozame-os ([how](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md#without-nekozame-os)).

How it all works: [docs/guide.md](docs/guide.md).

## Install

With nekozame-emu (on nekozame os, or any Linux with a clone of nekozame-os):

```sh
nekozame-emu esde on
```

It downloads the right AppImage, sets everything up and keeps it updated.

Without it, download `nekozame-emu-frontend_x64.AppImage` (or `nekozame-emu-frontend_x64_SteamDeck.AppImage` on a Steam Deck) from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases), make it executable and run it. It keeps its settings in `~/ES-DE`, like ES-DE.

## Region flags in themes

Two extra values for an `image` element's `imageType`:

| `imageType` | Shows |
|---|---|
| `flag` | The flag of the first region in the file name |
| `flag2` | The second one, for games like `(USA, Europe)` |

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

- GPL-3.0-or-later ([LICENSE](LICENSE)).
- ES-DE's code keeps its MIT license and copyright notice ([LICENSE-ES-DE](LICENSE-ES-DE)).
- The libraries' licenses are in [licenses](licenses), and [CREDITS.md](CREDITS.md) is ES-DE's list of the people who made it.
- The flags are public domain, from Wikimedia Commons ([resources/flags/CREDITS.txt](resources/flags/CREDITS.txt)).
