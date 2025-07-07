## Introduction

![PSI logo](images/logo.svg)

The Platform System Interface Specification, or _psi-spec_, is
a collection of documents for [hardware and software co-design](
#) from a general perspective.
It describes how [microprocessors](./application-processors) provide an
[environment for booting](boot-environments.md) operating systems or otherwise
bare-metal applications, typically starting from intermediate, rewritable code
that initializes clocks, DRAM and peripherals, commonly referred to as boot
firmware or [platform initialization firmware](platform-initialization.md).

In the following sections, _psi-spec_ describes principles and
abstractions that apply agnostic of vendors and products.
