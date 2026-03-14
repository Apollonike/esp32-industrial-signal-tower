## DNS Configuration

When ESPHome is running inside Docker or when the device is located in
a different network segment, mDNS discovery may not work.

In such setups it is recommended to configure a DNS entry for the device.

Example:

led-tower-01.geier.solutions → 10.40.1.52

The ESPHome configuration can then reference the device via DNS:

wifi:
  use_address: led-tower-01.geier.solutions