Temper Settings
===============

Controlling my [temper](https://github.com/raeedcho/temper), a split wireless-only
mechanical keyboard with [nice!view](https://nicekeyboards.com/docs/nice-view/) displays.

 * [timer-less home row mods](https://github.com/urob/zmk-config#timeless-homerow-mods)
 * sticky shift on right thumb, double-tap (or shift+tap) activates caps-word
 * shift+space morphs into dot+space+sticky-shift


## Building

Either generate the firmware via the GitHub action, or build locally by setting
up the ZMK toolchain as described [here](https://zmk.dev/docs/development/setup).
Given a directory structure like:

```
...
|-- config-temper/
|-- zephyr-sdk-0.16.4/
`-- zmk/
    |-- app
    `-- ...
```

Then from the `zmk/app` directory run the following command to build the
firmware for the left hand board:

```sh
west build -b nice_nano_v2 -p -c -- -DSHIELD="temper_left nice_view_adapter nice_view" -DZMK_CONFIG=../../config-temper-zmk/config -DZMK_EXTRA_MODULES=../../config-temper-zmk -DZephyr-sdk_DIR=../../zephyr-sdk-0.16.4/cmake
```

This will produce the file `zmk/app/build/zephyr/zmk.utf`. Put the board into
bootloader mode by pressing the reset button twice, and copy this file to the
board, which will show up as a USB drive when connected to your computer. Repeat
for the right side board.


## Miscellaneous

In MacOS, when a key is held down while entering text, a popup is shown which
lets you choose between various accented forms of the character. The following
command will disable this behaviour.

```
defaults write -g ApplePressAndHoldEnabled -bool false
```

## Resources

 * https://github.com/urob/zmk-config
 * https://github.com/caksoylar/keymap-drawer

