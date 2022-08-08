# ps2x2pico
USB keyboard/mouse to PS/2 interface converter using a Raspberry Pi Pico

![Hardware](https://raw.githubusercontent.com/No0ne/ps2x2pico/main/hw1.jpg)

WIP - until I know enought about Rust use this instead: https://github.com/No0ne/ps2pico

# Usage
* Copy `ps2x2pico.uf2` to your Pi Pico by pressing BOOTSEL before pluggging in.
* 3.3V/5V conversion is done using a bi-directional level shifter: https://learn.sparkfun.com/tutorials/bi-directional-logic-level-converter-hookup-guide/
* Afterwards connect a USB keyboard and/or mouse using an OTG-adapter and optional USB hub.
```
                   _________________
                  |                 |
Pico GPIO11 ______| LV1         HV1 |______ PS/2 keyboard clock
Pico GPIO12 ______| LV2         HV2 |______ PS/2 keyboard data
Pico GPIO13 ______| LV          HV  |______ PS/2 5V + Pico VBUS
Pico    GND ______| GND         GND |______ PS/2 GND
Pico GPIO14 ______| LV3         HV3 |______ PS/2 mouse clock
Pico GPIO15 ______| LV4         HV4 |______ PS/2 mouse data
                  |_________________|
```

# Build
```
rustup target install thumbv6m-none-eabi
cargo install flip-link
cargo install elf2uf2-rs --locked
cargo build --release
elf2uf2-rs target/thumbv6m-none-eabi/release/ps2x2pico ps2x2pico.uf2
```

# Resources
* https://github.com/No0ne/ps2pico
