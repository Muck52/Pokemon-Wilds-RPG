# Pokemon Wilds RPG — build notes

`pokemon-wilds.gba` is a build of this branch, ready to play in mGBA.

## Build environment (Ubuntu 24.04, Claude Code cloud session)

Install dependencies (from `docs/install/linux/UBUNTU.md`):

    sudo apt install build-essential binutils-arm-none-eabi gcc-arm-none-eabi libnewlib-arm-none-eabi git libpng-dev python3

Build:

    make -j$(nproc)

- Toolchain: arm-none-eabi-gcc 13.2.1
- Clean build time: ~2.5 min on 4 cores
- Output: `pokeemerald.gba` (32 MB), copied here as `pokemon-wilds.gba`
- No game source changes were needed.

## Tests (`make check`)

5886 total: 5439 passed, 0 unexpected failures
(19 known-failing, 419 to-do, 9 expected-fail — all upstream-labelled).

## Updating the ROM

After changing game files, rebuild and refresh the committed copy:

    make -j$(nproc)
    cp pokeemerald.gba release/pokemon-wilds.gba
    git add -f release/pokemon-wilds.gba
