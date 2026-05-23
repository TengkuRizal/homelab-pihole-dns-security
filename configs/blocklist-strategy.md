# Blocklist Strategy

## Purpose

This document describes the blocklist strategy for the Pi-hole DNS security service.

Blocklists are used to reduce unwanted DNS lookups such as advertising, tracking, telemetry, and other low-value domains.

## Strategy

The blocklist approach should be controlled and conservative.

The goal is to improve DNS filtering without causing unnecessary false positives or breaking legitimate services.

## Selection Criteria

A blocklist should be selected based on:

- Reputation of the maintainer
- Update frequency
- Clear purpose
- Low false-positive rate
- Compatibility with Pi-hole
- Relevance to homelab use

## Change Process

Before adding a new blocklist:

1. Review the source and purpose of the list.
2. Confirm that the list is maintained.
3. Add the list to Pi-hole.
4. Update gravity.
5. Test common websites and applications.
6. Monitor for false positives.
7. Document the reason for using the list.

## Validation Commands

Use these commands during validation:

- pihole -g
- pihole status
- dig google.com @<PIHOLE_IP>
- nslookup google.com <PIHOLE_IP>

## False Positive Handling

If a legitimate domain is blocked:

1. Identify the blocked domain.
2. Confirm which blocklist caused the block.
3. Validate whether the domain is required.
4. Add to allowlist only if justified.
5. Retest the affected service.
6. Document the reason.

## Public Repository Safety

Do not publish:

- Raw query logs
- Sensitive blocked domains
- Client-specific browsing patterns
- Unsanitized dashboard screenshots

## Future Improvements

- Document approved blocklists
- Review blocklists monthly
- Track false-positive cases
- Create allowlist decision log
- Test blocklist impact before applying major changes
