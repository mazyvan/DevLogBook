# Quarterly Rollup Examples

These show the tone, structure, and level of detail. Keep it tight — the whole doc should be readable in 2-3 minutes. Only say what the weekly logs actually said. Don't embellish.

## Example 1: Partial quarter, onboarding + ramp-up

```markdown
# Q1 2026 — Weeks 9–12 (in progress)

## Overview

Joined in late February. Ramp-up → first contributions → AI-powered productivity by week 3.

## Key Threads

1. **Legacy system decommission** — Removed unused apps/infra ([INFRA-771](link), W10), released to prod (W12). Reduces costs and simplifies codebase.

2. **Order status investigations** — Two spikes on the order state machine:
   - Reversal flow ([ORD-2394](link)): support can't set deductions on completed orders. Wrote [spike doc](link), got product approval.
   - Payment close ([PAY-1355](link)): voiding fails under certain conditions. Wrote [spike doc](link). Pending eng sync.

3. **Fee correction** — [PAY-359](link). 23 orders showing wrong fee. Direct SQL fix. [Documented](link).

4. **AI-powered engineering** — Set up Claude Code with MCP integrations (Jira, Confluence, Slack, DB). Created epic for AI metrics. Shipped 4 tooling PRs.

5. **Bug fix + catalog updates** — Fixed document matching bug ([BUG-827](link)) blocking operations. Added 6 catalog changes ([CAT-127](link)–[CAT-132](link)), customer-requested.

6. **Support & reviews** — Handled support tickets across 3 projects. Code reviews across the team.

## By the Numbers

- 12+ PRs merged across 4 active weeks
- 4 Confluence docs (2 spikes, 1 data correction, 1 onboarding report)
- 3 production fixes

## Growth & Learning

- AI workflows went from exploration to daily use for code, tickets, docs, and DB queries
- Learned the order lifecycle state machine
- Recognition from manager for structured approach
- Completed release owner training

## Looking Ahead

- Shipment visibility feature
- Permissions refactor ([FEAT-3774](link))
- Payment investigation after eng sync
```

## Example 2: A full, steady-state quarter

```markdown
# Q3 2026 — Weeks 27–39

## Overview

Feature-heavy quarter. Shipped visibility feature and permissions refactor. Support load stayed steady.

## Key Threads

1. **Shipment visibility** — [FEAT-4100](link). New feature for tracking shipment status. 3-week build: design, implementation, QA and launch. Requested by 4 customers.

2. **Permissions refactor** — [FEAT-3774](link). Moved permission source of truth to external system. Eliminated manual syncs that ops was doing weekly.

3. **Incident: payment duplicates** — W33. Idempotency key bug caused ~50 duplicate charges. Hotfix same day, wrote [postmortem](link). Led to RFC for shared middleware.

4. **Support rotation** — Averaged 4-5 tickets per week. Biggest: [SUP-450](link) required cross-service investigation.

## By the Numbers

- 18 PRs merged
- 2 features shipped to prod
- 1 incident resolved (same-day hotfix)
- 6 Confluence docs

## Growth & Learning

- First feature shipped end-to-end
- Incident response experience — first time leading a hotfix

## Looking Ahead

- Idempotency RFC arch review
- Invoice status redesign
```

## What makes a good quarterly rollup

- **Keep it short.** 2-4 lines per thread max. Combine small related items.
- **Only say what the logs said.** Don't invent phrases or inflate accomplishments. If the logs say "handled tickets", say "handled tickets."
- **Tell stories, not lists.** Connect multi-week work into a thread, but stay factual.
- **Lead with impact** — only where the weekly logs captured it. Don't fabricate.
- **Quantify from the logs.** PRs merged, tickets closed, docs written.
- **Don't inflate.** Honest framing builds trust.
- **Link everything.** Every ticket and Confluence page should be clickable.
