# Overview

This repository provides examples of using Rust to program the [Polos Alef]
development board. All of these build on foundational crates provided by the
[Rust Embedded Working Group].

Available examples:

* [*blinky*](./src/blinky.rs)

[Polos Alef]: https://www.analoglamb.com/product/polos-gd32v-alef-board-risc-v-mcu-board/
[Rust Embedded Working Group]: https://github.com/rust-embedded/wg

# Building

These examples can be compiled and flashed from any Windows or Linux system.

Prerequisites:

* Stable Rust w/ `riscv32imac-unknown-none-elf` target
* [Nuclei RISC-V toolchain] (needed only for objcopy)
* [Modified dfu-util] with support for GD32V bootloader
  * As noted in the release notes, Windows users must also use [Zadig] to
    configure WinUSB for the enumerated USB bootloader

To build and flash *blinky*:

```
cargo build --bin blinky --release
riscv-nuclei-elf-objcopy target/riscv32imac-unknown-none-elf/release/blinky -O binary -S blinky.bin
dfu-util -d 28e9:0189 -a 0 --dfuse-address 0x08000000:leave -D blinky.bin
```

[Nuclei RISC-V toolchain]: https://nucleisys.com/download.php
[Modified dfu-util]: https://github.com/riscv-mcu/gd32-dfu-utils

# License

Licensed under either of:

* Apache License, Version 2.0
  ([LICENSE-APACHE](LICENSE-APACHE) or http://www.apache.org/licenses/LICENSE-2.0)
* MIT license
  ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

at your option.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.