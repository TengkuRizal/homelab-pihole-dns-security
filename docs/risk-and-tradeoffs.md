# Risks and Tradeoffs

## Purpose

This document describes the main risks and tradeoffs of running Pi-hole as a DNS security and filtering service in a homelab environment.

The goal is to show operational awareness, not just installation.

## Key Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Single Pi-hole instance | DNS may fail if Raspberry Pi is down | Backup, restore runbook, future secondary Pi-hole |
| Raspberry Pi hardware failure | DNS filtering becomes unavailable | Keep Teleporter backup and recovery notes |
| SD card corruption | Pi-hole configuration may be lost | Regular backup and restore testing |
| False positive blocking | Legitimate sites or apps may break | Allowlist review process |
| Aggressive blocklists | User disruption and troubleshooting noise | Use reputable lists and validate changes |
| Raw DNS log exposure | Privacy risk | Do not publish raw logs or unsanitized screenshots |
| Client bypassing Pi-hole | Reduced visibility and filtering | Future firewall rule to enforce DNS through Pi-hole |
| Upstream DNS issue | Allowed queries may fail | Use reliable upstream DNS and fallback plan |

## Single Point of Failure

The current design uses one Raspberry Pi running Pi-hole.

This is simple and cost-effective, but it introduces a single point of failure. If the device is unavailable, clients relying only on Pi-hole may fail to resolve domains.

Mitigation:

- Maintain Pi-hole configuration backup
- Document restore procedure
- Keep DNS service down runbook
- Consider temporary fallback DNS
- Plan secondary Pi-hole for high availability

## Privacy Tradeoff

Pi-hole provides DNS visibility, but DNS logs can reveal browsing behaviour and client activity.

Mitigation:

- Do not publish raw query logs
- Sanitize screenshots
- Hide client names and IP addresses
- Review log retention
- Limit dashboard access to trusted users

## Security Tradeoff

Pi-hole improves DNS-layer visibility and filtering, but it is not a full security platform.

It does not replace:

- Firewall
- Endpoint detection and response
- SIEM
- IDS or IPS
- Malware analysis platform
- Secure web gateway

Pi-hole should be treated as one control in a wider security architecture.

## Operational Tradeoff

More blocklists can improve filtering coverage, but they can also increase false positives.

Mitigation:

- Add blocklists gradually
- Validate important services after changes
- Keep allowlist process documented
- Review blocklist quality periodically

## Future Improvements

- Deploy secondary Pi-hole
- Add automated backup to NAS
- Add DNS service monitoring
- Enforce DNS through firewall rules
- Add Prometheus and Grafana dashboard
- Test failure and restore scenarios
