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
