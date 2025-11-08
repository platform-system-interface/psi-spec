# Mask ROMs and Loaders

Many SoCs have initial pieces of code baked into them to bootstrap the system.
Some may call them boot ROMs, an ambiguous term, so they are otherwise known as
[mask ROMs](https://patents.google.com/patent/US20050254280A1/en)s or Zero Stage
Boot Loaders (ZSBL). They would typically remain mostly the same over time for
the same vendor, because change would mean cost.

## Boot modes and sources

This initial code is designed to load the changeable application code from
rewritable storages, such as SPI flash parts, SD cards, or eMMC, or possibly an
internal reprogrammable memory part. Those stages are also referred to as
[platform initialization](platform-initialization.md).

Some platforms offer boot mode selection via GPIO pins and/or fuses to lock down
a system once used in production. A development board may have a pin header with
jumpers or a set of DIP switches or similar, or possibly a test point used in
final steps when manufacturing.

## Protocols, variants and tools

Mask ROM loaders may define a low-level access channel for development and fall
back to a mechanism allowing for talking to the SoC directly, e.g. via USB or
UART. Because each vendor has their own implementation of such a mechanism, they
also have their own software utilities that understand the respective protocol.
With that software, one may read out chip information, perform MMIO access,
transfer data into memory and execute it, set fuses, etc.

### Generic

- [USB Device Firmware Upgrade (DFU)](https://www.usb.org/document-library/device-firmware-upgrade-11-new-version-31-aug-2004)
  - [STM32](https://www.st.com/resource/en/application_note/an3156-usb-dfu-protocol-used-in-the-stm32-bootloader-stmicroelectronics.pdf)
  - [usbd-dfu (written in Rust)](https://github.com/vitalyvb/usbd-dfu)
- [fastboot](https://android.googlesource.com/platform/system/core/+/master/fastboot/README.md)
  - [flashing instructions for Android development](https://source.android.com/docs/setup/test/running)
  - [U-Boot documentation on fastboot](https://docs.u-boot.org/en/latest/android/fastboot-protocol.html)
  - [fastboot host-side implementation in Rust](https://github.com/platform-system-interface/fastboot)

### Vendor specific

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
- Qualcomm
  - [`qc_boot`](https://github.com/platform-system-interface/qc_boot)
- Rockchip: **TODO**
  - [`rkflashtool`](https://github.com/linux-rockchip/rkflashtool)
  - [`xrock`](https://github.com/xboot/xrock)
- Sophgo
  - [`sg_boot`](https://github.com/platform-system-interface/sg_boot)
- StarFive JingHong (JH)
  - [`jh_boot`](https://github.com/platform-system-interface/jh_boot)

## Image formats

Besides copying data from the boot source, a mask ROM also needs to understand a
_binary format_. There are multiple binary formats used by later stage loaders
that are more widely known, such as PE32 in UEFI PI, or (S)ELF and FIT in other
projects. Most vendors have defined their own formats for the mask ROM loader,
integrating with their specific tooling and bootstrapping mechanisms.

For example, Qualcomm defines a format named MBN[^1], which holds metadata in
addition to the segments and entry point as commonly seen in formats like ELF.
The additional metadata contains OEM specific information, certificate chains,
and signatures. The design of such a format may reflect how the respective chip
vendor's business relationships work, i.e., how customers may or may not extend
the basic platform.

[^1]: <https://www.qualcomm.com/content/dam/qcomm-martech/dm-assets/documents/secure-boot-and-image-authentication-version_final.pdf>
