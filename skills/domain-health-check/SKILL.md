---
name: domain-health-check
description: Check a list of domains for expiry and SSL problems with TLDix - registration expiry, registrar, lock status and the TLS certificate each site serves - and summarise the risks. Works without a TLDix account. Use when the user pastes domains to audit, onboards a new client, or asks whether sites are about to expire or have SSL issues.
---

# Domain health check

Audit up to 25 domains at a time and return a short risk summary.

## Steps

1. Collect the domains from the user's message. Strip `https://`, paths and `www.`; keep each registrable domain once.
2. Call `check_domain_expiries` with the list (25 per call; batch larger lists). Re-check any domain marked `pending` once.
3. For each domain that resolves to a website, call `check_ssl_certificate`. Skip SSL for domains that are not registered.
4. Call `lookup_domain` only for domains where you need status codes or nameservers to explain a problem.
5. Report:
   - A table: domain, expiry date, days left, registrar, SSL valid until, SSL days left, status.
   - **Risks**, most urgent first: domain expiring within 30 days, SSL expiring within 14 days, certificate that does not cover the name, missing `clientTransferProhibited` lock, domain not registered.
   - **All clear** list for the rest, in one line.

## Next step

If the user has TLDix connected, offer to add the domains that are not tracked yet with `add_domain`. Ask before adding, and use the alert days they choose (default 60, 30, 14, 7, 3, 1).

## Rules

- Lookups may be cached for up to 48 hours; mention this if a recent renewal does not show.
- Do not guess expiry dates for domains the tools could not check. List them as "could not check".
