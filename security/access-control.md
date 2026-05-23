# Access Control

## Purpose

This document describes access control considerations for the Pi-hole DNS security service.

The goal is to reduce the risk of unauthorized access to the Pi-hole dashboard, Raspberry Pi host, and DNS configuration.

## Access Control Objectives

Access control should ensure that:

- Pi-hole dashboard is only reachable from trusted internal network
- Raspberry Pi SSH access is limited to trusted administrator
- Strong password is used for Pi-hole admin interface
- Credentials are not stored in the public repository
- Configuration changes are performed intentionally
- Sensitive operational data is not exposed publicly

## Protected Assets

| Asset | Protection Goal |
|---|---|
| Pi-hole dashboard | Prevent unauthorized configuration changes |
| Raspberry Pi SSH access | Protect host-level access |
| Pi-hole configuration | Prevent unwanted DNS policy changes |
| DNS query data | Protect privacy and browsing visibility |
| Backup files | Prevent leakage of configuration details |

## Recommended Controls

Recommended baseline controls:

- Use strong Pi-hole admin password
- Keep dashboard accessible only from trusted LAN
- Do not expose Pi-hole admin interface to the public internet
- Restrict SSH access to trusted admin device
- Keep Raspberry Pi OS updated
- Do not commit credentials, tokens, or backup files to GitHub
- Sanitize screenshots before publishing
- Review allowlist and blocklist changes

## SSH Access

SSH access should be limited to authorized administrator only.

Recommended practices:

- Use strong user password or SSH key-based access
- Disable unused accounts
- Keep operating system updated
- Avoid exposing SSH to the internet
- Document access method privately, not in public repo

## Pi-hole Dashboard Access

Pi-hole dashboard should be treated as an administrative interface.

Recommended practices:

- Use strong admin password
- Restrict access to internal network
- Do not expose dashboard through public port forwarding
- Avoid sharing dashboard screenshots with sensitive data
- Review configuration changes carefully

## Public Repository Safety

Do not publish:

- Admin password
- SSH private key
- API token
- Teleporter backup
- Raw DNS query logs
- Client hostnames
- MAC addresses
- Sensitive domains
- Unsanitized screenshots

## Future Improvements

- Use network firewall rules to restrict dashboard access
- Add secondary admin recovery account if required
- Review SSH hardening
- Document private access procedure outside public repo
- Add monitoring for unauthorized access attempts
