# ZMK config for Pepito v1.13

The Pepito is a wireless split keyboard made by [ClicketySplit](https://clicketysplit.ca/).

> Pepito is a 44 key wireless keyboard with a form factor of 3x6x4M, and based on the Seeed Studio XIAO BLE. It has inherent support for nice!view displays, which leverage memory-in-pixel display panels by Sharp. Pepito's firmware is based on ZMK v3.5 and currently stable in test.

![pepito-picture](https://cdn.shopify.com/s/files/1/0599/3460/5491/files/Pepito-Orange.jpg)

## Specs

- nice!view displays
- USB-C ports
- Seeed Studio XIAO BLE (Bluetooth)
- LiPo 700mAh batteries
- MBK Legend 40s grey on white key
- Kailh Pro Red low profile switches

## Firmware

Built with upstream [ZMK](https://zmk.dev) plus Clickety Split's hardware module
[zmk-clickety-split](https://github.com/ClicketySplit/zmk-clickety-split), both
pinned to commit SHAs in `config/west.yml`. Push to any branch and GitHub Actions
builds `pepito-firmware` (left, right and settings-reset `.uf2` files).

The keymap targets the macOS **Canadian - CSA** input source on an ANSI keyboard
type; `config/keys_fr_canadian_standard.h` maps characters to the HID keys that
layout expects.

### Updating ZMK

1. Check the ZMK revision Clickety Split validates in
   [zmk-config-pepito](https://github.com/ClicketySplit/zmk-config-pepito/blob/main/config/west.yml)
   and the latest [zmk-clickety-split](https://github.com/ClicketySplit/zmk-clickety-split/commits/main) commit.
2. Update the `zmk` revision in `config/west.yml` **and** the
   `build-user-config.yml@<sha>` ref in `.github/workflows/build.yml` to the same SHA.
3. Update the `zmk-clickety-split` revision in `config/west.yml`.
4. Push on a branch, let CI build, flash and test before merging.
