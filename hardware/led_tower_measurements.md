[⬅ Back to Hardware Architecture](../docs/hardware_architecture.md)

---
# LED Signal Tower – Electrical Measurements

## Purpose

This document records electrical measurements performed on the prototype LED signal tower.

The goal of these measurements is to determine the actual electrical load of the LED modules in order to validate the hardware design.

The results are used to confirm that a simple transistor-based switching stage is sufficient.

---

# Test Setup

The measurements were performed using a laboratory setup with a regulated DC power supply.

| Parameter           | Value                            |
| ------------------- | -------------------------------- |
| Supply voltage      | 12.11 V                          |
| LED tower type      | Generic no-name signal tower     |
| Measurement method  | Steady-state current measurement |
| Ambient temperature | Room temperature                 |

Each LED segment was measured individually.

---

# Measured Current per Segment

| Segment | Current |
| ------- | ------- |
| Red     | 8.0 mA  |
| Green   | 5.8 mA  |
| Yellow  | 4.6 mA  |

---

# Calculated Power Consumption

Power consumption was calculated using:

```
P = U × I
```

Where:

* **U** = supply voltage
* **I** = measured current

| Segment | Current | Power   |
| ------- | ------- | ------- |
| Red     | 8.0 mA  | 0.097 W |
| Green   | 5.8 mA  | 0.070 W |
| Yellow  | 4.6 mA  | 0.056 W |

---

# Combined Load

All segments active simultaneously:

| Active Segments      | Current |
| -------------------- | ------- |
| Red + Green + Yellow | 18.4 mA |

Total power consumption:

```
P = 12.11 V × 0.0184 A
P ≈ 0.223 W
```

---

# Startup Behaviour

No measurable inrush current was detected using the available measurement equipment.

The LED modules appear to contain internal current limiting components.

---

# Observed Electrical Characteristics

Key observations:

* extremely low current consumption
* stable operation at ~12 V
* no detectable startup current spike
* LED modules operate independent of polarity

---

# Design Implications

These measurements confirm that the LED tower represents a **very small electrical load**.

Implications for the hardware design:

* relay outputs are unnecessary
* boost converters are unnecessary
* transistor switching is fully sufficient
* thermal stress on switching components is negligible

The dominant power consumption of the system will be the controller electronics rather than the LED tower itself.

---

# Future Measurements

Additional measurements may be added later:

* operation at different voltages
* long-term stability tests
* temperature measurements under enclosure conditions
* full system power consumption including ESP32 and network interface
