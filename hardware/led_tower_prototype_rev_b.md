[⬅ Back to Hardware Overview](README.md)

# LED Signal Tower – Prototype Rev.B

## Overview

Prototype Rev.B is a minor mechanical revision of the initial prototype.

The original layout (Rev.A) assumed a **30-row perfboard**.  
During assembly it was discovered that the available prototype boards
only provided **28 rows**, requiring a slight rearrangement of the
component placement.

---

## Reason for Revision

The change was purely mechanical:

- prototype PCB had **28 rows instead of 30**
- components had to be repositioned slightly
- wiring layout was adjusted to fit the available board

---

## Electrical Design

The electrical design remains **identical to Rev.A**.

No changes were made to:

- transistor driver stage
- GPIO assignments
- power supply architecture
- LED tower connector
- component values

---

## Firmware Compatibility

Rev.B uses the same GPIO assignments as Rev.A and is therefore fully
compatible with the existing firmware and ESPHome test configurations.

No firmware changes were required.

---

## Prototype Layout

![Prototype Rev.B PCB](../docs/images/pcb_prototype_rev_b.svg)

---

## Power Supply Used in Prototype

The prototype is currently powered by a simple external **12 V DC power
supply** connected to the input terminals.

While the system is designed to support **PoE powered deployments**, the
PoE hardware is not used in this prototype in order to keep the hardware
setup simple.

Functionally this is equivalent to using the 12 V output of a PoE
splitter.

## Summary

Rev.B represents a **mechanical adjustment** of the prototype layout
without electrical changes.

The revision ensures compatibility with commonly available
28-row perfboard prototypes while maintaining the original circuit design.