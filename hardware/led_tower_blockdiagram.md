# LED Signal Tower – System Block Diagram

## Overview

This document provides a high-level overview of the LED signal tower controller architecture.

The system is designed as a **PoE-powered network device** capable of controlling three LED segments via an ESP32-C3 microcontroller.

The hardware architecture prioritizes simplicity and reliability.

---

# System Architecture

The following block diagram illustrates the main system components.

```text id="zzg2gx"
                 +----------------------+
                 |        Network       |
                 |   (Ethernet / IoT)   |
                 +----------+-----------+
                            |
                            |
                       PoE Switch
                            |
                            |
                    +-------+-------+
                    |   PoE Splitter |
                    | (Power + Data) |
                    +-------+--------+
                            |
                            |
                           12 V
                            |
        +-------------------+-------------------+
        |                                       |
        |                                       |
+-------+--------+                     +--------+--------+
|  Step-Down     |                     |  LED Tower      |
|  Converter     |                     |  Common +12 V   |
|  12 V → 3.3 V  |                     |                 |
+-------+--------+                     +--------+--------+
        |                                       |
        |                                       |
        v                                       v
+--------------------+                +--------------------+
|     ESP32-C3       |                |  LED Segments      |
|                    |                |                    |
| GPIO_RED  ---------+----------------> RED LED           |
| GPIO_YEL  ---------+----------------> YELLOW LED        |
| GPIO_GRN  ---------+----------------> GREEN LED         |
|                    |                |                    |
+--------------------+                +--------------------+
```

---

# Functional Blocks

## Network / PoE

The device receives power and network connectivity through **Power over Ethernet (PoE)**.

A PoE splitter separates:

* power
* network data

The splitter provides a regulated **12 V output rail**.

---

## Power Conversion

The system uses two voltage domains:

| Voltage | Purpose             |
| ------- | ------------------- |
| 12 V    | LED tower supply    |
| 3.3 V   | ESP32-C3 controller |

A **step-down converter** generates the controller supply voltage.

---

## Controller

The system controller is an **ESP32-C3** microcontroller.

Responsibilities include:

* network communication
* command processing
* LED state control
* integration with automation systems

Each LED segment is controlled by a dedicated GPIO pin.

---

## LED Output Stage

The LED tower segments are controlled using **low-side transistor switches**.

Advantages of this approach:

* minimal component count
* high reliability
* simple PCB layout
* large electrical safety margin

The LED tower is wired with:

```
Common +12 V
Individual switched ground lines
```

---

# Signal Flow

System control flow:

```text id="9gb44x"
Automation System
        │
        │
        ▼
ESP32 Network Stack
        │
        │
        ▼
GPIO Output Signals
        │
        │
        ▼
Transistor Output Stage
        │
        │
        ▼
LED Tower Segments
```

---

# Power Flow

Electrical power flow:

```text id="4gt3gk"
PoE Switch
    │
    ▼
PoE Splitter
    │
    ├── 12 V → LED Tower
    │
    └── Step-Down Converter
            │
            ▼
          ESP32
```

---

# Design Philosophy

The hardware architecture is intentionally simple.

Key principles:

* avoid unnecessary power conversion stages
* use minimal components
* ensure robust operation
* simplify debugging and maintenance

Due to the very low current consumption of the LED modules, a simple transistor switching stage is sufficient for reliable operation.

---

# Future Extensions

Possible future improvements include:

* integrated PoE module
* PCB miniaturization
* relay expansion board for industrial towers
* additional status indicators
* hardware watchdog
* enclosure integration
