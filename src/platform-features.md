# Platform Features

## Hardware fixups

When designing a hardware platform, the available features are fixed at tapeout.
To allow for fixing issues later on, multiple concepts have evolved:
- chicken bits allow for opting out of features
- microcode adds a translation layer before instruction decoding

## Software configuration

Besides extensions behind buses such as PCI or USB, the built-in controllers are
decided early on. On top of that, the software running on the hardware platform
determines what features are eventually usable via two means, driver enablement
and runtime configuration. For example, the Linux kernel, configured via
Kconfig, offers many drivers and parameters for them. Which of them are used and
how is chosen through ACPI or DeviceTree, possbily both.
