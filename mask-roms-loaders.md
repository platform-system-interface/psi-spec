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
  - [`sunxi-fel`](https://github.com/linux-sunxi/sunxi-tools)
  - [`xfel`](https://github.com/xboot/xfel)
  - [`fel-cli`](https://github.com/Razican/fel-cli)
  - other tools exist
- Amlogic: (name unknown?), changed at least once over time (?)
  - [`pyamlboot`](https://github.com/superna9999/pyamlboot)
  - [`aml_boot`](https://github.com/orangecms/aml_boot)
  - other tools exist
- Rockchip: **TODO**
  - [`rkflashtool`](https://github.com/linux-rockchip/rkflashtool)
  - [`xrock`](https://github.com/xboot/xrock)

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

**Note**:
[oreboot
](https://github.com/oreboot/oreboot/tree/main/Documentation/boot-flow.md) and
[coreboot](https://doc.coreboot.org/getting_started/architecture.html) do not
implement boot loaders to access external storage themselves. Instead, they
provide options for payloads that could load a final OS or stand for themselves;
it is up to the vendor designing a system with it. A _boot block_ is only
necessary for some specific platforms, and possibly _CAR_ (cache-as-RAM).
RISC-V does not have a term for this, since it is conceptually not necessary.
Generic naming does not make much sense either, since different hardware
platforms require some stages or not depending on their constraints. Nor does
counting, due to different points of view: U-Boot, for example, starts counting
[backwards from its proper environment (the one offering a shell)](
https://u-boot.readthedocs.io/en/latest/develop/spl.html#u-boot-boot-phases), to
secondary and (rarely) tertiary program loader (SPL/TPL), while
[RISC-V starts counting forward, the mask ROM being the Zero Stage Boot Loader
(ZSBL)](https://riscv.org/wp-content/uploads/2019/12/Summit_bootflow.pdf).

### References

#### Arm platforms

- [How Arm systems are booted](https://youtu.be/GXFw8SV-51g)
- [U-Boot / Amlogic](https://youtu.be/u0-swEMDFp0)
- Arm secure boot chain on Ampere Altra
  * [Armed to boot talk](https://youtu.be/i2IG6Au34xM)
  * [Armed to boot blog post](https://blog.cloudflare.com/armed-to-boot/)
