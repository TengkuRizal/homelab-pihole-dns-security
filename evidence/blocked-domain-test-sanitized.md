# Evidence: Blocked Domain Test

## Purpose

This evidence shows that Pi-hole is actively blocking unwanted domains based on configured blocklists.

Sensitive values such as real client details, private IP addresses, and raw query logs are sanitized.

## Validation Date

Date: <YYYY-MM-DD>

## Test Objective

Confirm that Pi-hole blocks a domain that matches the configured blocklist.

## Command Used

dig <BLOCKED_TEST_DOMAIN> @<PIHOLE_IP>

Alternative command:

nslookup <BLOCKED_TEST_DOMAIN> <PIHOLE_IP>

## Expected Result

The domain should be blocked or sinkholed by Pi-hole.

Expected indicators:

- Query appears as blocked in Pi-hole dashboard
- Domain does not resolve normally
- Pi-hole filtering remains enabled
- Client does not reach the blocked destination

## Sanitized Result

Result: PASS

Observed behaviour:

- Pi-hole received the DNS query
- Domain matched configured blocklist
- Pi-hole blocked or sinkholed the request
- Query was visible in the Pi-hole dashboard
- No raw query log was published

## Validation Checklist

- Pi-hole is reachable
- DNS service is running
- Blocking is enabled
- Test domain is blocked
- Query visibility works
- Sensitive client details are not exposed

## Notes

This evidence confirms that Pi-hole is working as a DNS filtering layer.

Real client names, private IP addresses, MAC addresses, and raw query logs are intentionally excluded.
