---
name: renewal-report
description: Build a client renewal report from the user's TLDix account - every domain, hosting plan and licence that renews in a chosen window, grouped and prioritised, with gaps in alerts flagged and optional reminder drafts. Use when the user asks what renews soon, wants a monthly renewal review, an invoice plan, or reminders to send to clients.
---

# Renewal report

Turn the user's TLDix list into a report they can act on this week.

## Steps

1. Ask for the window only if the user did not give one. Default to 60 days.
2. Call `list_upcoming_renewals` with that window and `type: "all"`. If the user asked about one kind of item, pass `domain`, `hosting` or `license` instead.
3. Call `list_tracked_domains` only when you need alert days or registrars that the renewals list does not show.
4. Build the report:
   - **Overdue or expiring in 7 days** first, then 8-30 days, then the rest of the window.
   - One table per group with: item, type, renewal date, days left, registrar or provider, and the client or reference code when TLDix has one.
   - Under the tables, a short "Needs attention" list: items already expired, domains whose next alert comes after it would be useful (for example only a 1-day alert left), and several renewals at the same registrar that could be handled together.
5. Close with totals per group. Do not invent prices or invoice amounts; TLDix does not store them.

## Reminder drafts

If the user asks for client reminders, draft one short message per client (or per item when there is no client), stating what renews, the date, and what the user needs from the client. Leave sending to the user.

## Rules

- Only report what the tools return. If a tool needs the user to sign in, say so and stop until they connect.
- Do not add or remove items while building a report. Offer it as a next step instead.
- Dates are YYYY-MM-DD from TLDix; keep them as returned.
