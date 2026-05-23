# Network Flow

## Purpose

This document describes the DNS network flow for the Pi-hole DNS security service.

The goal is to show how client DNS queries move through Pi-hole, how filtering happens, and where upstream DNS resolution occurs.

## High-Level Flow

The expected DNS flow is:

Client Device -> Pi-hole -> Upstream DNS Resolver -> Internet

Pi-hole acts as the local DNS filtering and visibility point.

## Normal DNS Flow

1. Client device requests a domain.
2. Client sends DNS query to Pi-hole.
3. Pi-hole checks the domain against blocklists and allowlists.
4. If the domain is allowed, Pi-hole forwards the query to upstream DNS.
5. Upstream DNS returns the answer to Pi-hole.
6. Pi-hole returns the answer to the client.
7. Client connects to the resolved destination.

## Blocked DNS Flow

1. Client device requests a blocked domain.
2. Client sends DNS query to Pi-hole.
3. Pi-hole matches the domain against a blocklist.
4. Pi-hole blocks or sinkholes the request.
5. Query is visible in the Pi-hole dashboard.
6. The request is not forwarded normally to upstream DNS.

## DNS Ports

| Protocol | Port | Purpose |
|---|---|---|
| UDP | 53 | Standard DNS query |
| TCP | 53 | DNS fallback or larger DNS response |
| HTTP or HTTPS | Internal dashboard access | Pi-hole admin interface |

## Client DNS Assignment

Clients may receive Pi-hole as DNS resolver through:

- Router DHCP setting
- Manual DNS setting
- Static network configuration
- Lab-specific network configuration

The preferred approach is router DHCP assignment because it centralizes DNS configuration.

## Failure Scenarios

Possible failure scenarios:

| Scenario | Impact |
|---|---|
| Pi-hole down | Clients may fail to resolve domains |
| Raspberry Pi unreachable | DNS filtering unavailable |
| Upstream DNS unavailable | Allowed domains may fail to resolve |
| Router DHCP misconfigured | Clients may not use Pi-hole |
| Client uses external DNS | DNS visibility and filtering may be bypassed |
| Aggressive blocklist | Legitimate domains may fail |

## Validation

Validation should confirm:

- Client receives Pi-hole as DNS resolver
- Pi-hole receives client queries
- Allowed domains resolve successfully
- Blocked domains are blocked
- Upstream DNS forwarding works
- Query activity appears in Pi-hole dashboard

## Public Repository Safety

Do not publish:

- Real client names
- Full internal network map
- MAC addresses
- Sensitive private IP mapping
- Raw query logs
- Unsanitized screenshots

## Future Improvements

- Add network diagram image
- Add secondary Pi-hole flow
- Add firewall rule to prevent DNS bypass
- Add DNS failover testing
- Add monitoring from another homelab node
