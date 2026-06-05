# Voltball ZMK Config

This repository initializes a split ZMK keyboard named `voltball` for `nice_nano_v2`.

Current assumptions:

- Split layout with 48 keys total
- Matrix from [matrix.png](./matrix.png)
- Logical matrix is `4x12`
- Each half scans `4x6`
- Left half is central, right half is peripheral
- Battery is `AA` and uses `zmk-feature-non-lipo-battery-management`

Files of interest:

- `build.yaml`: build targets for `voltball_left` and `voltball_right`
- `boards/shields/voltball`: shield definition
- `config/voltball.keymap`: default 3-layer keymap

Pin mapping from `pinout.png`:

- Rows: `row0=P0.08`, `row1=P0.02`, `row2=P1.15`, `row3=P1.13`
- Cols on both halves: `col0=P0.24`, `col1=P1.00`, `col2=P1.11`, `col3=P1.04`, `col4=P1.06`, `col5=P0.10`
- Battery ADC: `P0.31/AIN7`

Battery notes:

- Default ZMK `vbatt` is disabled in favor of `zmk,non-lipo-battery`
- `config/west.yml` includes `zmk-feature-non-lipo-battery-management`

Typical build examples:

```sh
west init -l config
west update
west zephyr-export
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=voltball_left
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD=voltball_right
```
