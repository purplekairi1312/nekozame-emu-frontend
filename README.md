# nekozame-emu-frontend

<p align="center"><img src="nekozame/preview.png" alt="the mega drive's page in nekozame-emu-frontend on a steam deck, in nekozame's magazine theme"></p>

nekozame's emulation frontend, a fork of [ES-DE](https://es-de.org) with nekozame's theme and some new stuff. on [nekozame os](https://github.com/purplekairi1312/nekozame-os), `nekozame-emu esde on` installs it.

## what's different

it's built around your file names. whatever you name a file is what shows, and scraping won't rename it. the region in the name (`(Japan)`, `(USA, Europe)`) is where the game's flags come from.

the frontend itself adds region flags per game (from the file name), nekozame and nekozame light menu colors (nekozame by default), and nekozame's loading screen and icon. ES-DE's update check is off.

on nekozame os, nekozame-emu also sets up the nekozame theme, the systems ordered by maker and year with each console's regions together, launching through nekozame-emu so saves sync, 3D boxes made from your covers, a ports system, and music.

how it all works: [docs/guide.md](docs/guide.md)

## install

on nekozame os:

```sh
nekozame-emu esde on
```

on other linux: grab `nekozame-emu-frontend_x64.AppImage` (or the `_SteamDeck` one on a deck) from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases), make it executable and run it. it keeps its stuff in `~/ES-DE`, same as ES-DE.

## region flags in themes

two extra values for an `image` element's `imageType`:

| `imageType` | shows |
|---|---|
| `flag` | the flag of the first region in the file name |
| `flag2` | the second one, for games like `(USA, Europe)` |

```xml
<image name="flag">
    <pos>0.9 0.8</pos>
    <origin>1 1</origin>
    <maxSize>0.04 0.034</maxSize>
    <imageType>flag</imageType>
</image>
```

regions without their own flag (World, Asia, Scandinavia, Latin America) show none. the rest works like ES-DE's [theme docs](https://gitlab.com/es-de/emulationstation-de/-/blob/master/THEMES.md).

## building

github builds both appimages on every push (`tools/create_AppImage_SteamDeck.sh` and `tools/create_AppImage.sh`) and publishes them when a version gets tagged.

## license

GPL-3.0-or-later ([LICENSE](LICENSE)). ES-DE's code keeps its MIT license ([LICENSE-ES-DE](LICENSE-ES-DE)), the libraries' licenses are in [licenses](licenses), and [CREDITS.md](CREDITS.md) is ES-DE's list of the people who made it. the flags are public domain, from wikimedia commons ([resources/flags/CREDITS.txt](resources/flags/CREDITS.txt)).
