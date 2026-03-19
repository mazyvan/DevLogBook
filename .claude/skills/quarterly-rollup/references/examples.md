# Quarterly Rollup Examples

These show the tone, structure, and level of detail. Keep it tight — the whole doc should be readable in 2-3 minutes. Only say what the weekly logs actually said. Don't embellish.

## Example 1: Partial quarter, onboarding + ramp-up

```markdown
# Q1 2026 — Weeks 9–12 (in progress)

## Overview

Rejoined ProducePay in late February. Ramp-up → first contributions → AI-powered productivity by week 3.

## Key Threads

1. **Pre-harvest decommission** — Removed unused apps/infra ([VP-3771](https://producepay.atlassian.net/browse/VP-3771), W10), cleaned up role references, released to prod (W12). Reduces costs and simplifies codebase.

2. **Order lifecycle investigations** — Two spikes on the order state machine:
   - Un-fulfill orders ([TMS-2394](https://producepay.atlassian.net/browse/TMS-2394)): trade support can't set deductions on fulfilled orders. Wrote [spike doc](link), got product approval.
   - INVOICE_PAID ([POS-1355](https://producepay.atlassian.net/browse/POS-1355)): voiding fails on fully attributed orders. Wrote [spike doc](link). Pending eng sync.

3. **Financing fee correction** — [BSR-359](https://producepay.atlassian.net/browse/BSR-359). 23 trade orders showing wrong fee in TMS. Direct SQL fix. [Documented](link).

4. **AI-powered engineering** — Set up Claude Code with MCP integrations (Jira, Confluence, Slack, DB). Created [TF-527](https://producepay.atlassian.net/browse/TF-527) epic for AI metrics. Shipped: [TF-517](https://producepay.atlassian.net/browse/TF-517), [TF-518](https://producepay.atlassian.net/browse/TF-518), [TF-512](https://producepay.atlassian.net/browse/TF-512), [TF-513](https://producepay.atlassian.net/browse/TF-513).

5. **Nanonets fix + Marketplace SKUs** — Fixed document matching bug ([VP-3827](https://producepay.atlassian.net/browse/VP-3827)) blocking operations. Added 6 SKU changes ([SM-127](https://producepay.atlassian.net/browse/SM-127)–[SM-132](https://producepay.atlassian.net/browse/SM-132)), customer-requested.

6. **Support & reviews** — Handled BSR, POS, and TMS support tickets. Code reviews across the team.

## By the Numbers

- 12+ PRs merged across 4 active weeks
- 4 Confluence docs (2 spikes, 1 data correction, 1 onboarding report)
- 3 production fixes

## Growth & Learning

- AI workflows went from exploration to daily use for code, tickets, docs, and DB queries
- Learned the order lifecycle state machine (fulfillment, invoicing, attribution)
- Recognition from manager for structured, process-oriented approach
- Completed release owner training

## Looking Ahead

- Visibility shipments
- [VP-3774](https://producepay.atlassian.net/browse/VP-3774) — Salesforce company permissions
- POS-1355 investigation after eng sync
```

## Example 2: A full, steady-state quarter

```markdown
# Q3 2026 — Weeks 27–39

## Overview

Feature-heavy quarter. Shipped visibility shipments and permissions refactor. Support load stayed steady.

## Key Threads

1. **Visibility shipments** — [VP-4100](https://producepay.atlassian.net/browse/VP-4100). New feature allowing buyers to track shipment status. 3-week build: design (W28), implementation (W29-30), QA and launch (W31). Requested by 4 customers during sales calls.

2. **Salesforce permissions refactor** — [VP-3774](https://producepay.atlassian.net/browse/VP-3774). Moved user company permission to Salesforce source of truth. Eliminated manual permission syncs that ops was doing weekly.

3. **Incident: payment webhook duplicates** — W33. Idempotency key bug caused ~50 duplicate charges. Hotfix same day, wrote [postmortem](link). Led to RFC for shared idempotency middleware.

4. **Support rotation** — Averaged 4-5 BSR/POS tickets per week. Biggest: [BSR-450](https://producepay.atlassian.net/browse/BSR-450) required cross-service investigation across TMS and payments.

## By the Numbers

- 18 PRs merged
- 2 features shipped to prod
- 1 incident resolved (same-day hotfix)
- 6 Confluence docs

## Growth & Learning

- First feature shipped end-to-end (visibility shipments)
- Incident response experience — first time leading a hotfix

## Looking Ahead

- Idempotency RFC arch review
- Invoice status machine redesign
```

## What makes a good quarterly rollup

- **Keep it short.** 2-4 lines per thread max. Combine small related items.
- **Only say what the logs said.** Don't invent phrases like "became the go-to person" or "owned end-to-end." If the logs say "handled tickets", say "handled tickets."
- **Tell stories, not lists.** Connect multi-week work into a thread, but stay factual.
- **Lead with impact** — only where the weekly logs captured it. Don't fabricate.
- **Quantify from the logs.** PRs merged, tickets closed, docs written.
- **Don't inflate.** Honest framing builds trust.
- **Link everything.** Every ticket and Confluence page should be clickable.
