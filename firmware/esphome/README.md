# ESPHome Firmware

This directory contains ESPHome configurations used to validate and
develop the LED tower controller.

## Available Configurations

### GPIO Test

Tests the transistor output stage by switching the LED tower segments.

- [led_tower_rev_b_gpio_test.yaml](led_tower_rev_b_gpio_test.yaml)

## Notes

The current GPIO test configuration is intended for basic hardware
validation of:

- ESP32-C3 SuperMini
- transistor output stage
- LED tower wiring

GPIO mapping used in Rev.B:

- GPIO10 → Red
- GPIO21 → Yellow
- GPIO20 → Green

### Ethernet Test (W5500)

Validates the SPI Ethernet module and DHCP connectivity.

- [led_tower_rev_b_ethernet_test.yaml](led_tower_rev_b_ethernet_test.yaml)

Test results for Prototype Rev.B:

- ESP32-C3 controller starts successfully
- W5500 Ethernet module initializes correctly
- DHCP address is obtained
- 100 Mbit full duplex link established