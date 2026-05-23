# Homelab Pi-hole DNS Security

This project documents a production-style DNS security and filtering layer using Pi-hole running on a Raspberry Pi within a homelab environment.

The objective is to provide centralized DNS filtering, DNS query visibility, unwanted domain blocking, and operational documentation for a critical internal network service.

Although this is a homelab deployment, the project is documented using SRE and DevSecOps practices including architecture design, security controls, monitoring, backup and restore, risk assessment, and incident response runbooks.

## Objectives

- Provide centralized DNS filtering for homelab clients
- Improve DNS query visibility for troubleshooting and security review
- Block known advertising, tracking, telemetry, and unwanted domains
- Reduce unnecessary outbound DNS traffic
- Treat DNS as a critical internal network dependency
- Document backup, restore, and failure recovery procedures
- Build operational evidence suitable for DevOps, DevSecOps, and SRE portfolio review

## Architecture Summary

Client devices in the homelab network send DNS queries to Pi-hole running on Raspberry Pi.

Pi-hole evaluates each query against configured blocklists and allowlists. Allowed queries are forwarded to configured upstream DNS resolvers, while blocked domains are sinkholed by Pi-hole.

```text
Client Devices
     |
     | DNS Query :53
     v
Pi-hole on Raspberry Pi
     |
     | Allowed Queries
     v
Upstream DNS Resolver
     |
     v
Internet

Blocked Domains
     |
     v
Pi-hole Blocklist / Sinkhole
```

## Technology Stack

| Component | Purpose |
|---|---|
| Raspberry Pi | Lightweight DNS security host |
| Pi-hole | DNS filtering and query visibility |
| Linux | Operating system layer |
| Router / DHCP | Client DNS assignment |
| Blocklists | Domain filtering control |
| Runbooks | Operational recovery procedures |
| GitHub | Documentation and portfolio evidence |

## Security Controls

This project focuses on practical DNS-layer security controls:

- Centralized DNS resolution through Pi-hole
- Domain blocking using curated blocklists
- Allowlist process for false-positive handling
- Local-only administrative access
- Sanitized evidence and screenshots
- Backup and restore procedure
- Operational documentation for DNS failure scenarios

## Operational Scope

This repository does not publish raw DNS query logs, private client information, passwords, tokens, MAC addresses, or sensitive internal network details.

All screenshots, configuration examples, and evidence are sanitized before being added to the repository.

## Documentation

| Document | Description |
|---|---|
| [Architecture](docs/architecture.md) | High-level DNS security architecture |
| [DNS Security Design](docs/dns-security-design.md) | DNS filtering and security role |
| [Network Flow](docs/network-flow.md) | DNS query flow and forwarding path |
| [Security Hardening](docs/security-hardening.md) | Hardening controls for Pi-hole and Raspberry Pi |
| [Monitoring and Alerting](docs/monitoring-and-alerting.md) | Health checks and availability monitoring |
| [Backup and Restore](docs/backup-and-restore.md) | Recovery process for Pi-hole configuration |
| [Risks and Tradeoffs](docs/risk-and-tradeoffs.md) | Known limitations and mitigation plan |
| [Lessons Learned](docs/lessons-learned.md) | Operational lessons from running DNS filtering |

## Runbooks

| Runbook | Purpose |
|---|---|
| [DNS Service Down](runbooks/dns-service-down.md) | Recovery steps when DNS service is unavailable |
| [Client Cannot Resolve Domain](runbooks/client-cannot-resolve-domain.md) | Troubleshooting client DNS resolution issues |
| [False Positive Block](runbooks/false-positive-block.md) | Handling legitimate domains blocked by Pi-hole |
| [Restore Pi-hole Backup](runbooks/restore-pihole-backup.md) | Restore procedure after failure or migration |

## Evidence

Evidence is added in sanitized form only.

| Evidence | Purpose |
|---|---|
| [Service Status](evidence/service-status-sanitized.md) | Shows Pi-hole DNS service status |
| [DNS Resolution Test](evidence/dns-resolution-test-sanitized.md) | Shows allowed domain resolution works |
| [Blocked Domain Test](evidence/blocked-domain-test-sanitized.md) | Shows DNS filtering is active |
| [Backup Export](evidence/backup-export-sanitized.md) | Shows backup process exists |

Evidence rules:

- No raw DNS query logs
- No real client hostnames
- No MAC addresses
- No sensitive domains
- No passwords or tokens
- No unsanitized screenshots

## Future Improvements

- Deploy a secondary Pi-hole instance for high availability
- Add automated backup to NAS or external storage
- Integrate Pi-hole metrics with Prometheus and Grafana
- Add alerting for DNS service failure
- Enforce DNS usage through firewall rules
- Test client behaviour during Pi-hole outage
- Document recovery time objective and recovery point objective

## Portfolio Positioning

This project demonstrates practical understanding of DNS security, network visibility, operational reliability, backup and restore planning, and incident response documentation.

The goal is not only to run Pi-hole, but to operate it as a critical DNS security service with production-style documentation.
