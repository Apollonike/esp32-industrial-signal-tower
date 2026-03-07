# Power Architecture

This document describes the power supply architecture of the signal
tower controller.

The system is designed to support multiple power supply configurations
depending on the installation environment. The primary goal is to enable
**simple deployment, high reliability, and minimal installation
effort**.

In many infrastructure environments, adding new power wiring is costly
and may require service interruptions. Therefore the design supports
both **direct DC power supply** and **Power over Ethernet (PoE)**.

------------------------------------------------------------------------

# Power Architecture Overview

The controller can be powered using different approaches depending on
the deployment scenario.

``` mermaid
flowchart LR
    A[Local DC Supply<br/>12V / 24V] --> B[Controller Power Stage]
    C[PoE Switch] --> D[PoE Module / PoE HAT]
    D --> B
    B --> E[Step-Up Converter]
    E --> F[Industrial Signal Tower]
```

The architecture allows the controller to operate in environments where
either local power supplies or PoE network infrastructure are available.

------------------------------------------------------------------------

# Direct DC Supply

The simplest configuration uses a local DC power supply.

Typical configuration:

    12V / 24V power supply → controller → signal tower

This configuration is straightforward but requires dedicated power
wiring.

Advantages:

-   simple electrical architecture
-   direct compatibility with many industrial power systems
-   suitable for installations where power is already available

Limitations:

-   additional power cabling required
-   more complex installation in network cabinets or server racks

------------------------------------------------------------------------

# Power over Ethernet (PoE)

A more flexible option is powering the controller via **Power over
Ethernet**.

In many modern infrastructure environments, PoE-capable switches are
already present for devices such as:

-   wireless access points
-   IP cameras
-   VoIP phones
-   monitoring devices

Using PoE allows the signal tower controller to be installed with a
**single Ethernet cable providing both power and data connectivity**.

Typical architecture:

    PoE switch → PoE module → ESP controller → step-up converter → signal tower

Advantages:

-   single-cable installation
-   reduced deployment effort
-   ideal for racks and network cabinets
-   centralized power management
-   automatic UPS backup if PoE switch is UPS-backed

------------------------------------------------------------------------

# Step-Up Converter

Industrial signal towers typically operate at **12V or 24V**, while many
embedded controllers operate at **5V or 3.3V**.

When powered via PoE, the controller usually receives a regulated **5V
supply** from the PoE module.

A **step-up (boost) converter** can then generate the required tower
voltage.

Example:

    5V → Step-Up Converter → 12V output → Signal Tower

This allows the system to drive industrial signal towers while keeping
the controller electronics simple and modular.

Advantages of using modular step-up converters:

-   reduced electrical design complexity
-   easy replacement if defective
-   widely available components
-   flexibility for different tower voltage requirements

------------------------------------------------------------------------

# Design Considerations

Supporting multiple power architectures provides flexibility during
deployment.

PoE is particularly advantageous in **network-centric environments**,
where Ethernet infrastructure already exists.

Key considerations include:

-   installation simplicity
-   infrastructure compatibility
-   maintenance requirements
-   system reliability

In many datacenter or network cabinet deployments, PoE can significantly
reduce installation time and eliminate the need for additional power
wiring.

------------------------------------------------------------------------

# Related Documentation

Additional architectural aspects are described in the following
documents:

-   System Architecture
-   Hardware Architecture
-   Network and Reliability Considerations
