# Evidence: Pi-hole Backup Export

## Purpose

This evidence shows that Pi-hole configuration backup process exists using Pi-hole Teleporter.

The actual backup file is not committed to this public repository because it may contain sensitive configuration details.

## Validation Date

Date: <YYYY-MM-DD>

## Backup Objective

Confirm that Pi-hole configuration can be exported for recovery purposes.

## Backup Method

Recommended method:

Pi-hole Dashboard -> Settings -> Teleporter -> Backup

## Backup Scope

The backup may include:

- Pi-hole configuration
- Blocklists
- Allowlists
- Custom DNS records
- Group configuration
- DHCP settings if used
- Local DNS entries if used

## Sanitized Result

Result: PASS

Observed behaviour:

- Pi-hole dashboard was accessible
- Teleporter backup option was available
- Configuration export was generated
- Backup file was stored outside the public repository
- No backup file was committed to GitHub

## Security Decision

The Teleporter backup file is intentionally excluded from this repository.

Reason:

- It may contain sensitive configuration
- It may expose internal DNS settings
- It may reveal blocklists, allowlists, or local DNS records
- It is not required for public portfolio evidence

## Validation Checklist

- Backup process identified
- Backup export tested
- Backup file stored securely
- Backup file excluded from GitHub
- Restore procedure documented
- Public evidence sanitized

## Related Documents

- docs/backup-and-restore.md
- runbooks/restore-pihole-backup.md

## Notes

This evidence confirms that backup planning exists for the Pi-hole DNS security service.

Actual backup files should be stored privately and securely.
