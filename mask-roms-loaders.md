## Mask ROMs and Loaders

Many SoCs have initial pieces of code baked into them to bootstrap the system.
Some may call them boot ROMs, otherwise known as mask ROMs or Zero Stage Boot
Loaders (ZSBL). They define a low-level access channel for development and would
typically remain mostly the same over time for the same vendor, because change
would mean cost.
This initial code is designed to load the changeable application code from
rewritable storages, such as SPI flash parts, SD cards, or eMMC, or possibly an
internal reprogrammable memory part.

Those loaders may fall back to a mechanism allowing for talking to the SoC
directly, e.g. via USB or UART. Because each vendor has their own implementation
of such a mechanism, they also have their own software utilities that understand
the respective protocol. With that software, one may read out chip information,
perform MMIO access, transfer data into memory and execute it, set fuses, etc.

### Examples

- Allwinner: FEL mode, usable with
  - `sunxi-fel`
  - `xfel`
  - `fel-cli`
  - other tools exist
- Amlogic: (name unknown?), changed at least once over time (?)
  - `pyamlboot`
  - `aml_boot`
  - other tools exist
- Rockchip: **TODO**
  - `rkflashtool`

### Boot Loaders

Since memory and storage parts can be complex, additional firmware and loaders
are implemented in software. They would initialize the platform step by step,
phase by phase, or stage by stage; projects differ in naming.

- U-Boot: TPL -> SPL -> maybe extra code -> U-Boot proper -> OS
- EDK2: SEC -> PEI -> DXE -> BDS -> payload/OS
- Oxide: phbl -> OS
- coreboot: Cache-as-RAM / ROM stage -> RAM stage -> [payload -> OS]
- Allwinner: boot0 -> possibly intermediate -> U-Boot proper
- RISC-V: [ZSBL ->] FSBL -> SBI -> OS
- oreboot: bt0 -> main -> [payload -> OS]

Note: oreboot and coreboot do not implement boot loaders to access external
storage. Instead, they provide options for payloads that could load a final OS
or stand for themselves; it is up to the system design.
