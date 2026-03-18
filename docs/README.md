# System Documentation

This directory contains the architectural documentation of the
ESP32 Industrial Signal Tower controller.

The documents in this section describe the overall system design,
independent of specific hardware implementation details.

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

## Power Architecture

Description of the system power concept, including the 12 V rail and
controller supply generation.

- [Power Architecture](power_architecture.md)

## Network and Reliability

Description of network communication, reliability considerations,
and behavior during communication failures.

- [Network and Reliability](network_and_reliability.md)

## Home Assistant Integration

Example Home Assistant configurations and automations:

- [Home Assistant Setup](home_assistant/README.md)
- [Heartbeat Automation](home_assistant/heartbeat_automation.yaml)

## Use Cases

Example deployment scenarios and practical applications of the
signal tower controller.

- [Use Cases](use_cases.md)

---

# Images

Architecture diagrams and supporting images are stored in:

`docs/images/`

---

# Related Documentation

Detailed hardware design and prototype documentation can be found in:

- [Hardware Documentation](../hardware/README.md)

Project overview:

- [Project README](../README.md)