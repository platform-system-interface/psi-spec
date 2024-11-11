## Boot Environments

A _boot environment_ is the hosting system of a _boot loader_.

Boot processes may be interactive, or automatic, or static, set up in many ways.

The following table classifies various approaches with example implementations.

|             | serial       | network         | graphics               |
| ----------- | ------------ | --------------- | ---------------------- |
| Automatic   | xmodem       | TFTP, HTTP, PXE | splash screen          |
| Interactive | shell, ReGIS | `cpu`, web      | framebuffer, text menu |

A boot environment may be configurable. Configuration may be changed at runtime,
out of band, or at build time depending on the use case.

The following is a list of examples.

- [U-Boot configuration](https://docs.u-boot.org/en/latest/develop/distro.html)
- [UEFI NVRAM](https://uefi.org/specs/UEFI/2.10/03_Boot_Manager.html)
- [SeaBIOS (e.g., coreboot NVRAM)](https://www.seabios.org/Runtime_config)
- [Boot Loader Specification](https://uapi-group.org/specifications/specs/configuration_files_specification/)
- [GRUB configuration](https://www.gnu.org/software/grub/manual/grub/html_node/Configuration.html)
- [syslinux/extlinux configuration files](https://wiki.syslinux.org/wiki/index.php?title=SYSLINUX)
- [PXE scripting/menu](https://ipxe.org/)
