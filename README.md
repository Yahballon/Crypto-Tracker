# Crypto Tracker

**Native PS5 Homebrew · v0.3.0 · by YAHBALLON**

Crypto Tracker is a native, controller-driven cryptocurrency market dashboard for PlayStation 5 homebrew, built with [ps5-homebrew-ui](https://github.com/blackbearreloaded/ps5-homebrew-ui).

The project now has its **own independent repository**, build workflow, version history and GitHub Releases.

## Features

- Dark-blue 1920×1080 dashboard with live USD cryptocurrency quotes and 7-day sparklines.
- Scrollable **Pinned** area supporting as many favourites as the configured market list allows.
- Persistent pin/unpin preferences stored in a local settings file.
- Individual coin logos from the CC0 [cryptocurrency-icons](https://github.com/spothq/cryptocurrency-icons) collection, bundled at build time. Unsupported symbols get a distinct ticker badge.
- Detailed price, change, market-cap, volume, supply, ATH/ATL and historical charts for each coin.
- HTTPS market data from CoinGecko; TLS certificate checks, rate-limit errors, and background fetches.
- Original header branding: **CRYPTO TRACKER by YAHBALLON**, with the version on the far right.

## Controller

| Button | Action |
| --- | --- |
| D-Pad | Navigate coins and chart ranges |
| L1 / R1 | Scroll quickly through coin cards |
| Cross | Open coin details |
| Circle | Back / Exit |
| Square | Pin or unpin a coin |
| Triangle | Refresh market quotes |

## Build and Releases

This repository contains the original native application code in [`native/`](native/) and a dedicated [GitHub Actions workflow](.github/workflows/build-ps5-crypto-tracker.yml).

The workflow:

1. Retrieves the [PS5-DevBridge](https://github.com/Yahballon/PS5-DevBridge) native scaffold and required toolchain.
2. Copies the native source files into the build scaffold, generates the app icon, and bundles the offline coin-logo atlas.
3. Compiles the native PS5 FSELF and packages all required assets and libraries.
4. Verifies the executable, metadata and complete `PPSA99442.zip` archive.
5. Uploads the ZIP as a GitHub Actions artifact.
6. On a successful push to `main`, publishes a GitHub Release with an English changelog and the PS5 ZIP if that version tag does not already exist.

**Versions are independent of the former multi-project repository.** For future releases, update the app version, metadata version, tag, artifact label and English release notes together before merging the release. The workflow deliberately does not overwrite already-published tags.

## Installation

1. Download `PPSA99442.zip` from [Releases](../../releases).
2. Extract it. The ZIP contains the folder `PPSA99442/` with `eboot.bin`, `sce_module/libc.prx`, `sce_sys` and required assets.
3. Copy `PPSA99442/` to `/data/homebrew/` on your PS5.
4. Register the application using a compatible homebrew loader / ShadowMountPlus.

**Title ID:** `PPSA99442` · **Content version:** `01.000.005`.

## Notes and limitations

- Network access requires valid DNS/TLS and may be rate-limited by CoinGecko (HTTP 429).
- Successful GitHub Actions compilation does **not** constitute a runtime test on physical PS5 hardware.
- Favourites are stored separately from the application code and should survive routine app updates if their data path is preserved.
- No wallet keys, trading functionality, or financial transactions are included.

## License and attribution

The native application is GPL-3.0-or-later, and its UI scaffold derives from [ps5-homebrew-ui](https://github.com/blackbearreloaded/ps5-homebrew-ui). The bundled cryptocurrency icon artwork is from [spothq/cryptocurrency-icons](https://github.com/spothq/cryptocurrency-icons) under CC0 1.0. Retain upstream notices and dependencies' license conditions.
