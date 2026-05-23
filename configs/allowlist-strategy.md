# Allowlist Strategy

## Purpose

This document describes the allowlist strategy for the Pi-hole DNS security service.

Allowlists are used when legitimate domains are blocked by Pi-hole and need to be allowed for normal application or website functionality.

## Strategy

The allowlist approach should be careful and controlled.

Adding a domain to the allowlist reduces filtering coverage, so every allowlist decision should have a clear reason.

## When to Allowlist

A domain may be added to the allowlist when:

- A legitimate website fails to load
- A trusted application cannot function
- A required service is blocked by mistake
- A business-critical or lab-critical domain is affected
- The domain is confirmed as safe and required

## Review Process

Before adding a domain to the allowlist:

1. Identify the blocked domain.
2. Confirm which client is affected.
3. Confirm what application or website requires the domain.
4. Check whether the domain is trusted.
5. Add the domain to the allowlist only if justified.
6. Retest the affected service.
7. Document the reason for the allowlist decision.

## Validation Commands

Use these commands during validation:

- pihole status
- pihole -q example.com
- dig example.com @<PIHOLE_IP>
- nslookup example.com <PIHOLE_IP>

## Documentation Standard

Each allowlist decision should record:

- Domain name
- Reason for allowlisting
- Date added
- Service or application affected
- Validation result
- Reviewer or owner

## Risks

Poor allowlist management can create risk.

Possible risks include:

- Allowing tracking domains unnecessarily
- Reducing DNS filtering effectiveness
- Hiding suspicious client behaviour
- Creating inconsistent filtering policy
- Making troubleshooting harder later

## Public Repository Safety

Do not publish:

- Sensitive domains
- Internal client names
- Raw query logs
- Private browsing patterns
- Unsanitized screenshots

## Future Improvements

- Maintain sanitized allowlist decision log
- Review allowlist entries monthly
- Remove unused allowlist entries
- Categorize allowlist entries by application
- Document false-positive examples
