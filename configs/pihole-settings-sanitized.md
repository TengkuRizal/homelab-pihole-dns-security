# Pi-hole Settings Sanitized

## Purpose

This document records sanitized Pi-hole configuration notes for portfolio and operational documentation.

Sensitive values are intentionally excluded or replaced with placeholders.

## Deployment Summary

| Item | Value |
|---|---|
| Platform | Raspberry Pi |
| Service | Pi-hole |
| Role | DNS filtering and query visibility |
| Network Scope | Homelab clients |
| Admin Access | Internal network only |
| Public Exposure | No |

## Sanitized Network Settings

| Setting | Sanitized Value |
|---|---|
| Pi-hole IP Address | <PIHOLE_IP> |
| Gateway | <GATEWAY_IP> |
| DNS Port | 53 |
| Admin Interface | Internal access only |
| Upstream DNS | Documented separately |
| DHCP Mode | Router-managed or Pi-hole-managed, depending on deployment |

## Core Settings

Recommended baseline:

- Pi-hole used as primary DNS resolver for selected clients
- Web dashboard restricted to trusted internal network
- Query logging reviewed carefully due to privacy sensitivity
- Blocklists managed using controlled change process
- Allowlists reviewed before approval
- Teleporter backup created after major changes

## DNS Behaviour

Expected DNS behaviour:

- Clients send DNS queries to Pi-hole
- Pi-hole checks blocklists and allowlists
- Allowed domains are forwarded to upstream DNS
- Blocked domains are sinkholed
- Query visibility is available from dashboard

## Privacy and Sanitization

Do not publish:

- Real client hostnames
- MAC addresses
- Raw DNS query logs
- Sensitive domains
- Real private IP mapping
- Passwords
- Tokens
- Unsanitized screenshots

## Operational Notes

Important operational notes:

- DNS is a critical service
- Backup should be created before major changes
- Blocklist changes should be validated
- False positives should be documented
- Pi-hole outage should follow DNS service down runbook
- Router DHCP DNS setting should be documented privately

## Evidence Allowed in Public Repo

Safe evidence examples:

- Sanitized dashboard screenshot
- Pi-hole service status output
- DNS resolution test output with placeholders
- Blocked domain test using non-sensitive test domain
- Sanitized architecture diagram

## Future Improvements

- Add secondary Pi-hole
- Add monitoring integration
- Add automated backup
- Add DNS failover testing
- Add sanitized configuration screenshots

