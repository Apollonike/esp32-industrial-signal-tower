# ESPHome Firmware

This directory contains the ESPHome configurations used during
development and validation of the ESP32 Industrial Signal Tower
controller.

The firmware examples demonstrate the different development stages
of the project from hardware validation to the final operational
signal tower firmware.

---

# Development Firmware

## GPIO Hardware Test

Tests the transistor output stage by manually switching the LED tower segments.

- [led_tower_rev_b_gpio_test.yaml](led_tower_rev_b_gpio_test.yaml)

This configuration was used to validate:

- ESP32-C3 SuperMini operation
- transistor switching stage
- LED tower wiring
- GPIO assignments

GPIO mapping used in Rev.B:

- GPIO10 → Red
- GPIO21 → Yellow
- GPIO20 → Green

---

## Ethernet Test (W5500)

Validates the SPI Ethernet module and DHCP connectivity.

- [led_tower_rev_b_ethernet_test.yaml](led_tower_rev_b_ethernet_test.yaml)

This configuration verifies:

- SPI communication with the W5500
- Ethernet initialization
- DHCP address acquisition
- network connectivity

Test results for Prototype Rev.B:

- ESP32-C3 controller starts successfully
- W5500 Ethernet module initializes correctly
- DHCP address obtained
- 100 Mbit full duplex link established

---

# Production Firmware

The final firmware used for the signal tower prototype integrates
all hardware components and implements the operational signalling
logic used by the monitoring system.

- [led_tower.yaml](led_tower.yaml)

This firmware provides the following features:

- WiFi connectivity for integration with Home Assistant
- selectable tower status via Home Assistant entity
- deterministic state machine for signal behaviour
- watchdog-style heartbeat monitoring

Supported tower states:

| State | Behaviour |
|------|-----------|
| Off | All LEDs off |
| OK | Green steady |
| Warning | Yellow steady |
| Warning Blink | Yellow blinking |
| Alarm | Red steady |
| Alarm Blink Slow | Red blinking (1s interval) |
| Alarm Blink Fast | Red blinking (0.5s interval) |

---

# Heartbeat Monitoring

The firmware includes a heartbeat mechanism to detect loss of
communication with the monitoring system.

If no heartbeat signal is received within the defined timeout:

- all tower segments flash briefly every **3 seconds**

This indicates that the signal tower is operational but has lost
communication with the monitoring system.

The heartbeat mechanism is intentionally implemented in a way that
does not interfere with active signal patterns.

---

# Integration

The firmware is designed to integrate with:

- Home Assistant
- infrastructure monitoring systems
- automation platforms

Signal states can be controlled via Home Assistant entities and
automations.

---

# Firmware Architecture

The firmware implements a simple state-driven signalling model:


Monitoring System → Home Assistant → ESPHome API → Signal Tower Controller


This architecture keeps the firmware simple while allowing complex
logic to be implemented in the automation platform.

---

# Hardware Compatibility

Current firmware targets the following hardware configuration:

- ESP32-C3 SuperMini
- W5500 SPI Ethernet module
- LM2596 step-down power supply
- NPN transistor switching stage
- industrial 12V LED signal tower
