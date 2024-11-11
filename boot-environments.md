## Boot Environments

A _boot environment_ is the hosting system of a _boot loader_.

Boot processes may be interactive, automated, static, and set up in many ways.

The following table classifies various approaches with example implementations.

|             | serial       | network         | graphics             |
| ----------- | ------------ | --------------- | -------------------- |
| Automated   | xmodem       | TFTP, HTTP, PXE | splash screen        |
| Interactive | shell, ReGIS | `cpu`, web      | framebuffer, textual |

A boot environment may be configurable. Configuration may be changed at runtime,
out of band, or at build time depending on the use case.

- U-Boot config partition, env file
- UEFI NVRAM
- coreboot NVRAM
- SeaBIOS (?)
- GRUB config (runtime?)
- PXE?
