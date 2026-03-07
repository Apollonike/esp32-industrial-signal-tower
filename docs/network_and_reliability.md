# Network and Reliability Considerations

This document describes networking and operational reliability aspects
of the signal tower controller.

Because the device is intended to visualize monitoring states in
infrastructure environments, **network reliability and predictable
behaviour during failures** are important design considerations.

------------------------------------------------------------------------

# Preferred Network Medium

For production-oriented deployments, **wired Ethernet is the preferred
communication medium**.

Infrastructure environments such as datacenters, wiring centers, or
industrial installations typically rely on structured cabling, which
provides predictable network availability.

Advantages of Ethernet include:

-   improved reliability compared to wireless communication
-   lower attack surface
-   predictable availability
-   no dependency on RF conditions
-   deterministic connectivity
-   better suitability for structured infrastructure environments

For installations where Power over Ethernet (PoE) is available, Ethernet
can also provide both **network connectivity and power delivery via a
single cable**.

------------------------------------------------------------------------

# Wi‑Fi Limitations

Wi‑Fi may still be useful in the following scenarios:

-   development environments
-   temporary installations
-   prototype setups
-   locations without structured cabling

However, Wi‑Fi has several limitations that make it less suitable for
critical monitoring visualization systems.

Potential issues include:

-   unstable coverage depending on building layout
-   radio interference
-   shared bandwidth with mobile devices
-   roaming or reconnection delays
-   increased security exposure

For these reasons, Wi‑Fi should generally be considered a **secondary
option** rather than the primary connectivity method in infrastructure
environments.

------------------------------------------------------------------------

# Communication Failure Behaviour

One important reliability consideration is the behaviour of the
controller when communication with the monitoring system is interrupted.

If the controller simply continues to display the **last received signal
state**, the visual indication may become outdated or misleading.

To avoid this situation, the system should implement supervision
mechanisms.

Recommended strategies include:

-   heartbeat messages from the monitoring platform
-   communication timeout detection
-   transition to a defined fallback state
-   optional local fault indication
-   visual indication of communication loss

Such mechanisms help ensure that the displayed signal always reflects a
valid and current system state.

------------------------------------------------------------------------

# Operational Considerations

In infrastructure environments, monitoring systems are often part of a
larger operations workflow.

A reliable signaling system should therefore:

-   integrate cleanly with monitoring platforms
-   provide predictable behaviour during failures
-   avoid misleading visual states
-   remain simple to operate and maintain

These considerations help ensure that the signal tower acts as a useful
extension of the monitoring system rather than an additional point of
failure.

------------------------------------------------------------------------

# Scope Limitation

The controller is designed for **monitoring visualization and
operational status indication**.

It is **not a certified safety device** and must not be used as a
replacement for functional safety systems such as:

-   safety PLCs
-   certified machine safety controllers
-   emergency shutdown systems

Safety‑critical signaling must always be implemented using appropriately
certified systems.
