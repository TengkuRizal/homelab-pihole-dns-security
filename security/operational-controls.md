# Operational Controls

## Purpose

This document describes operational controls for running Pi-hole as a DNS security and filtering service.

The goal is to make the service reliable, maintainable, and safe to document in a public portfolio repository.

## Control Objectives

Operational controls should support:

- DNS service availability
- Controlled configuration changes
- Safe blocklist and allowlist management
- Backup and restore readiness
- Monitoring and troubleshooting
- Privacy protection
- Public repository sanitization

## Change Control

Any change to Pi-hole configuration should be done carefully.

Examples of configuration changes:

- Adding blocklists
- Removing blocklists
- Adding allowlist entries
- Changing upstream DNS
- Changing DHCP or router DNS settings
- Updating Pi-hole
- Restoring from backup

Recommended change process:

1. Record the change reason.
2. Take backup before major change.
3. Apply the change.
4. Validate DNS resolution.
5. Validate blocking behaviour.
6. Monitor for false positives.
7. Document the result.

## Backup Control

Backup should be created:

- Before major configuration changes
- After important blocklist or allowlist changes
- Before Pi-hole upgrade
- Before Raspberry Pi maintenance
- On a regular schedule

Backup files should be stored securely and not committed to this public repository.

## Monitoring Control

The service should be monitored for:

- Pi-hole service status
- Raspberry Pi availability
- DNS resolution success
- Disk usage
- CPU and memory usage
- Dashboard availability
- Unusual DNS query behaviour

## Incident Control

Operational incidents should follow documented runbooks.

Example incidents:

- DNS service down
- Client cannot resolve domain
- False positive block
- Pi-hole dashboard unavailable
- Raspberry Pi unreachable

Each incident should record:

- Symptom
- Impact
- Root cause if known
- Fix applied
- Validation result
- Preventive action

## Privacy Control

DNS logs can reveal client behaviour.

Privacy controls:

- Do not publish raw query logs
- Sanitize screenshots
- Hide client hostnames
- Hide MAC addresses
- Remove sensitive domains
- Avoid publishing full internal network details

## Repository Control

This repository is public and must only contain sanitized information.

Allowed:

- Architecture diagrams without sensitive details
- Sanitized configuration notes
- Runbooks
- High-level design documents
- Safe evidence screenshots

Not allowed:

- Passwords
- Tokens
- Teleporter backup files
- Raw logs
- Client device names
- MAC addresses
- Private browsing details

## Future Improvements

- Add change log template
- Add incident report template
- Add backup schedule
- Add monitoring dashboard
- Add automated DNS health check
- Add secondary Pi-hole for resilience
