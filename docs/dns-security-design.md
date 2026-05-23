# DNS Security Design

## Overview

This document explains the DNS security design for the homelab Pi-hole deployment.

Pi-hole is used as a centralized DNS filtering layer to provide visibility, control, and basic protection against unwanted domain lookups.

The goal is not only to block advertisements, but to operate DNS as a controlled and observable network service.

## Security Objectives

The DNS security layer is designed to achieve the following objectives:

- Centralize DNS resolution for selected homelab clients
- Improve visibility of DNS queries
- Block advertising, tracking, telemetry, and unwanted domains
- Reduce unnecessary outbound DNS traffic
- Support troubleshooting of suspicious endpoint behaviour
- Provide an operational control point for domain-level filtering

## DNS Filtering Strategy

Pi-hole receives DNS queries from clients and checks each requested domain against configured blocklists and allowlists.

If a domain matches a blocklist, Pi-hole blocks or sinkholes the request.

If the domain is allowed, the query is forwarded to the configured upstream DNS resolver.

## Blocklist Strategy

Blocklists are used to reduce unwanted traffic and known low-value domains.

The blocklist strategy should follow these principles:

- Use reputable and maintained blocklists
- Avoid adding too many aggressive lists without validation
- Review false positives before adding new lists
- Document any custom blocklist decision
- Validate that important services still work after blocklist updates

## Allowlist Strategy

Allowlists are used when a legitimate domain is blocked by mistake.

Allowlist changes should be treated carefully because they reduce filtering coverage.

Before allowing a domain:

1. Identify the blocked domain.
2. Confirm the domain is required.
3. Check whether the domain is related to a trusted service.
4. Add the domain to allowlist if justified.
5. Retest the affected application or website.
6. Document the reason for the allowlist entry.

## Security Value

This design provides practical DNS-layer security value by:

- Making DNS activity visible
- Reducing unwanted third-party lookups
- Helping identify unusual client behaviour
- Providing a first-level filtering control
- Supporting incident investigation
- Improving awareness of network activity

## Limitations

Pi-hole is not a full security gateway, firewall, EDR, IDS, or SIEM.

It does not inspect encrypted traffic content and does not replace endpoint security tools.

Its role is DNS-layer visibility and domain filtering.

## Operational Considerations

DNS is a critical network dependency. If Pi-hole becomes unavailable, clients may fail to resolve domain names.

Operational considerations include:

- Monitoring Pi-hole service health
- Keeping backup configuration available
- Documenting restore procedure
- Having a fallback DNS plan
- Reviewing false positives
- Avoiding publication of raw DNS query logs

## Privacy Considerations

DNS logs can reveal user behaviour and browsing patterns.

For this reason:

- Raw query logs are not published
- Screenshots must be sanitized
- Client names and IP addresses should be hidden
- Sensitive domains should be removed from evidence
- Log retention should be reviewed periodically

## Future Improvements

Potential improvements include:

- Secondary Pi-hole instance for high availability
- Prometheus and Grafana integration
- Automated backup to NAS
- Alerting for DNS service failure
- Firewall rule to enforce DNS usage through Pi-hole
- Periodic blocklist review process
