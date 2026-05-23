# Runbook: Client Cannot Resolve Domain

## Purpose

This runbook describes how to troubleshoot a client device that cannot resolve domain names when using Pi-hole as DNS resolver.

The goal is to identify whether the issue is caused by the client, network, Pi-hole, upstream DNS, or blocklist filtering.

## Symptoms

Common symptoms include:

- Client cannot browse websites
- Browser shows DNS error
- Application cannot connect
- Client can ping IP addresses but cannot access domains
- Only one device is affected
- Some domains work but others fail

## Initial Questions

Before troubleshooting, confirm:

- Is the issue affecting one client or all clients?
- Is the client using Pi-hole as DNS resolver?
- Can the client reach the router?
- Can the client reach the Pi-hole IP?
- Is the domain blocked or failing to resolve?
- Did the issue start after a blocklist or DNS change?

## Client-Side Checks

Check the client DNS server setting.

Confirm the DNS server points to Pi-hole.

Check whether the client has network connectivity.

Try reconnecting the client to the network.

Restart the client network adapter if needed.

## Pi-hole Checks

From the Pi-hole host, check:

- Pi-hole status
- pihole-FTL service status
- Recent query log
- Whether the affected client appears in query logs
- Whether the domain is blocked
- Whether upstream DNS is reachable

## DNS Resolution Test

Test common domain resolution from the affected client.

Use:

- nslookup google.com <PIHOLE_IP>
- dig google.com @<PIHOLE_IP>

If the domain resolves through Pi-hole, the issue may be client-specific.

If the domain does not resolve through Pi-hole, check Pi-hole service and upstream DNS.

## Blocklist Check

If only one domain fails:

1. Search for the domain in Pi-hole query log.
2. Confirm whether the domain is blocked.
3. Identify which list blocked the domain.
4. Decide whether allowlisting is justified.
5. Retest after allowlisting if approved.

## Scope Isolation

Use this decision guide:

| Observation | Likely Area |
|---|---|
| Only one client affected | Client DNS or network configuration |
| All clients affected | Pi-hole, router DHCP, or upstream DNS |
| Only one domain affected | Blocklist or domain-specific issue |
| IP ping works but domain fails | DNS resolution issue |
| Pi-hole dashboard unreachable | Pi-hole host or service issue |

## Recovery Steps

Possible recovery actions:

1. Renew client DHCP lease.
2. Confirm router is assigning Pi-hole as DNS.
3. Restart Pi-hole DNS service.
4. Restart pihole-FTL if needed.
5. Check upstream DNS resolver.
6. Use temporary fallback DNS only if Pi-hole cannot be restored quickly.

## Validation

After recovery, confirm:

- Client can resolve common domains
- Client appears in Pi-hole query log
- Blocked domains are still blocked
- Allowed domains resolve correctly
- No sensitive logs are exposed

## Documentation Notes

Record:

- Affected client type
- Domain affected
- Time issue started
- Root cause if known
- Fix applied
- Validation result
- Whether allowlist was changed

## Preventive Improvements

- Document router DHCP DNS settings
- Monitor Pi-hole service health
- Keep backup DNS recovery procedure
- Review blocklists before major changes
- Maintain allowlist decision log
