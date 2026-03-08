# LED Signal Tower – Schematic Description

## Overview

This document describes the electrical schematic of the LED signal tower controller.

The system uses a simple transistor-based output stage to switch individual LED segments connected to a common **+12 V supply rail**.

The switching stage is controlled by an **ESP32-C3** microcontroller.

---

# Output Switching Topology

The LED tower is wired with a **common +12 V supply**.

Each LED segment is switched on the **low side** using an NPN transistor.

This topology simplifies the design and allows direct control from ESP32 GPIO pins.

---

# Simplified Output Circuit

```text
             +12 V
               │
               │
          LED Segment
               │
               │
             Collector
                │
             NPN Transistor
                │
             Emitter
                │
               GND

ESP GPIO ── 2.2 kΩ ── Base
                     │
                   100 kΩ
                     │
                    GND
```

---

# Output Channel Components

Each LED channel consists of three components.

| Component      | Typical Value           | Purpose                 |
| -------------- | ----------------------- | ----------------------- |
| NPN transistor | 2SC720 / BC547 / 2N3904 | Low-side switch         |
| Base resistor  | 2.2 kΩ                  | Limits base current     |
| Base pulldown  | 100 kΩ                  | Prevents floating input |

---

# Channel Assignment

The controller provides three independent LED outputs.

| Channel   | Signal Name | Description          |
| --------- | ----------- | -------------------- |
| Channel 1 | LED_RED     | Red signal output    |
| Channel 2 | LED_YELLOW  | Yellow signal output |
| Channel 3 | LED_GREEN   | Green signal output  |

---

# GPIO Mapping (Example)

The exact GPIO assignment can be adjusted in firmware.

Example configuration:

| ESP32-C3 GPIO | Function   |
| ------------- | ---------- |
| GPIO4         | LED_RED    |
| GPIO5         | LED_YELLOW |
| GPIO6         | LED_GREEN  |

Only standard GPIO pins should be used to avoid conflicts with boot or flash functions.

---

# Electrical Operation

## LED Off

When the GPIO output is **LOW**:

* no base current flows
* the transistor remains in cutoff
* the LED segment is disconnected from ground
* the LED remains off

---

## LED On

When the GPIO output is **HIGH**:

* base current flows through the base resistor
* the transistor enters saturation
* the LED segment is connected to ground
* current flows through the LED

---

# Current Analysis

Measured LED currents:

| Segment | Current |
| ------- | ------- |
| Red     | 8.0 mA  |
| Yellow  | 4.6 mA  |
| Green   | 5.8 mA  |

With a base resistor of **2.2 kΩ**, the base current is approximately:

```text
Ib = (3.3 V − 0.7 V) / 2200 Ω
Ib ≈ 1.18 mA
```

This provides ample drive current to saturate the transistor for the measured collector currents.

---

# LED Tower Connector

The LED tower is connected using a **4-pin connector**.

| Pin | Signal                 |
| --- | ---------------------- |
| 1   | LED_COMMON_POS (+12 V) |
| 2   | LED_RED_NEG            |
| 3   | LED_YELLOW_NEG         |
| 4   | LED_GREEN_NEG          |

---

# Power Distribution

The system power architecture is intentionally simple.

```text
PoE
 │
 └── PoE Splitter / DC-DC
        │
        ├── 12 V rail → LED tower
        │
        └── Step-Down Converter → ESP32 supply
```

---

# Recommended Power Filtering

For stable operation the following capacitors are recommended:

| Component            | Value  | Purpose                      |
| -------------------- | ------ | ---------------------------- |
| Bulk capacitor       | 100 µF | Stabilizes 12 V rail         |
| Decoupling capacitor | 100 nF | Local ESP32 supply filtering |

These components should be placed close to the respective supply inputs.

---

# Design Margin

Due to the extremely low current consumption of the LED modules, the transistor output stage operates far below its electrical limits.

This ensures:

* high reliability
* low thermal stress
* large electrical safety margin
