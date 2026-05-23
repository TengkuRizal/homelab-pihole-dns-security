# Backup and Restore

## Purpose

This document describes the backup and restore approach for the Pi-hole DNS security service.

The goal is to ensure Pi-hole configuration can be recovered if the Raspberry Pi fails, the SD card is corrupted, or the Pi-hole service needs to be migrated to new hardware.

## Why Backup Matters

Pi-hole is part of the DNS path for selected homelab clients. If configuration is lost, DNS filtering, allowlists, blocklists, and custom settings may need to be rebuilt manually.

A documented backup and restore process helps reduce recovery time and operational risk.

## Backup Scope

The backup should include:

- Pi-hole configuration
- Blocklists
- Allowlists
- Custom DNS records
- DHCP settings if used
- Local DNS entries
- Group management settings if used
- Important operational notes

## Recommended Backup Method

Use Pi-hole Teleporter to export the Pi-hole configuration.

The Teleporter export can be generated from the Pi-hole web interface.

Recommended path:

```text
Pi-hole Dashboard
  -> Settings
  -> Teleporter
  -> Backup
```

The exported file should be stored securely.

## Backup Storage

Backup files should not be committed to this public GitHub repository if they contain sensitive information.

Recommended backup locations:

- Local admin workstation
- Encrypted external drive
- NAS storage
- Private backup folder
- Password manager secure file storage if supported

## Backup Frequency

Recommended backup schedule:

| Scenario | Action |
|---|---|
| Before major Pi-hole change | Export backup |
| After blocklist change | Export backup |
| After allowlist change | Export backup |
| After custom DNS change | Export backup |
| Monthly baseline | Export backup |
| Before Raspberry Pi maintenance | Export backup |

## Restore Scenario

Restore may be required when:

- Raspberry Pi SD card fails
- Pi-hole configuration is corrupted
- Pi-hole is migrated to new hardware
- Pi-hole is reinstalled
- A major configuration mistake occurs
- Blocklists or allowlists need to be recovered

## Restore Procedure

1. Install Pi-hole on the target device.
2. Access the Pi-hole dashboard.
3. Open Teleporter restore.
4. Upload the previous Teleporter backup file.
5. Restore configuration.
6. Restart DNS service if required.
7. Validate DNS resolution.
8. Validate blocklist and allowlist behaviour.

## Validation After Restore

After restore, confirm:

- Pi-hole dashboard is accessible
- DNS service is running
- Clients can resolve domains
- Blocklists are restored
- Allowlists are restored
- Custom DNS records are restored
- DNS queries appear in the dashboard
- Router or DHCP points clients to Pi-hole

Useful validation commands:

```bash
pihole status
```

```bash
sudo systemctl status pihole-FTL
```

```bash
dig google.com @<PIHOLE_IP>
```

```bash
nslookup google.com <PIHOLE_IP>
```

## Recovery Objective

Target recovery objective for homelab use:

| Metric | Target |
|---|---|
| Recovery Time Objective | Restore DNS service within 30 to 60 minutes |
| Recovery Point Objective | Last known good Pi-hole backup |
| Priority | High, because DNS affects client access |

## Public Repository Safety

Do not publish:

- Teleporter backup files
- Raw DNS logs
- Client hostnames
- MAC addresses
- Private IP mapping
- Sensitive domains
- Passwords or tokens
- Unsanitized screenshots

## Future Improvements

- Automate encrypted backup to NAS
- Schedule monthly backup reminder
- Test restore on spare Raspberry Pi or VM
- Deploy secondary Pi-hole for high availability
- Document backup retention policy
- Add monitoring for backup age
