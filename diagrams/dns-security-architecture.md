# DNS Security Architecture Diagram

## Purpose

This diagram shows how Pi-hole fits into the broader DevSecOps homelab as the DNS security and filtering layer.

Pi-hole is not the main compute platform. It supports the homelab by providing centralized DNS filtering, query visibility, and domain-level control.

## Current Architecture

```mermaid
flowchart TD
    A[Homelab Client Devices] -->|DNS Query TCP/UDP 53| B[Pi-hole on Raspberry Pi]

    B -->|Allowed DNS Query| C[Upstream DNS Resolver]
    C -->|DNS Response| B
    B -->|DNS Response| A

    B -->|Blocked Domain| D[Pi-hole Blocklist Sinkhole]

    E[Router / DHCP] -->|Assigns Pi-hole as DNS| A

    F[Admin Workstation] -->|Internal Admin Access| B

    B --> G[Query Visibility]
    B --> H[Blocklist / Allowlist Control]
    B --> I[DNS Filtering Policy]
```

## Homelab Context

```mermaid
flowchart LR
    A[DevSecOps Homelab] --> B[Virtualization / Proxmox]
    A --> C[Kubernetes Lab]
    A --> D[GitLab CI/CD]
    A --> E[Monitoring Stack]
    A --> F[Security Tools]
    A --> G[Pi-hole DNS Security Layer]

    G --> G1[DNS Filtering]
    G --> G2[Query Visibility]
    G --> G3[Domain Blocking]
    G --> G4[Operational Runbooks]
```

## Failure Scenario

```mermaid
flowchart TD
    A[Client Device] -->|DNS Query| B[Pi-hole]

    B -->|Healthy| C[Domain Resolution Works]
    B -->|Service Down| D[DNS Resolution Fails]

    D --> E[Run DNS Service Down Runbook]
    E --> F[Restart Pi-hole DNS Service]
    E --> G[Check Raspberry Pi Network]
    E --> H[Temporary Fallback DNS if Needed]

    F --> I[Validate DNS Resolution]
    G --> I
    H --> I
```

## Future Improvement: Secondary Pi-hole

```mermaid
flowchart TD
    A[Client Devices] -->|Primary DNS| B[Primary Pi-hole]
    A -->|Secondary DNS| C[Secondary Pi-hole]

    B --> D[Upstream DNS Resolver]
    C --> D

    B --> E[Primary DNS Filtering]
    C --> F[Failover DNS Filtering]

    G[Monitoring] --> B
    G --> C
```

## Safety Notes

This diagram intentionally uses generic labels.

It does not expose:

- Real IP addresses
- Client hostnames
- MAC addresses
- VLAN IDs
- Sensitive internal network details
- Full home network topology
