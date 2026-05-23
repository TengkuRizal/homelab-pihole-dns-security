# Upstream DNS Sanitized

## Purpose

This document describes the sanitized upstream DNS configuration approach for the Pi-hole DNS security service.

The goal is to document the DNS forwarding design without exposing sensitive network details.

## Overview

Pi-hole receives DNS queries from homelab clients.

If a domain is allowed, Pi-hole forwards the query to the configured upstream DNS resolver.

If a domain is blocked, Pi-hole sinkholes the request and prevents the query from being forwarded.

## Upstream DNS Role

The upstream DNS resolver is responsible for resolving allowed domains that are not blocked by Pi-hole.

Pi-hole remains the local DNS filtering and visibility layer.

## Sanitized Configuration

| Setting | Value |
|---|---|
| Local DNS Resolver | Pi-hole |
| Pi-hole IP | <PIHOLE_IP> |
| Upstream DNS Provider | <UPSTREAM_DNS_PROVIDER> |
| DNS Port | 53 |
| Client DNS Assignment | Router DHCP or manual client setting |
| Public Exposure | No |

## Selection Criteria

An upstream DNS resolver should be selected based on:

- Reliability
- Low latency
- Privacy policy
- Security features
- Availability
- Compatibility with Pi-hole
- Suitability for homelab use

## Operational Considerations

Important considerations:

- Pi-hole should be the DNS resolver seen by clients
- Upstream DNS should only receive allowed queries
- Router DHCP settings should point clients to Pi-hole
- Fallback DNS should be documented carefully
- Avoid bypassing Pi-hole unless required for recovery
- Do not expose Pi-hole DNS service to the public internet

## Fallback DNS Consideration

Fallback DNS can restore connectivity during a Pi-hole outage, but it may reduce DNS visibility and filtering.

Fallback should be treated as a temporary recovery measure.

After Pi-hole is restored, client DNS settings should be reverted to Pi-hole.

## Validation

Validation checks:

- Confirm clients receive Pi-hole as DNS resolver
- Confirm Pi-hole forwards allowed queries upstream
- Confirm blocked domains are not forwarded
- Confirm DNS resolution works
- Confirm Pi-hole dashboard shows query activity

## Public Repository Safety

Do not publish:

- Real internal DNS mapping
- Sensitive upstream configuration
- Private client names
- Raw query logs
- MAC addresses
- Unsanitized screenshots
- Public IP details

## Future Improvements

- Document upstream DNS decision record
- Test latency between upstream providers
- Add DNS failover design
- Add secondary Pi-hole
- Add monitoring for upstream DNS failure
- Review privacy and security features of upstream DNS provider

