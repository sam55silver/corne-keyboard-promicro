# Corne Keyboard (Pro Micro)

ZMK firmware config for a Corne keyboard built with nice!nano v2 controllers and nice!view displays.

## Hardware

- **Board:** nice_nano_v2
- **Shields:** corne_left, corne_right, nice_view_adapter, nice!view
- **Wireless:** Bluetooth (ZMK)

## Keymap

The keymap is in [`config/corne.keymap`](config/corne.keymap) with four layers:

| Layer | Trigger | Purpose |
|---|---|---|
| Default | — | QWERTY + Ctrl/Esc mod-tap |
| Lower (LWR) | Left middle thumb | Numbers, arrows, nav keys, screenshot |
| Raise (RSE) | Right middle thumb | Programmer symbols |
| Adjust (ADJ) | Hold LWR + tap `\` | Bluetooth management, bootloader |

## Building

Firmware is built automatically by GitHub Actions on push. Download the artifact from the Actions tab and flash the `.uf2` files to each half via the nice!nano bootloader (double-tap reset, drag `.uf2` to the `NICENANO` drive).

## ZMK Studio

ZMK Studio is **not enabled** in the current build. It was removed because it saves keymap overrides to persistent flash that survive reflashing, which can cause `.keymap` file changes to appear not to apply.

To re-enable ZMK Studio, add the following to `build.yaml`:

```yaml
include:
  - board: nice_nano_v2
    shield: corne_left nice_view_adapter nice_view
    snippet: studio-rpc-usb-uart
    cmake-args: -DCONFIG_ZMK_STUDIO=y
  - board: nice_nano_v2
    shield: corne_right nice_view_adapter nice_view
```

If you do re-enable it and your `.keymap` changes aren't taking effect, use "Restore Stock Settings" in the [ZMK Studio](https://zmk.studio) web app to clear the stored overrides.
