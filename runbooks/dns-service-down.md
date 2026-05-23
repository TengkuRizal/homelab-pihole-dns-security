# Runbook: DNS Service Down

## Purpose

This runbook provides troubleshooting and recovery steps when the Pi-hole DNS service is unavailable or clients cannot resolve domain names.

DNS is a critical dependency. If Pi-hole is down and clients depend on it as the primary DNS resolver, internet access may appear unavailable even when the network connection is working.

## Symptoms

- Clients cannot browse websites
- `nslookup` or `dig` fails
- Pi-hole dashboard is unavailable
- DNS queries are not showing in Pi-hole dashboard
- Clients can ping IP addresses but cannot resolve domain names

## Initial Checks

Check whether the Raspberry Pi is reachable:

```bash
ping <PIHOLE_IP>
```

Check SSH access:

```bash
ssh <PI_USER>@<PIHOLE_IP>
```

Check Pi-hole status:

```bash
pihole status
```

Check Pi-hole FTL service:

```bash
sudo systemctl status pihole-FTL
```

Check DNS resolution directly against Pi-hole:

```bash
dig google.com @<PIHOLE_IP>
nslookup google.com <PIHOLE_IP>
```

## Recovery Steps

Restart Pi-hole DNS service:

```bash
pihole restartdns
```

Restart FTL if required:

```bash
sudo systemctl restart pihole-FTL
```

Verify service status:

```bash
sudo systemctl status pihole-FTL
pihole status
```

Retest DNS resolution:

```bash
dig google.com @<PIHOLE_IP>
nslookup google.com <PIHOLE_IP>
```

## If Raspberry Pi Is Unreachable

1. Confirm the device has power.
2. Confirm network cable or Wi-Fi connectivity.
3. Check router DHCP lease table.
4. Reboot the Raspberry Pi if required.
5. Confirm the Pi-hole IP address has not changed.

## Temporary Fallback

If Pi-hole cannot be restored quickly, temporarily configure router DHCP DNS to use a fallback DNS resolver.

After Pi-hole is restored, revert DHCP DNS back to Pi-hole to maintain DNS visibility and filtering.

## Validation

After recovery, confirm:

- Pi-hole dashboard is accessible
- DNS queries are visible in the dashboard
- Clients can resolve common domains
- Blocked test domain is blocked
- Allowed domain resolves successfully

## Post-Incident Notes

Document the following after recovery:

- What failed
- Time issue started
- Time service recovered
- Root cause if known
- Commands used
- Whether fallback DNS was enabled
- Preventive action

## Preventive Improvements

- Add monitoring for Pi-hole service health
- Add alerting when DNS resolution fails
- Schedule regular Pi-hole configuration backup
- Deploy secondary Pi-hole for high availability
- Test restore procedure periodically
