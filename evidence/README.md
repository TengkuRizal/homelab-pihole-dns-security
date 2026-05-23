# Evidence

## Purpose

This folder stores sanitized evidence for the Pi-hole DNS security project.

Evidence is used to prove that the service is running, DNS resolution works, filtering is active, and operational checks have been performed.

## Evidence Rules

All evidence must be sanitized before being committed to this public repository.

Do not publish:

- Raw DNS query logs
- Real client hostnames
- MAC addresses
- Sensitive domains
- Private browsing activity
- Passwords or tokens
- Teleporter backup files
- Unsanitized dashboard screenshots
- Full internal network details

## Recommended Evidence

Safe evidence examples:

| Evidence | Purpose |
|---|---|
| Pi-hole dashboard screenshot | Show service visibility |
| Service status output | Show Pi-hole is running |
| DNS resolution test | Show allowed domain resolution works |
| Blocked domain test | Show filtering is active |
| Backup export screenshot | Show backup process exists |
| Sanitized query view | Show DNS visibility without exposing private data |

## Suggested File Names

Use clear sanitized file names:

- dashboard-sanitized.png
- service-status-sanitized.png
- dns-resolution-test-sanitized.png
- blocked-domain-test-sanitized.png
- teleporter-backup-sanitized.png
- query-visibility-sanitized.png

## Evidence Checklist

Before committing evidence, confirm:

- Screenshot is sanitized
- Client names are hidden
- Private IPs are hidden if not required
- MAC addresses are hidden
- Sensitive domains are hidden
- No password or token is visible
- No raw query log is included

## Future Evidence Plan

Planned evidence:

- Pi-hole dashboard sanitized screenshot
- pihole status output
- pihole-FTL service status output
- DNS resolution test
- Blocked domain test
- Backup export process screenshot
- Future monitoring dashboard screenshot
