# Use Cases

This document describes practical use cases for the industrial signal
tower controller.

The goal of the system is to provide **clear visual feedback for
monitoring systems in physical environments** such as server rooms,
network cabinets, or control rooms.

------------------------------------------------------------------------

# Rack-Level Fault Indication

In server rooms or wiring centers, locating the source of a fault can
take time, especially when multiple racks or cabinets are involved.

A signal tower mounted on or near a rack can provide immediate visual
indication of the affected location.

``` mermaid
flowchart TD
    A[Monitoring detects fault<br/>RAID degraded / temperature alarm / network issue]
    --> B[Monitoring system triggers event]
    --> C[ESP32 signal tower controller receives command]
    --> D[Signal tower on affected rack changes state]
    --> E[Technician identifies correct rack immediately]
```

This approach reduces the time required to locate infrastructure issues.

------------------------------------------------------------------------

# Example Scenarios

## Datacenter / Server Rack

In datacenter environments, the signal tower can indicate failures
detected by infrastructure monitoring systems.

Possible alarm sources include:

-   RAID degradation
-   server hardware fault
-   overheating
-   power supply failure
-   network uplink loss

The tower provides a clear visual indication of the affected rack.

------------------------------------------------------------------------

## Wiring Center / Network Cabinet

Network cabinets often host switches, routers, and patch infrastructure.

Possible alarm sources include:

-   switch failure
-   fiber uplink problem
-   PoE overload
-   UPS state change
-   environmental alerts

Visual signaling can help technicians quickly identify the cabinet
requiring attention.

------------------------------------------------------------------------

## Operations / Control Room

Signal towers can also be used as a physical indicator in monitoring or
operations rooms.

Possible signals include:

-   aggregated alert count
-   infrastructure health status
-   energy consumption thresholds
-   service degradation

The tower can act as a high-visibility alert indicator for operators.

------------------------------------------------------------------------

# Operational Benefits

Compared to dashboard-only monitoring, local optical signaling provides
several advantages:

-   faster physical fault localization
-   reduced search time
-   improved operational clarity
-   increased visibility of critical alerts
-   flexible mapping of infrastructure states

This approach complements traditional monitoring dashboards by adding a
physical signaling layer.
