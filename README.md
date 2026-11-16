# nekozame-emu-frontend

<p align="center"><img src="nekozame/preview.png" alt="The Mega Drive's page in nekozame-emu-frontend on a Steam Deck: a 90s Japanese game magazine page with the headline 深く、青く。あの夏の海へ, the Mega Drive and a painted bullhead shark on a pink sky, a column of game screenshots, a reef shark photo below, and the system's name running down a pink spine"></p>

The frontend of [nekozame os](https://github.com/purplekairi1312/nekozame-os)'s emulation: browse your whole game library, from a NAS or wherever it lives, in nekozame's magazine theme. Built on [ES-DE](https://es-de.org) 3.5.0.

What's different from ES-DE:

- **nekozame's menu colors**: *nekozame* (violet-gray, orchid and lilac) and *nekozame light* (soft white and pastel pink), from [nekozame-theme](https://github.com/purplekairi1312/nekozame-theme)'s palette, beside ES-DE's own. nekozame is the default
- **Region flags**: each game's regions are read from its file name the way No-Intro and Redump write them, `(Japan)` or `(USA, Europe)`, and themes can show their flags
- Made to be set up by `nekozame-emu`: your file names kept as the game names, nekozame's launcher (with save sync) first for every system, the magazine theme printed from your own library, quiet music while you browse

## Install

On nekozame os:

```sh
nekozame-emu esde on
```

It downloads the newest release, sets everything up, and puts it in Steam and your apps menu. The [emulation guide](https://github.com/purplekairi1312/nekozame-os/blob/main/docs/emulation.md) explains the whole setup.

Anywhere else on Linux: download `nekozame-emu-frontend_x64.AppImage` (or `_x64_SteamDeck.AppImage` on a Steam Deck) from the [releases](https://github.com/purplekairi1312/nekozame-emu-frontend/releases), make it executable and run it. It reads and writes `~/ES-DE`, like ES-DE.

## For theme authors

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

Regions without one flag of their own (World, Asia, Scandinavia, Latin America) show none. Everything else works as in ES-DE: see [THEMES.md](THEMES.md).

## Building

GitHub builds both AppImages with ES-DE's own scripts on every push, and publishes them on a tag. To build one yourself, see [INSTALL.md](INSTALL.md) (`tools/create_AppImage_SteamDeck.sh` or `tools/create_AppImage.sh`).

## Credits

[ES-DE](https://es-de.org) is by Leon Styhre and Northwestern Software, MIT licensed; its own readme is [README-ES-DE.md](README-ES-DE.md), and [USERGUIDE.md](USERGUIDE.md) covers everything it does. The flags are public domain, from Wikimedia Commons ([resources/flags/CREDITS.txt](resources/flags/CREDITS.txt)).

## License

MIT, like ES-DE ([LICENSE](LICENSE)).
