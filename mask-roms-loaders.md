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

| Project/Vendor    | mask ROM | ................ | ..... | .................. | ................... | .......... |
| ----------------- | -------- | ---------------- | ----- | ------------------ | ------------------- | ---------- |
| U-Boot            |   (N/A)  |       TPL        |  SPL  | platform-dependent |     U-Boot proper   | OS         |
| EDK2              |   (N/A)  |       SEC        |  PEI  |        DXE         |         BDS         | payload/OS |
| Oxide             |   (N/A)  |       phbl       |   X   |        (-)         |         (-)         |     OS     |
| coreboot          |   (N/A)  | boot block / CAR |  ROM  |     RAM stage      |       payload       |     OS     |
| sunxi (Allwinner) |    FEL   |       (-)        | boot0 | maybe intermediate | maybe U-Boot proper |     OS     |
| RISC-V            |   ZSBL   |       (-)        |  FSBL |        SBI         |     boot loader     |     OS     |
| oreboot           | mask ROM |    boot block    |  bt0  |        main        |      LinuxBoot      |     OS     |

Note: oreboot and coreboot do not implement boot loaders to access external
storage. Instead, they provide options for payloads that could load a final OS
or stand for themselves; it is up to the system design. A _boot block_ is only
necessary for some specific platforms, and possibly _CAR_ (cache-as-RAM).
RISC-V does not have a term for this, since it is conceptually not necessary.
Generic naming or counting does not make much sense either, since different
hardware platforms require some stages or not depending on their constraints.
U-Boot, for example, starts counting backwards from its proper environment (the
one offering a shell), to secondary and (rarely) tertiary program loader
(SPL/TPL), while RISC-V starts counting forward, the mask ROM being the Zero
Stage Boot Loader (ZSBL).
