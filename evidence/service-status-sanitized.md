# Evidence: Pi-hole Service Status

## Purpose

This evidence shows that Pi-hole DNS service is running on Raspberry Pi.

Sensitive values such as real hostname, IP address, and user information are sanitized.

## Validation Date

Date: <YYYY-MM-DD>

## Pi-hole Status Check

Command used:

pihole status

Expected result:

- Pi-hole blocking is enabled
- DNS service is running
- FTL service is running

Sanitized output:

```text
[✓] FTL is listening on port 53
[✓] UDP 53 is in use by pihole-FTL
[✓] TCP 53 is in use by pihole-FTL
[✓] Pi-hole blocking is enabled

