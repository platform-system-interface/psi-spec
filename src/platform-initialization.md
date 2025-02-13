## Platform Initialization

Booting a rich, virtual memory operating system poses challenges. While modern
machines may offer gigabytes or even terabytes of _dynamic random access memory_
[DRAM](https://en.wikipedia.org/wiki/Dynamic_random-access_memory) and extremely
high speed peripheral buses in the range of gigahertz frequencies, they still
start small with low amounts of static RAM and peripheral controllers in an
uninitialized state.

Early platform firmware takes the responsibility to bring up DRAM and other
controllers as needed to load and boot an operating system. Due to the high
diversity of hardware, every SoC, SoM and mainboard comes with specific
necessities.

### Boot Flows

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

**Note**:
Vendors may define artificial constraints in addition to their hardware
limitiations. For example, AMD implements DRAM initialization in signed code
that runs on a coprocessor before the main x86 cores come out of reset.
Because the signatures of the binaries involved are verified, they cannot be
customized by anyone but those who hold the signing keys, i.e., the vendor,
unless ways to circumvent the verification are found. This is also true for many
OEM products in general, where custom firmware is not part of the product
design. I.e., it is [protected against modification](platform-security.md).

### References

#### Arm platforms

- [How Arm systems are booted](https://youtu.be/GXFw8SV-51g)
- [U-Boot / Amlogic](https://youtu.be/u0-swEMDFp0)
- Arm secure boot chain on Ampere Altra
  * [Armed to boot talk](https://youtu.be/i2IG6Au34xM)
  * [Armed to boot blog post](https://blog.cloudflare.com/armed-to-boot/)

#### RISC-V platforms

**TODO**
