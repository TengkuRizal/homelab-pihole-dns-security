# Runbook: Restore Pi-hole Backup

## Purpose

This runbook describes how to restore Pi-hole configuration from a backup.

This procedure is used when Pi-hole configuration is lost, corrupted, migrated to new hardware, or rebuilt after Raspberry Pi failure.

## When to Use This Runbook

Use this runbook when:

- Raspberry Pi SD card fails
- Pi-hole is reinstalled
- Pi-hole is migrated to new hardware
- Blocklist or allowlist configuration is lost
- Configuration is corrupted
- A previous known-good configuration needs to be restored

## Prerequisites

Before restore, confirm:

- Target device is powered on
- Target device has network connectivity
- Pi-hole is installed
- Pi-hole dashboard is reachable
- Backup file is available
- Backup file is from a trusted source
- Admin access is available

## Restore Method

Pi-hole Teleporter is the recommended restore method.

General restore path:

Pi-hole Dashboard -> Settings -> Teleporter -> Restore

## Restore Steps

1. Access the Pi-hole dashboard.
2. Go to Settings.
3. Open Teleporter.
4. Select the backup file.
5. Restore the configuration.
6. Restart DNS service if required.
7. Validate Pi-hole status.
8. Validate DNS resolution.
9. Confirm blocklists and allowlists are restored.
10. Confirm clients are using Pi-hole as DNS resolver.

## Validation Commands

Use these commands after restore:

- pihole status
- sudo systemctl status pihole-FTL
- dig google.com @<PIHOLE_IP>
- nslookup google.com <PIHOLE_IP>

## Validation Checklist

After restore, confirm:

- Pi-hole dashboard is accessible
- Pi-hole DNS service is running
- Clients can resolve common domains
- Blocked domains are still blocked
- Allowed domains resolve successfully
- Blocklists are restored
- Allowlists are restored
- Custom DNS records are restored if used
- Query visibility works
- Router DHCP DNS setting points to Pi-hole

## Rollback Plan

If restore causes issues:

1. Record the issue.
2. Restore a previous known-good backup if available.
3. Reinstall Pi-hole if required.
4. Temporarily use fallback DNS to restore client connectivity.
5. Reapply configuration carefully.
6. Validate again.

## Public Repository Safety

Do not publish:

- Teleporter backup files
- Raw configuration exports
- Passwords
- Tokens
- Client hostnames
- MAC addresses
- Sensitive domains
- Raw DNS logs
- Unsanitized screenshots

## Post-Restore Notes

Document:

- Restore date
- Reason for restore
- Backup version used
- Validation result
- Any issue encountered
- Recovery time
- Follow-up action

## Future Improvements

- Test restore procedure periodically
- Store encrypted backup on NAS
- Automate backup reminders
- Document backup retention policy
- Deploy secondary Pi-hole for faster recovery
