# Hardware Architecture

This document describes the hardware architecture of the industrial
signal tower controller.

The design follows a **modular hardware concept** that prioritizes
maintainability, flexibility, and rapid replacement of individual
components.

Instead of building a highly integrated custom PCB from the beginning,
the system is intentionally structured as a set of interchangeable
modules.

This approach simplifies prototyping, reduces development risk, and
allows hardware components to be replaced easily in operational
environments.

------------------------------------------------------------------------

# Design Principles

The hardware architecture separates the system into several functional
layers.

The main design principles are:

-   modular hardware architecture
-   use of widely available components
-   minimal custom power electronics
-   easy replacement of defective modules
-   suitability for prototypes and small-scale deployments

Instead of integrating all functions into a single PCB, the following
functional blocks are separated:

-   control logic
-   output stage
-   power conversion
-   signal device

------------------------------------------------------------------------

# Hardware Block Diagram

``` mermaid
flowchart LR
    A[Power Input<br/>12V Supply / PoE Splitter] --> B[12V System Rail]
    B --> C[Step-Down Converter<br/>ESP32 Supply]
    C --> D[ESP32 Controller Module]
    D --> E[Output Stage]
    B --> E
    E --> F[Signal Device<br/>LED Signal Tower]
```

The carrier platform distributes power and signals between the modules.
This modular structure allows different implementations of the output
stage or signal device without redesigning the entire controller.

------------------------------------------------------------------------

# Controller Module

The controller module contains the ESP32 microcontroller responsible
for:

-   communication with monitoring systems
-   signal state processing
-   output control
-   network connectivity

Depending on the deployment scenario, the controller may use:

-   Ethernet connectivity
-   Wi‑Fi (primarily for development environments)
-   Ethernet combined with external power sources

For infrastructure-oriented installations, **wired Ethernet is typically
preferred** due to higher reliability and operational stability.

------------------------------------------------------------------------

# Output Stage

The output stage connects the low-voltage GPIO signals of the ESP32 to
the external signaling device.

Its purpose is to translate microcontroller control signals into
electrical switching of the individual signal channels.

The architecture allows different implementations depending on the
target hardware.

Typical implementations may include:

* transistor-based low-side switching stages
* MOSFET driver stages
* relay modules for switching external loads

The current prototype uses a **simple transistor-based driver stage**
to control a low-power LED signal tower.

Because the controller only provides logic-level control signals, the
output stage can be replaced or extended without modifying the core
controller design.

------------------------------------------------------------------------

# Power Conversion

Industrial signal towers typically operate on **12V or 24V supply
voltage**, while the controller electronics require **3.3V or 5V**.

To supply the different voltage domains, the system uses a **modular
power conversion stage**.

Possible power sources include:

* external DC power supplies
* PoE splitters
* dedicated DC adapters

In the current prototype configuration, the system uses a **12V system
rail** which directly powers the LED tower.

A **step-down converter** is used to generate the supply voltage for the
ESP32 controller.

This architecture minimizes the number of power conversion stages and
keeps the electrical design simple and efficient.

------------------------------------------------------------------------

# Modular Hardware Strategy

The modular concept provides several operational advantages:

-   simplified troubleshooting
-   rapid replacement of defective modules
-   reduced development complexity
-   easier sourcing of replacement parts
-   flexibility for different deployment scenarios

While a fully integrated PCB might be preferable for large-scale
manufacturing, the modular design is better suited for:

-   experimental infrastructure projects
-   prototyping
-   small batch production
-   field-serviceable installations

------------------------------------------------------------------------

# Maintenance Perspective

Industrial signal towers are sometimes damaged or replaced during normal
operation, especially in production environments.

A modular control platform allows maintenance personnel to replace
individual hardware components quickly without replacing the entire
controller.

This reduces downtime and simplifies service procedures.

------------------------------------------------------------------------

# Detailed Hardware Documentation

More detailed information about the LED signal tower controller hardware
can be found in the following documents.

## LED Tower Hardware Design

Complete description of the LED tower controller hardware design,
including power architecture and switching concept.

-   [LED Tower Hardware Design](../hardware/led_tower_design.md)

## Electrical Measurements

Measured current consumption and electrical characteristics of the LED
tower modules used in the prototype.

-   [LED Tower Electrical
    Measurements](../hardware/led_tower_measurements.md)

## Schematic Description

Detailed explanation of the switching stage, GPIO mapping, and connector
layout.

-   [LED Tower Schematic
    Description](../hardware/led_tower_schematic.md)

## System Block Diagram

High-level system architecture showing the relationship between power
supply, controller, and LED tower modules.

-   [LED Tower Block Diagram](../hardware/led_tower_blockdiagram.md)

# Prototype Status

The hardware architecture has been validated using a perfboard
prototype (Prototype Rev.B).

Validated subsystems include:

- ESP32-C3 controller module
- LM2596 power supply stage
- transistor-based LED driver stage
- W5500 SPI Ethernet interface

Further integration with monitoring systems and automation platforms
is performed via ESPHome firmware.

------------------------------------------------------------------------

# Related Documentation

Additional system aspects are described in the following documents:

-   System Architecture
-   Power Architecture
-   Network and Reliability Considerations
