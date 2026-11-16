# nekozame-emu-frontend

<p align="center"><img src="nekozame/preview.png" alt="The Mega Drive's page in nekozame-emu-frontend on a Steam Deck, in nekozame's ocean magazine theme"></p>

nekozame's emulation frontend: a fork of [ES-DE](https://es-de.org) with nekozame's theme and new functions. On [nekozame os](https://github.com/purplekairi1312/nekozame-os), `nekozame-emu esde on` installs it.

## What's different

- Your file names are the game names. Scraping doesn't rename them, so the versions of a game (regions, revisions, translations, hacks) don't all end up with the same name.
- Region flags for each game, read from the file name, like `(Japan)` or `(USA, Europe)`.
- The nekozame theme: each system is a page in the style of an ocean-themed 90s Japanese magazine.
- Systems sorted by maker and year, with each console's regions together.
- Games launch through nekozame-emu, so saves sync between machines.
- 3D boxes made from your covers.
- A Ports system for ports, decomps and recomps.
- Music while browsing: "dolphin sanctuary" by purplekairi1312 ([more below](#the-music)).
- nekozame and nekozame light menu colors, and nekozame's loading screen and icon.
- ES-DE's update check is off, since nekozame-emu keeps it updated.

The theme, system order, launching, boxes, ports and music are set up by `nekozame-emu esde on`. nekozame-emu comes with nekozame os. On any other Linux, you can download it with git and run it from there ([how](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md#without-nekozame-os)).

How it all works: [docs/guide.md](docs/guide.md).

## Install

With nekozame-emu (on nekozame os, or on any Linux after downloading it):

```sh
nekozame-emu esde on
```

It downloads the right AppImage, sets everything up and keeps it updated.

Without it, download `nekozame-emu-frontend_x64.AppImage` (or `nekozame-emu-frontend_x64_SteamDeck.AppImage` on a Steam Deck) from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases), make it executable and run it. It keeps its settings in `~/ES-DE`, like ES-DE.

## The music

While you browse, you hear "dolphin sanctuary" by [purplekairi1312](https://passedrecordings.bandcamp.com/track/dolphin-sanctuary), an ocean-themed ambient track released by Passed Recordings on [Passed Oceans](https://ampwall.com/a/passedrecordings/album/passed-oceans).

> inspired by the watery sounds of videogames such as Ecco the Dolphin: Defender of the Future, Treasures of the Deep, or Diver's Dream, and using only KORG gear, the KORG Wavestate, and KORG Prophecy for the synth lead solo, i wanted to bring back the specific feelings of wonder i had as a child playing those beautiful underwater themed games, but reinterpreted through my own personal style.

- Buy it on [Bandcamp](https://passedrecordings.bandcamp.com/track/dolphin-sanctuary) or [Ampwall](https://ampwall.com/a/passedrecordings/album/passed-oceans), or listen on [YouTube](https://www.youtube.com/watch?v=-QDAa7hzcGU&t=7730s).
- It pauses during games and the screensaver. `"music": false` in nekozame-emu's settings turns it off.
- © 2026 purplekairi1312, all rights reserved. It comes with nekozame os, not with this repo, and isn't under its license.

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
