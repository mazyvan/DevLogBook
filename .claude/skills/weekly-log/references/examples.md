# Weekly Log Examples

These are examples of tone, structure, and length — not templates to fill in. Every week is different. Some weeks have 3 items, some have 7. But the log always has three sections: a **Recap** (intro + numbered items), **Up Next** (what's coming), and optionally **Notes** (learnings, recognition, anything that doesn't fit an item).

All Jira tickets are linked: `[KEY-123](https://producepay.atlassian.net/browse/KEY-123)`.

## Example 1: A support-heavy week with impact framing

```markdown
# W12 — Mar 16–20

> **Monday off — Mexican holiday**

## Recap

Support-heavy week. Main focus on financing fee corrections and investigating the PIF/INVOICE_PAID flow.

1. **Financing fee correction** — [BSR-359](https://producepay.atlassian.net/browse/BSR-359). TMS was showing 1.75% instead of 1.1% on 23 trade orders. Direct SQL fix in prod. Unblocked billing for those accounts — FinOps had already confirmed the correct rate. Documented in [Confluence: BSR-359 Financing Fee Correction](link).

2. **Paid in Full / INVOICE_PAID investigation** — [POS-1355](https://producepay.atlassian.net/browse/POS-1355). Orders can't transition to INVOICE_PAID because voiding fails when fully attributed (minDue <= 0). Wrote [spike doc](link). This blocks FinOps from closing out fully paid orders — needs sync with eng before acting.

3. **Tooling improvements** — [TF-518](https://producepay.atlassian.net/browse/TF-518) (notify PR author on backport cherry-pick failure) and [TF-520](https://producepay.atlassian.net/browse/TF-520) (added to core team auto-approve). Both merged.

4. **Support & reviews** — Most of the week on support tickets and code reviews. [BSR-366](https://producepay.atlassian.net/browse/BSR-366) (change status to order) still pending.

5. **Synced with Budi** — Aligned on [VP-3774](https://producepay.atlassian.net/browse/VP-3774) (use Salesforce company for user company permission).

## Up Next

- Visibility shipments
- [VP-3774](https://producepay.atlassian.net/browse/VP-3774)

## Notes

- Recognition from manager for structured, process-oriented approach to work.
```

## Example 2: A productive week — merged is what matters

Note: tickets that just moved to Done/Closed (released to prod) but were merged in a previous week are NOT included. Only the week where the actual work happened gets the entry.

```markdown
# W11 — Mar 9–13

## Recap

Most productive week yet. AI setup matured — using Claude for everything: Jira, Confluence, Slack, DB queries, code. Six PRs merged.

1. **Pre-harvest cleanup** — [VP-3844](https://producepay.atlassian.net/browse/VP-3844). Cleaned up PRE_HARVEST_INSPECTOR role, user assignments, and code references. PR merged. Final piece of the Pre-harvest decommission — no more cost leakage from unused infra.

2. **Marketplace SKU updates** — [SM-127](https://producepay.atlassian.net/browse/SM-127) through [SM-132](https://producepay.atlassian.net/browse/SM-132). Added Frozen variety to 5 commodities and added Pears as new commodity. Requested by marketplace ops to unblock supplier onboarding. Two PRs merged.

3. **Un-fulfill orders investigation** — [TMS-2394](https://producepay.atlassian.net/browse/TMS-2394) / [BSR-366](https://producepay.atlassian.net/browse/BSR-366). Wrote [spike doc on reverting FULFILLED orders](link). Got product approval. Done.

4. **Duplicate orders bug** — [TMS-2393](https://producepay.atlassian.net/browse/TMS-2393). Duplicated order records returned by GraphQL query. Done.

5. **Tooling & AI** — [TF-518](https://producepay.atlassian.net/browse/TF-518) (backport notifications), [TF-517](https://producepay.atlassian.net/browse/TF-517) (skill-creator plugin), [TF-513](https://producepay.atlassian.net/browse/TF-513) (PostgreSQL doc updates). All merged. Created [TF-527](https://producepay.atlassian.net/browse/TF-527) epic for AI Integration Success Metrics.

6. **Wrote onboarding report** — [First 2 Weeks Back](link) covering W09-W10. Published in personal Confluence space.

## Up Next

- [BSR-359](https://producepay.atlassian.net/browse/BSR-359) financing fee correction
- Continue POS-1355 investigation
- Support rotation

## Notes

- AI workflow leveled up: now using Claude for Jira, Confluence, Slack, and DB connections. Setup is solid.
```

## Example 3: A light week (PTO + support)

```markdown
# W15 — Apr 6–10

> **Off Monday and Tuesday — personal time**

## Recap

Short week. Eased back in with support rotation.

1. **Support rotation Wed–Fri** — handled 3 BSR tickets, nothing major. [BSR-401](https://producepay.atlassian.net/browse/BSR-401) (missing shipment data) required a manual backfill — blocked the customer's weekly reconciliation report.

2. **Caught up on PRs** — reviewed 4 across tms and payments.

## Up Next

- Back to full capacity, picking up the notification system RFC.
```

## Example 4: An incident-heavy week

```markdown
# W20 — May 11–15

## Recap

Rough week. Production incident on Tuesday ate two days.

1. **Prod incident: duplicate invoice charges** — webhook retry logic was regenerating idempotency keys. Root cause was middleware ordering in the payments gateway. Affected ~150 customers, finance had to issue manual credits. Hotfix in PR #523, postmortem in [Confluence: May 12 Invoice Incident](link).

2. **Wrote RFC for idempotency key standardization** — came out of the incident. Without this, any payment-related service could hit the same bug. Proposes a shared middleware. [Confluence: RFC-041](link). Needs arch review.

3. **Node 20 deprecation in GitHub Actions** — [TF-535](https://producepay.atlassian.net/browse/TF-535). Updated 12 workflows. Merged but need to watch for breakage.

## Up Next

- Arch review for idempotency RFC
- Monitor TF-535 for CI breakage

## Notes

- Learned: never trust middleware ordering docs — read the source.
```

## What makes a good entry

- **Lead with what matters, not what the tool found.** A ticket that took 5 minutes of clicking doesn't deserve the same space as a 2-day investigation.
- **Connect the dots.** If a Jira ticket led to a Confluence doc which led to a PR, tell that story in one item — don't scatter it.
- **Always link Jira tickets.** `[KEY-123](https://producepay.atlassian.net/browse/KEY-123)` — every ticket reference gets a link.
- **Include impact on significant items.** Don't just say what was done — say who it unblocked, what it prevented, or why it was urgent. This is what makes logs useful for perf reviews.
- **Include context future-you will need.** "Fixed BSR-359" means nothing in 6 months. "Fixed financing fee on 23 orders — unblocked billing" does.
- **Merged is the milestone.** Log tickets when the PR merges (actual work done), not when they move to Done/Closed (released to prod). The QA → prod pipeline is routine and doesn't need logging unless something noteworthy happened during release.
- **Short prose is fine.** A one-line intro setting the tone for the week helps when scanning later.
- **Skip what doesn't matter.** Routine standup attendance, trivial ticket updates, recurring meetings — leave them out.
- **Notes is optional.** Only include when there's something worth recording (learnings, recognition, observations).
