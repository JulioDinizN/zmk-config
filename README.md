# ZMK Config

This repository contains my ZMK user configuration for a Corne split keyboard
using nice!nano v2 controllers.

## Layout

![Corne layout](keymap-drawer/corne.svg)

## Firmware

This repo builds two firmware files through GitHub Actions:

- `corne_left` for the left half
- `corne_right` for the right half

The build currently includes the `nice_oled` shield for the OLED status screen.

### Build New Firmware

1. Change the config files, usually `config/corne.keymap` or
   `config/corne.conf`.
2. Commit and push the change to `main`.
3. GitHub Actions builds the firmware automatically.
4. When the build succeeds, GitHub Actions creates a new release automatically.
5. Open the latest release and download the `.uf2` firmware files.

Each release should contain one `.uf2` file for `corne_left` and one `.uf2`
file for `corne_right`.

Releases are versioned automatically with the Sao Paulo date and the GitHub
Actions run number, for example `v2026.06.02-42`.

The firmware build only runs automatically when firmware-relevant files change,
such as `build.yaml`, files under `config/`, or the firmware workflow itself.

Do not use the keymap-drawer artifact for flashing. That workflow only updates
the layout image in this README.

If you need the temporary Actions artifact instead of the release, open the
latest `Build ZMK firmware` run and download the artifact named `firmware`.

### Flash The Keyboard

Flash each half with the matching `.uf2` file:

1. Plug the left half into USB.
2. Double-tap the reset button quickly to enter bootloader mode.
3. Wait for the removable drive to mount. It is usually named `NICENANO`.
4. Copy the `.uf2` file containing `corne_left` to that drive.
5. Wait for the drive to eject and reboot automatically.
6. Repeat the same steps on the right half with the `.uf2` file containing
   `corne_right`.

For keymap-only changes, flashing the central half can be enough, but flashing
both halves keeps the split firmware and OLED configuration aligned.

### Notes

- The GitHub Actions Node.js deprecation warnings are not firmware failures if
  the run status is `Success`.
- If a half does not enter bootloader mode, unplug it, reconnect it, and
  double-tap reset again.
