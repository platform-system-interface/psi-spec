# From Hardware to Software

A piece of hardware on its own is nothing without code. Typical SoCs run their
first code from a [mask ROM](mask-roms-loaders.md), which in turn loads
additional code from other kinds of memory, [initializing the platform](
platform-initialization.md) to offer a [boot environment](boot-environments.md).

## Hardware fixups

When designing a hardware platform, the available features are fixed at tapeout.
To allow for fixing issues later on, multiple concepts have evolved:

- chicken bits allow for opting out of features
- microcode adds a translation layer before instruction decoding

These can be instrumented by any component of the boot chain.

## Software configuration

While buses such as PCI and USB allow for flexible extension, built-in
controllers themselves are defined at the time of [hardware platform design](
hw-sw-codesign.md). On top of that, the software running on the platform
determines what features are eventually usable via two means, driver enablement
and runtime configuration.

For example, the Linux kernel, configured via Kconfig, offers many drivers and
parameters for them. Which of them are used and how is chosen through parameters
via ACPI or DeviceTree, possbily both, or hardcoded. Any component in a boot
chain could take care of (re)initializing any feature of the platform.
