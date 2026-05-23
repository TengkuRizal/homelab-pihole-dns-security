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
