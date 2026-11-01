# Hardware/Software Co-Design

Integrated circuits, simulation, drivers, applications and compilers specific to
a purpose are often described as the main aspects of co-designing[^1] hardware
and software.

In PSI spec, however, we look at a different dimension:
How are [hardware and software combined](bootstrapping.md) as _platforms and
systems_?

## Platforms and Systems

There are multiple kinds of patforms and systems. In PSI spec, we are concerned
with _hardware and software platforms_ that are based on application processors
with peripherals and designed as a [System on Chip](application-processors.md).
We look at aspects of such platforms and how they provide interfaces for
versatile operating systems.

> [!NOTE]
> The two terms are closely related, often viewed as the same thing, and very
> abstract. In the following, a platform is more specific.

A **system** is a set of rules and multiple components that work together[^2].

A compute **platform** is a system with a specific set of interfaces[^3].

### Hardware

A **hardware system** comprises [processing units](application-processors.md),
memories and [peripherals](peripherals.md) connected via buses and/or networks.

A **hardware platform** is a specific implementation of instruction sets and
interfaces, such as processing unit control registers, shared memory, peripheral
register blocks and mailboxes, e.g. the Allwinner D1[^4]. In a broader sense,
this may include a board or an entire product.

### Software

A **software system** is a kernel or firmware runtime with its drivers and
libraries communicating via APIs.

A **software platform** is a software system, such as an operating system or
firmware, with its interfaces applied to a specific instruction set, e.g.,
FreeBSD on RISC-V[^5].

[^1]: <https://books.google.de/books?id=9C0yEEvJMrEC&redir_esc=y>
[^2]: <https://en.wikipedia.org/wiki/System>
[^3]: <https://en.wikipedia.org/wiki/Computing_platform>
[^4]: <https://docs.aw-ol.com/d1/en/>
[^5]: <https://wiki.freebsd.org/riscv>
