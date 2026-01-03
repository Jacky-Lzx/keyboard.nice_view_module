# Keyboard.nice_view_module

Forked from <https://github.com/GPeye/nice-view-mod>

This zmk module provides a custom nice_view shield for displaying my personal figures on the nice_nano_v2 keyboard (as
peripherals)

> [!NOTE]
> I use a dongle as the central device to show information of the keyboard status. Please see my
> [config repository](https://github.com/Jacky-Lzx/keyboard.zmk-config) for more details.

|                    Hollow Knight                     |                    Silk Song                     |
| :--------------------------------------------------: | :----------------------------------------------: |
| ![Hollow Knight](assets/imgs/26-01-03_21-55-36.avif) | ![Silk Song](assets/imgs/26-01-03_21-54-31.avif) |

## Usage

### Add the Module to Your West Manifest

To use this module, first add it to your config/west.yml by adding a new entry to remotes and projects

```yml
manifest:
  remotes:
    # zmk official
    - name: zmkfirmware
      url-base: https://github.com/zmkfirmware
    # New entry
    - name: jackylzx
      url-base: https://github.com/Jacky-Lzx

  projects:
    - name: zmk
      remote: zmkfirmware
      revision: v0.3.0
      import: app/west.yml
    # New entry
    - name: keyboard.nice_view_module # nice-view-module
      remote: jackylzx
      revision: main
  self:
    path: config
```

### Configure the Left/Right Peripheral

In your left/right keyboard peripheral configuration files, add `CONFIG_NICE_VIEW_LEFT=y`/`CONFIG_NICE_VIEW_RIGHT=y`
respectively to enable this module and show different figures

- Left keyboard: Hollow Knight
- Right keyboard: Silk Song

If the config is not set, the default nice_view images (ballon or mountain) will be randomly displayed

### Build with the Custom Shield

Now simply swap out the default nice_view shield on the board for the custom one in your build.yaml file

```yml
---
include:
  - board: nice_nano_v2
    shield: eyelash_sofle_central_dongle dongle_display
    artifact-name: eyelash_sofle_central_dongle_oled
  - board: nice_nano_v2
    shield: eyelash_sofle_peripheral_left nice_view_adapter nice_view_custom # Change this line
  - board: nice_nano_v2
    shield: eyelash_sofle_peripheral_right nice_view_adapter nice_view_custom # Change this line
  - board: nice_nano_v2
    shield: settings_reset
```

## Customization

If you want to customize the displayed images, you should better folk the [original repository](https://github.com/GPeye/nice-view-mod)
and go through the tutorial in [this repository](https://github.com/GPeye/urchin-peripheral-animation)
