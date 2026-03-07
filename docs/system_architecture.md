# System Architecture

This document describes the high-level architecture of the signal tower
controller.

The system is designed to visualize monitoring states directly in
physical environments using an industrial signal tower. It acts as a
bridge between infrastructure monitoring systems and a physical
signaling device.

------------------------------------------------------------------------

# Architecture Overview

The controller receives monitoring events from external systems and
translates them into visual signals using an industrial LED tower.

``` mermaid
flowchart LR
    A[Monitoring System<br/>Checkmk / Zabbix / Prometheus / Scripts] --> B[Integration Layer<br/>MQTT / REST / Webhook / Automation]
    B --> C[ESP32 Controller]
    C --> D[Switching Stage]
    D --> E[DC-DC Power Module]
    E --> F[Industrial Signal Tower]
```

The architecture separates the system into several logical layers:

-   monitoring source
-   integration layer
-   embedded control layer
-   power and switching stage
-   physical signal device

This modular approach simplifies integration, maintenance, and hardware
replacement.

------------------------------------------------------------------------

# System Components

## Monitoring System

Monitoring platforms detect failures and abnormal states in
infrastructure components such as servers, network devices, or
production systems.

Typical examples include:

-   Checkmk
-   Zabbix
-   Prometheus
-   custom monitoring scripts

These systems generate events that represent the operational state of
monitored components.

------------------------------------------------------------------------

## Integration Layer

The integration layer converts monitoring events into control commands
for the signal tower controller.

Possible mechanisms include:

-   MQTT messages
-   REST API calls
-   webhook events
-   automation scripts

This layer allows the controller to remain independent of any specific
monitoring platform.

------------------------------------------------------------------------

## ESP32 Controller

The ESP32 acts as the central control unit.

Responsibilities include:

-   receiving control commands
-   mapping system states to signal outputs
-   controlling the switching stage
-   managing communication with the monitoring system

Depending on the hardware configuration, the controller may use:

-   Ethernet connectivity
-   Power over Ethernet (PoE)
-   Wi-Fi (primarily for development environments)

For infrastructure-oriented deployments, **wired Ethernet is the
preferred communication medium** due to improved reliability and
operational stability.

------------------------------------------------------------------------

## Switching Stage

The switching stage connects the low-voltage control signals of the
ESP32 to the signal tower modules.

Typical implementations may include:

-   MOSFET switching stages
-   driver modules
-   relay modules (optional)

The switching stage activates the individual signal outputs of the
tower.

------------------------------------------------------------------------

## Power Module

A DC-DC power module provides the required operating voltage for the
signal tower.

Possible configurations include:

-   local DC power supply
-   step-up converter from 5V to 12V
-   PoE powered system with integrated step-up conversion

The modular power stage simplifies replacement and reduces electrical
design complexity.

------------------------------------------------------------------------

## Industrial Signal Tower

Industrial signal towers consist of stacked light modules used to
indicate system states.

Typical colors represent operational states such as:

-   normal operation
-   warning conditions
-   critical alarms
-   service or maintenance states

These towers are widely used in industrial automation and monitoring
environments due to their high visibility and robustness.

------------------------------------------------------------------------

# Functional Flow

The typical event flow within the system is:

1.  A monitoring platform detects a system state change.
2.  The monitoring system sends an event to the integration layer.
3.  The integration layer translates the event into a controller
    command.
4.  The ESP32 processes the command and activates the appropriate
    output.
5.  The signal tower displays the corresponding visual signal.

------------------------------------------------------------------------

# Typical Signal Mapping

A common mapping between system states and tower colors may look like
this:

  Color          Meaning
  -------------- ------------------------
  Green          Normal operation
  Yellow         Warning condition
  Red            Critical alarm
  Blue / White   Service or maintenance

The exact mapping can be adapted depending on the operational
requirements of the installation.

------------------------------------------------------------------------

# Reliability Considerations

In monitoring environments, communication failures must be handled
carefully.

If the controller loses communication with the monitoring system, the
displayed signal may no longer represent the current system state.

Possible mitigation strategies include:

-   heartbeat supervision
-   communication timeout detection
-   fallback signal states
-   dedicated communication failure indication

Further details are described in the network reliability documentation.

------------------------------------------------------------------------

# Related Documentation

Additional architectural aspects are described in the following
documents:

-   Hardware Architecture
-   Power Architecture
-   Network and Reliability Considerations
