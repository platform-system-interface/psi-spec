# Platform System Interface Specification

![PSI logo](images/logo.svg)

The Platform System Interface Specification, or _psi-spec_, is
a collection of documents for [hardware and software co-design](
#) from a general perspective. It describes how microprocessors
set up an environment for an operating system or otherwise
bare-metal applications, typically through intermediate,
rewritable code that initializes clocks, DRAM and peripherals,
commomly referred to as [firmware](#).

In the following sections, _psi-spec_ describes principles and
abstractions that apply agnostic of vendors and products.
