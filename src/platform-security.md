## Platform Security

In order to design a secure platform, each and every component in the boot
process must be _measured_ and/or _verified_. In addition, the platform in its
entirety must be modeled so that only desired operations are permitted.

There is one essential question: _Who_ can execute code _where_ and _when_?

- when: which step/phase/stage in a boot flow chart (draw one)
- where: which component (can be hardware parts and software layers)
- who: owner, vendor, untrusted (w.r.t. owner) third party

**Note: Third parties contracted by vendors are considered to be acting as
controlled by the vendor here, regardless of practical issues with that.**
