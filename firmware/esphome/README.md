# ESPHome Configurations

This directory contains ESPHome configurations used to validate and
develop the LED tower controller.

## Available Configurations

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