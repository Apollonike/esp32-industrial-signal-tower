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
    C --> D[Output Stage]
    D --> E[Signal Device]
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

The ESP32 acts as the central control unit of the system.

Responsibilities include:

- receiving control commands
- mapping system states to signal outputs
- controlling the switching stage
- managing communication with external monitoring systems

The controller communicates with external systems using standard
network protocols.

Depending on the deployment scenario, different connectivity options
may be used, such as:

- wired Ethernet
- Wi-Fi
- Ethernet combined with external power sources

For infrastructure-oriented deployments, **wired Ethernet is typically
preferred** due to improved reliability and operational stability.

The exact hardware configuration (for example power supply or Ethernet
interface modules) depends on the specific installation and is
described in the hardware documentation.

------------------------------------------------------------------------

## Switching Stage

The switching stage connects the low-voltage control signals of the
ESP32 controller to the external signaling device.

Its purpose is to translate microcontroller GPIO signals into
electrical switching of the individual signal channels.

Depending on the hardware implementation, the switching stage may use
different driver circuits suitable for the required voltage and current
levels.

Further details are described in the hardware design documentation.

------------------------------------------------------------------------

## Power Module

A power module provides the required operating voltages for both the
controller and the signal device.

Depending on the deployment scenario, the system may use different
power sources such as:

- local DC power supplies
- Power over Ethernet (PoE) splitters
- external power adapters

Voltage conversion stages may be used where required. The exact
electrical implementation is described in the hardware design
documentation.

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
