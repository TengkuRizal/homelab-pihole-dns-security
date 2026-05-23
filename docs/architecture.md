# Architecture

## Overview

This document describes the high-level architecture of the homelab DNS security service using Pi-hole running on Raspberry Pi.

Pi-hole acts as the primary DNS filtering layer for selected homelab clients. Client devices send DNS queries to Pi-hole, where queries are evaluated against configured blocklists and allowlists before being forwarded to upstream DNS resolvers.

The purpose of this architecture is to provide centralized DNS filtering, DNS query visibility, domain-level blocking, operational control over outbound DNS resolution, and a documented recovery model for DNS service failure.

## Logical Architecture

```text
Client Devices
     |
     | DNS Query TCP/UDP 53
     v
Pi-hole on Raspberry Pi
     |
     | Allowed DNS Queries
     v
Upstream DNS Resolver
     |
     v
Internet
```

## DNS Query Flow

1. Client device requests domain resolution.
2. Client sends the DNS query to Pi-hole.
3. Pi-hole checks the domain against configured blocklists and allowlists.
4. Allowed queries are forwarded to the upstream DNS resolver.
5. Blocked queries are sinkholed by Pi-hole.
6. DNS activity is reviewed from the Pi-hole dashboard for troubleshooting and operational visibility.

## Security Role

Pi-hole provides DNS-layer visibility and control inside the homelab network.

It helps with:

- Blocking advertising, tracking, telemetry, and unwanted domains
- Reducing unnecessary outbound DNS traffic
- Reviewing unusual DNS query behaviour
- Supporting endpoint troubleshooting
- Understanding which clients generate DNS traffic
- Providing a basic control point for domain-level filtering

## Reliability Consideration

DNS is a critical dependency. If Pi-hole is unavailable and clients rely only on Pi-hole for DNS, users may experience internet access issues because domain resolution fails.

For this reason, this project includes:

- DNS service recovery runbook
- Backup and restore documentation
- Monitoring and validation checks
- Fallback DNS consideration
- Future improvement plan for secondary Pi-hole

## Current Scope

The current implementation is a single Pi-hole instance running on Raspberry Pi.

This is suitable for homelab DNS filtering, DNS visibility, and operational learning. However, it introduces a single point of failure because DNS resolution depends on one device.

## Future Architecture Improvement

A future improvement is to deploy a secondary Pi-hole instance or another DNS failover mechanism.

Possible future design:

```text
Client Devices
     |
     | Primary DNS
     v
Primary Pi-hole
     |
     | Secondary DNS / Failover
     v
Secondary Pi-hole
     |
     v
Upstream DNS Resolver
```

## Out of Scope

This repository does not publish:

- Raw DNS query logs
- Private client hostnames
- MAC addresses
- Passwords or tokens
- Full internal network diagram
- Sensitive browsing history
- Unsanitized screenshots
