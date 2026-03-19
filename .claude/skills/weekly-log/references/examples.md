# Weekly Log Examples

These are examples of tone, structure, and length — not templates to fill in. Every week is different. Some weeks have 3 items, some have 7. But the log always has three sections: a **Recap** (intro + numbered items), **Up Next** (what's coming), and optionally **Notes** (learnings, recognition, anything that doesn't fit an item).

All Jira tickets are linked: `[KEY-123](https://<your-site>.atlassian.net/browse/KEY-123)`.

## Example 1: A support-heavy week with impact framing

```markdown
# W12 — Mar 16–20

> **Monday off — public holiday**

## Recap

Support-heavy week. Main focus on data corrections and investigating a payment flow issue.

1. **Fee correction on 23 orders** — [PAY-359](link). Platform was showing 1.75% instead of 1.1%. Direct SQL fix in prod — needed to match the real billing fee. Documented in [Confluence](link).

2. **Payment status investigation** — [PAY-1355](link). Orders can't transition to final status because voiding fails under certain conditions. Wrote [spike doc](link). Blocks finance from closing out paid orders — needs sync with eng.

3. **Tooling improvements** — [TF-518](link) (backport notifications) and [TF-520](link) (auto-approve list). Both merged.

4. **Support & reviews** — Most of the week on support tickets and code reviews. [SUP-366](link) still pending.

5. **Synced with teammate on permissions work** — Aligned on [FEAT-3774](link) for next week.

## Up Next

- Shipment visibility feature
- [FEAT-3774](link)

## Notes

- Recognition from manager for structured, process-oriented approach to work.
```

## Example 2: A productive week — merged is what matters

Note: tickets that just moved to Done/Closed (released to prod) but were merged in a previous week are NOT included. Only the week where the actual work happened gets the entry.

```markdown
# W11 — Mar 9–13

## Recap

Most productive week yet. Six PRs merged. AI setup matured — using it for tickets, docs, and DB queries.

1. **Catalog updates** — [CAT-127](link) through [CAT-132](link). Added new varieties to 5 product categories and a new product. Customer-requested for their catalog. Two PRs merged.

2. **Order reversal investigation** — [ORD-2394](link) / [SUP-366](link). Wrote [spike doc](link). Requested by support — they can't set deductions on completed orders. Had to investigate whether reverting is safe. Got product approval.

3. **Duplicate records bug** — [ORD-2393](link). Duplicate records returned by API query. Done.

4. **Tooling** — [TF-518](link) (notifications), [TF-517](link) (IDE plugin), [TF-513](link) (doc updates). All merged.

5. **Wrote onboarding report** — [First 2 Weeks](link) covering W09-W10. Published in Confluence.

## Up Next

- [PAY-359](link) fee correction
- Continue payment investigation
- Support rotation
```

## Example 3: A light week (PTO + support)

```markdown
# W15 — Apr 6–10

> **Off Monday and Tuesday — personal time**

## Recap

Short week. Eased back in with support rotation.

1. **Support rotation Wed–Fri** — handled 3 tickets, nothing major. [SUP-401](link) (missing data) required a manual backfill — blocked the customer's weekly report.

2. **Caught up on PRs** — reviewed 4 across two services.

## Up Next

- Back to full capacity, picking up the notification system RFC.
```

## Example 4: An incident-heavy week

```markdown
# W20 — May 11–15

## Recap

Rough week. Production incident on Tuesday ate two days.

1. **Prod incident: duplicate charges** — Webhook retry logic was regenerating idempotency keys. Root cause was middleware ordering. Affected ~150 customers, finance had to issue manual credits. Hotfix in PR #523, postmortem in [Confluence](link).

2. **Wrote RFC for idempotency standardization** — Came out of the incident. Without this, any payment service could hit the same bug. [Confluence](link). Needs arch review.

3. **CI dependency update** — [TF-535](link). Updated 12 workflows for deprecated runtime. Merged.

## Up Next

- Arch review for idempotency RFC
- Monitor CI for breakage

## Notes

- Learned: never trust middleware ordering docs — read the source.
```

## What makes a good entry

- **Lead with what matters, not what the tool found.** A ticket that took 5 minutes doesn't deserve the same space as a 2-day investigation.
- **Connect the dots.** If a ticket led to a doc led to a PR, tell that story in one item.
- **Always link Jira tickets.** `[KEY-123](link)` — every ticket reference gets a link.
- **Include impact on significant items.** Don't just say what was done — say who it unblocked, what it prevented, or why it was urgent.
- **Include context future-you will need.** "Fixed PAY-359" means nothing in 6 months. "Fixed fee on 23 orders — matched real billing rate" does.
- **Merged is the milestone.** Log tickets when the PR merges, not when they move to Done/Closed (released to prod).
- **Short prose is fine.** A one-line intro setting the tone helps when scanning later.
- **Skip what doesn't matter.** Routine standup attendance, trivial ticket updates, recurring meetings — leave them out.
- **Notes is optional.** Only include when there's something worth recording.
