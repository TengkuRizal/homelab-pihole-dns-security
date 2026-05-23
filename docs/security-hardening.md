# Security Hardening

## Purpose

This document describes basic security hardening practices for the Pi-hole DNS security service running on Raspberry Pi.

The goal is to reduce unnecessary exposure, protect administrative access, and keep the DNS filtering service reliable.

## Hardening Objectives

Security hardening should focus on:

- Protecting Pi-hole dashboard access
- Securing Raspberry Pi host access
- Avoiding public exposure
- Reducing credential leakage risk
- Keeping the system updated
- Protecting DNS query privacy
- Maintaining safe public documentation

## Network Exposure

Pi-hole should only be accessible from trusted internal network.

Recommended controls:

- Do not expose Pi-hole dashboard to the public internet
- Do not port-forward Pi-hole admin interface
- Avoid exposing DNS port 53 publicly
- Restrict dashboard access to trusted LAN
- Keep management access private

## Admin Password

Pi-hole dashboard should use a strong admin password.

Recommended controls:

- Use unique password
- Do not reuse weak password
- Store password securely
- Do not commit password to GitHub
- Change password if exposure is suspected

## Raspberry Pi Host Hardening

Recommended host controls:

- Keep Raspberry Pi OS updated
- Remove unused packages
- Disable unused services
- Use strong SSH password or SSH key
- Avoid exposing SSH to public internet
- Reboot after important security updates if required
- Monitor disk usage and system health

## SSH Security

SSH should be limited to trusted administrator access.

Recommended practices:

- Use SSH key-based access where possible
- Disable unused user accounts
- Avoid default or weak passwords
- Restrict SSH to internal network
- Do not publish SSH configuration with sensitive details
- Do not commit private keys

## Pi-hole Configuration Safety

Configuration changes should be controlled.

Recommended practices:

- Backup before major changes
- Validate after changing blocklists
- Validate after changing upstream DNS
- Review allowlist entries
- Avoid aggressive blocklists without testing
- Document operational changes

## DNS Privacy

DNS query data can reveal browsing behaviour.

Privacy controls:

- Do not publish raw DNS logs
- Sanitize dashboard screenshots
- Hide client names
- Hide MAC addresses
- Remove sensitive domains
- Review log retention

## Public Repository Safety

This repository must not contain:

- Passwords
- Tokens
- SSH keys
- Teleporter backup files
- Raw DNS query logs
- Sensitive domains
- Client hostnames
- MAC addresses
- Unsanitized screenshots
- Full private network mapping

## Validation Checklist

After hardening, confirm:

- Pi-hole dashboard is not publicly exposed
- DNS service is not exposed to the internet
- Admin password is strong
- Raspberry Pi OS is updated
- SSH access is controlled
- Backups are stored outside public repository
- Screenshots are sanitized before publishing

## Future Improvements

- Add firewall rule for management access
- Add automated update review process
- Add SSH hardening checklist
- Add monitoring for service health
- Add secondary Pi-hole for resilience
- Add periodic configuration review
