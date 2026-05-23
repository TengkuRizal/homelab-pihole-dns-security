# Evidence: DNS Resolution Test

## Purpose

This evidence shows that Pi-hole can resolve allowed domains through the configured upstream DNS resolver.

Sensitive values such as real IP address, hostname, and client details are sanitized.

## Validation Date

Date: <YYYY-MM-DD>

## Test Objective

Confirm that Pi-hole can successfully resolve a normal allowed domain.

## Command Used

dig google.com @<PIHOLE_IP>

Alternative command:

nslookup google.com <PIHOLE_IP>

## Expected Result

The domain should resolve successfully.

Expected indicators:

- DNS query returns an answer
- Query status is successful
- Response is received from Pi-hole
- No timeout occurs

## Sanitized Result

Result: PASS

Observed behaviour:

- Pi-hole received the DNS query
- Pi-hole forwarded allowed query to upstream DNS
- DNS response was returned successfully
- Client was able to resolve the domain

## Validation Checklist

- Pi-hole is reachable
- DNS service is running
- Allowed domain resolves successfully
- Query appears in Pi-hole dashboard
- No sensitive client data is published

## Notes

This evidence confirms that Pi-hole is functioning as a DNS resolver for allowed domains.

Real IP addresses, hostnames, and raw query logs are intentionally not included.
