## Mask ROMs and Loaders

Many SoCs have initial pieces of code baked into them to bootstrap the system.
Some may call them boot ROMs, otherwise known as mask ROMs or Zero Stage Boot
Loaders (ZSBL). They define a low-level access channel for development and would
typically remain mostly the same over time for the same vendor, because change
would mean cost.
This initial code is designed to load the changeable application code from
rewritable storages, such as SPI flash parts, SD cards, or eMMC, or possibly an
internal reprogrammable memory part. Those stages are also referred to as
[platform initialization](platform-initialization.md).

Mask ROM loaders may fall back to a mechanism allowing for talking to the SoC
directly, e.g. via USB or UART. Because each vendor has their own implementation
of such a mechanism, they also have their own software utilities that understand
the respective protocol. With that software, one may read out chip information,
perform MMIO access, transfer data into memory and execute it, set fuses, etc.

### Generic protocols, variants and tools

- [USB Device Firmware Upgrade (DFU)](https://www.usb.org/document-library/device-firmware-upgrade-11-new-version-31-aug-2004)
  - [STM32](https://www.st.com/resource/en/application_note/an3156-usb-dfu-protocol-used-in-the-stm32-bootloader-stmicroelectronics.pdf)
  - [usbd-dfu (written in Rust)](https://github.com/vitalyvb/usbd-dfu)
- [fastboot](https://android.googlesource.com/platform/system/core/+/master/fastboot/README.md)
  - [flashing instructions for Android development](https://source.android.com/docs/setup/test/running)
  - [U-Boot documentation on fastboot](https://docs.u-boot.org/en/latest/android/fastboot-protocol.html)
  - [fastboot host-side implementation in Rust](https://github.com/platform-system-interface/fastboot)

### Vendor specific protocols and tools

- Allwinner: FEL mode, usable with
  - [`sunxi-fel`](https://github.com/linux-sunxi/sunxi-tools)
  - [`xfel`](https://github.com/xboot/xfel)
  - [`fel-cli`](https://github.com/Razican/fel-cli)
  - other tools exist
- Amlogic: (name unknown?), changed at least once over time (?)
  - [`pyamlboot`](https://github.com/superna9999/pyamlboot)
  - [`aml_boot`](https://github.com/platform-system-interface/aml_boot)
  - other tools exist
- Bouffalo Lab
  - [`bl_boot`](https://github.com/platform-system-interface/bl_boot)
- Canaan Kendryte
  - [`kendryte_boot`](https://github.com/platform-system-interface/kendryte_boot)
- Rockchip: **TODO**
  - [`rkflashtool`](https://github.com/linux-rockchip/rkflashtool)
  - [`xrock`](https://github.com/xboot/xrock)
- Sophgo
  - [`sg_boot`](https://github.com/platform-system-interface/sg_boot)
- StarFive JingHong (JH)
  - [`jh_boot`](https://github.com/platform-system-interface/jh_boot)
