## Secure Boot

A platform is only as secure as the weakest link in the chain of its initial
setup. To ensure integrity and only execute approved code with its desired
configuration, a multitude of aspects has to be considered.

### Root of Trust

A _Root of Trust_ (RoT) is the single first step in a flow of execution that is
also called the _trust anchor_ of the platform. The full flow is also called a
_chain of trust_: Each and every part of the chain has to check on the
respective next one before executing it in order to guarantee integrity.

### OTP Fuses

One way of storing information used to verify the first piece of software is a
special block of storage within an SoC which is called One-Time Programmable
(Fuses). Once programmed, or fused, this area of storage is used by the SoC's
mask ROM for signature checks or similar. Vendors may call this storage area
different. For example, Intel has the _Field Programmable Fuses_ (FPFs).

### Trusted Platform Module

A Trusted Platform Module (TPM) is ...

### Verification and Attestation

There are multiple established modes of operation for platform security.

_Verification_ means that there is a _Static Root of Trust_ (SRoT) and each part
of the chain of trust has a clear owner that holds the keys to sign their code.
This approach is also called _trusted boot_.

_Attestation_ means that there is a component in the system to store
_measurements_ (e.g., hashes in a TPM) which are exchanged with a witness via a
suitable protocol. The witness (e.g., end user or service) will then attest that
the system is in a good state or alarm otherwise. This is also known as
_measured boot_.

### Ownership

If an OEM owns the root of trust, then they are the ultimate owner of the
platform. That means, in case they stop providing updates or are slow to fix
issues such as in the [UEFI ecosystem](
https://uefi.org/sites/default/files/resources/Decoding%20UEFI%20Firmware-Aug24-2023-Final_v2_0.pdf),
a device owner may suffer from uncertainty or compromises without even knowing.

### References

https://trustedcomputinggroup.org/resource/d-rtm-architecture-specification/

https://trustedcomputinggroup.org/wp-content/uploads/DRTM-Specification-Overview_June2013.pdf

https://www.amd.com/content/dam/amd/en/documents/epyc-technical-docs/user-guides/58453.pdf

https://www.intel.com/content/dam/develop/external/us/en/documents/uefi-pi-tcg-firmware-white-paper-1-820238.pdf

https://trustedfirmware-a.readthedocs.io/en/v2.11/design_documents/drtm_poc.html

https://documentation-service.arm.com/static/647731f816f0f201aa6b7607?token=

https://lpc.events/event/11/contributions/1122/attachments/881/1689/Dynamic%20Root%20of%20Trust(D-RTM)%20on%20non-x86%20architectures%20like%20ARM%20and%20POWER9.pdf

https://archive.fosdem.org/2024/events/attachments/fosdem-2024-3724-trenchboot-project-status-update/slides/22916/DRTM-presentation-FOSDEM_Crm6zWi.pdf

https://ieeexplore.ieee.org/document/6120848
