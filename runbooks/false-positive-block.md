# Runbook: False Positive Block

## Purpose

This runbook describes how to investigate and resolve a false positive DNS block in Pi-hole.

A false positive happens when Pi-hole blocks a legitimate domain that is required for a website, application, or service to work properly.

## Symptoms

Common symptoms include:

- Website does not load correctly
- Login page fails to load
- Images, scripts, or buttons are missing
- Mobile application cannot connect
- Payment, authentication, or API call fails
- User reports that a trusted service is broken

## Initial Checks

Confirm the issue is related to DNS filtering:

1. Identify the affected website or application.
2. Check whether the issue affects one client or multiple clients.
3. Review Pi-hole query log for blocked domains.
4. Identify the blocked domain.
5. Confirm whether the domain is required by the affected service.

## Investigation Steps

Use the Pi-hole dashboard to review recent blocked queries.

Check:

- Client device involved
- Blocked domain
- Time of block
- Blocklist source
- Frequency of the blocked request
- Whether the domain is related to the affected application

## Decision Criteria

Only allowlist the domain if:

- The domain is required for a legitimate service
- The domain is related to a trusted provider
- The impact is confirmed
- The domain is not suspicious
- The fix has been tested after allowlisting

Do not allowlist a domain just because it appears frequently.

## Resolution Steps

1. Identify the blocked domain.
2. Confirm the domain is required.
3. Add the domain to the Pi-hole allowlist.
4. Retest the affected website or application.
5. Confirm the issue is resolved.
6. Document the allowlist decision.
7. Monitor for repeated issues.

## Validation

After allowlisting, confirm:

- The affected website or app works
- DNS resolution succeeds
- No unrelated domains were allowlisted
- Pi-hole filtering remains active
- The allowlist entry is documented

## Documentation Notes

Record the following:

- Date
- Affected service
- Blocked domain
- Reason for allowlisting
- Validation result
- Whether the issue was caused by a specific blocklist

## Rollback

If the allowlisted domain is later found to be unnecessary or risky:

1. Remove the domain from allowlist.
2. Update Pi-hole gravity if required.
3. Retest the affected service.
4. Document the rollback reason.

## Public Repository Safety

Do not publish:

- Raw query logs
- User browsing activity
- Sensitive domains
- Client hostnames
- MAC addresses
- Unsanitized screenshots

## Preventive Improvements

- Review blocklists before adding new ones
- Avoid overly aggressive blocklists
- Maintain sanitized allowlist decision log
- Review allowlist entries monthly
- Document repeated false positive cases
