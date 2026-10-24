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

### Notes on newer ZMK than the Clickety pin

As of 2026-10, ZMK `main` is ~33 commits ahead of the pinned `83bc82d`. Notable
fixes there, not yet validated by Clickety Split on Pepito hardware:

- fix(split): use managed queue for input report to avoid deadlock (#3110),
  relevant to split keyboards like Pepito.
- fix(behaviors): correct HID usage validation range check (#3503).
- fix(studio): saving issue with >190 keys (#3431, does not affect Pepito).

If the halves freeze or drop keys, moving `zmk` to a newer `main` SHA (both in
`config/west.yml` and the workflow ref) is the first thing to try.

## ZMK Studio

CI also builds `pepito-left-studio.uf2`: the left half with
[ZMK Studio](https://zmk.dev/docs/features/studio) over USB. Flash it instead of
`pepito-left.uf2` (right half unchanged), connect the left half over USB and open
<https://zmk.studio>. Unlock with a `STUDIO` key on the BLE layer (hold the
rightmost right thumb, then press the D or K key).

- Studio shows US key labels; the actual output still follows Canadian - CSA
  (e.g. the key labelled `/` types `é`).
- Changes made in Studio are stored on the keyboard and override this repo's
  keymap until you use "Restore Stock Settings" in Studio or flash settings-reset.
