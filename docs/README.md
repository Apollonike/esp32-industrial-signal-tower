# System Documentation

This directory contains the architectural and technical documentation of
the ESP32 Industrial Signal Tower controller.

The documents in this section describe the system design, hardware
architecture, firmware behavior, and prototype implementations.

---

# Architecture Documents

## System Architecture

High-level system architecture describing the interaction between
monitoring systems, integration layer, controller, and signal device.

- [System Architecture](system_architecture.md)

## Hardware Architecture

Overview of the modular hardware architecture of the controller,
including power distribution, controller module, and output stage.

- [Hardware Architecture](hardware_architecture.md)

---

# Hardware Design

## LED Tower Hardware Design

Description of the electrical design of the LED signal tower controller.

- [LED Tower Design](led_tower_design.md)

## LED Tower Schematic

Detailed description of the transistor switching stage and LED tower
wiring.

- [LED Tower Schematic](led_tower_schematic.md)

---

# Prototype Implementations

## Prototype Revision A

Initial prototype layout and construction.

- [Prototype Rev.A](led_tower_prototype_rev_a.md)

## Prototype Revision B

Updated prototype layout adjusted for the 28-row perfboard.

- [Prototype Rev.B](led_tower_prototype_rev_b.md)

---

# Firmware Behavior

Description of the ESPHome firmware behavior including:

- signal states
- heartbeat supervision
- Home Assistant integration

- [Software Behavior](software_behavior.md)

---

# Images

Architecture diagrams, screenshots, and prototype photos are stored in:


docs/images/


---

# Related Documentation

Additional project documentation can be found in the repository root.

- [Project Overview](../README.md)