# Monitoring and Alerting

## Purpose

This document describes the monitoring and alerting approach for the Pi-hole DNS security service.

The goal is to ensure DNS service availability, detect service failure early, and provide basic operational visibility for a critical homelab network dependency.

## Why Monitoring Matters

DNS is a critical service. If Pi-hole is unavailable, clients may fail to resolve domain names even when internet connectivity is working.

Monitoring helps identify:

- Pi-hole service failure
- Raspberry Pi availability issue
- DNS resolution failure
- Dashboard access issue
- Unexpected DNS behaviour
- High block rate or unusual query activity

## Health Checks

Recommended health checks:

| Check | Purpose |
|---|---|
| Ping Raspberry Pi | Confirm device is reachable |
| SSH access | Confirm host access |
| Pi-hole status | Confirm Pi-hole service state |
| FTL service status | Confirm DNS engine is running |
| DNS query test | Confirm Pi-hole can resolve domains |
| Blocked domain test | Confirm filtering is active |
| Dashboard access | Confirm admin interface is reachable |

## Manual Validation Commands

Check Pi-hole status:

```bash
pihole status
```

Check FTL service:

```bash
sudo systemctl status pihole-FTL
```

Test DNS resolution:

```bash
dig google.com @<PIHOLE_IP>
```

Test using nslookup:

```bash
nslookup google.com <PIHOLE_IP>
```

Check listening ports:

```bash
sudo ss -tulpn | grep ':53'
```

Check system resource usage:

```bash
uptime
free -h
df -h
```

## Alert Conditions

Potential alert conditions:

| Condition | Severity | Action |
|---|---|---|
| Pi-hole not reachable | High | Check device power and network |
| DNS resolution fails | High | Restart DNS service and validate |
| FTL service stopped | High | Restart pihole-FTL |
| Dashboard unavailable | Medium | Check web service and host status |
| Disk space high | Medium | Clean logs or expand storage |
| CPU or memory high | Medium | Review processes and load |
| High number of blocked domains | Low | Review query activity |

## Basic Recovery Actions

If DNS fails:

1. Check Raspberry Pi connectivity.
2. Check Pi-hole status.
3. Restart DNS service.
4. Validate DNS resolution.
5. Enable temporary fallback DNS if needed.
6. Document the incident.

## Evidence to Capture

Safe evidence for GitHub:

- Sanitized dashboard screenshot
- Service status output
- DNS resolution test output
- Blocked domain test output
- Uptime check
- Sanitized monitoring screenshot

Do not publish:

- Raw DNS query logs
- Client hostnames
- MAC addresses
- Sensitive domains
- Private browsing history

## Future Improvements

- Add Prometheus exporter for Pi-hole
- Create Grafana dashboard
- Add uptime monitoring
- Add alert notification for DNS failure
- Track backup age
- Monitor Raspberry Pi CPU, memory, and disk usage
- Add synthetic DNS check from another homelab node
