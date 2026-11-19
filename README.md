# nekozame-emu-frontend

<p align="center"><img src="https://git.sr.ht/~purplekairi1312/nekozame-emu-frontend/blob/main/nekozame/preview.png" alt="The Mega Drive's page in nekozame-emu-frontend on a Steam Deck, in nekozame's ocean magazine theme"></p>

nekozame's emulation frontend: a fork of [ES-DE](https://es-de.org) with nekozame's theme and new functions. On [nekozame os](https://github.com/purplekairi1312/nekozame-os), `nekozame-emu esde on` installs it.

## What's different

- Your file names are the game names. Scraping doesn't rename them, so the versions of a game (regions, revisions, translations, hacks) don't all end up with the same name.
- Region flags for each game, read from the file name, like `(Japan)` or `(USA, Europe)`: in the game's details and before its name in the list.
- Scraping with ScreenScraper uses each game's own region from its file name, so the Japanese version gets the Japanese box and the European one the European box. Games without a region tag use the region set in the scraper's settings.
- The nekozame theme: each system is a page in the style of an ocean-themed 90s Japanese magazine.
- Systems sorted by maker and year, with each console's regions together.
- Games launch through nekozame-emu, so saves sync between machines.
- 3D boxes made from your covers.
- A Ports system for ports, decomps and recomps.
- Music while browsing: "dolphin sanctuary" by purplekairi1312 ([more below](#the-music)).
- nekozame and nekozame light menu colors, and nekozame's loading screen and icon.
- ES-DE's update check is off, since nekozame-emu keeps it updated.

The theme, system order, launching, boxes, ports and music are set up by `nekozame-emu esde on`. nekozame-emu comes with nekozame os. On any other GNU/Linux, you can download it with git and run it from there ([how](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md#without-nekozame-os)).

How it all works: [docs/guide.md](docs/guide.md).

## Install

With nekozame-emu (on nekozame os, or on any GNU/Linux after downloading it):

```sh
nekozame-emu esde on
```

It downloads the right AppImage, sets everything up and keeps it updated.

Without it, download `nekozame-emu-frontend_x64.AppImage` (or `nekozame-emu-frontend_x64_SteamDeck.AppImage` on a Steam Deck) from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases), make it executable and run it. It keeps its settings in `~/ES-DE`, like ES-DE.

## The theme without nekozame os

The theme lives in [nekozame](nekozame): its graphics, photos, music, and `nekozame-theme`, which prints each system's page on your machine from your own games. It comes inside the AppImage too (`usr/share/es-de/nekozame`).

- To print it: `nekozame/nekozame-theme install`. It needs Python 3 with pygame (`python3-pygame`, or `pip install pygame-ce`), mpv for the music, and the Noto Sans and Noto Sans CJK JP fonts. It finds your games and art from ES-DE's own settings. `nekozame-theme music on` adds the music.
- Ready-made: download `nekozame-theme-pack.zip` from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases) and unzip it into `~/ES-DE/themes`. Every system's pages are already printed, without your games' screens, and the fonts come with it.

Its credits: [nekozame/CREDITS.md](nekozame/CREDITS.md).

## The music

While you browse, you hear "dolphin sanctuary" by [purplekairi1312](https://passedrecordings.bandcamp.com/track/dolphin-sanctuary), an ocean-themed ambient track released by [Passed Recordings](https://passedrecordings.co.uk/) on [Passed Oceans](https://passedrecordings.bandcamp.com/album/passed-oceans).

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

And for a `textlist`, the flags before each game's name:

```xml
<textlist name="gamelist">
    <regionFlags>true</regionFlags>
</textlist>
```

Regions without a flag of their own (World, Asia, Scandinavia, Latin America) show none. Everything else works as in ES-DE's [theme documentation](https://gitlab.com/es-de/emulationstation-de/-/blob/master/THEMES.md).

## Building

GitHub builds both AppImages on every push with `tools/create_AppImage_SteamDeck.sh` and `tools/create_AppImage.sh`, and publishes them when a version is tagged.

## Credits

- Photos of the sea: [NOAA](https://www.noaa.gov/), its [Photo Library](https://www.flickr.com/photos/noaaphotolib/) and [National Marine Sanctuaries](https://sanctuaries.noaa.gov/), and the US National Park Service. Public domain, via [Wikimedia Commons](https://commons.wikimedia.org/).
- The sharks and rays: painted by Kawahara Keiga (川原慶賀) for Philipp Franz von Siebold, 1823-1829. Scans from the [Naturalis Biodiversity Center](https://www.naturalis.nl/), public domain. The paper of the spines is from one of his sheets.
- Photos of the consoles: [Evan-Amos](https://commons.wikimedia.org/wiki/User:Evan-Amos), via Wikimedia Commons. Public domain, apart from a few under CC BY-SA 3.0.
- Patent drawings of the consoles: from US patents, public domain.
- Flags: Wikimedia Commons, public domain.
- Fonts: Noto Sans and Noto Sans CJK JP by Google, SIL Open Font License.
- Music: "dolphin sanctuary" by purplekairi1312, released by [Passed Recordings](https://passedrecordings.co.uk/).
- ES-DE: Leon Styhre, Northwestern Software and everyone in [CREDITS.md](CREDITS.md).

Every image and drawing, one by one, with its source and license: [Credits](docs/credits.md).

## License

- The code: GPL-3.0-or-later ([LICENSE](LICENSE)). ES-DE's code keeps its MIT license and copyright notice ([LICENSE-ES-DE](LICENSE-ES-DE)).
- The libraries, fonts, sounds and ES-DE's own themes keep their licenses, in [licenses](licenses). [CREDITS.md](CREDITS.md) is ES-DE's list of the people who made it.
- nekozame's loading screen and icon: © 2026 purplekairi1312, [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) ([LICENSE-ART](LICENSE-ART)).
- The flags: public domain, from Wikimedia Commons ([resources/flags/CREDITS.txt](resources/flags/CREDITS.txt)).

The theme and the music aren't in this repo. They come with nekozame os:

- The theme: GPL-3.0-or-later. Its photos are public domain (NOAA, Kawahara Keiga's paintings from the Naturalis Biodiversity Center, most of Evan-Amos's console photos); a few console photos are CC BY-SA 3.0. Each one is listed with its source and license in [photos/CREDITS.txt](https://github.com/purplekairi1312/nekozame-os/blob/main/system_files/usr/share/nekozame-os/es-de/photos/CREDITS.txt).
- The music, "dolphin sanctuary": © 2026 purplekairi1312, all rights reserved. It isn't under the GPL. It may only be played as part of nekozame; copying it out, unscrambling it or sharing it isn't allowed without written permission ([its license](https://github.com/purplekairi1312/nekozame-os/blob/main/system_files/usr/share/nekozame-os/es-de/music/LICENSE)).
