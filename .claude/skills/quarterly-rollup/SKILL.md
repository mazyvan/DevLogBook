---
name: quarterly-rollup
description: Aggregate weekly logs into a quarterly summary / brag document for performance reviews. Use whenever the user wants to create a quarter summary, rollup, brag doc, or performance review prep. Triggers on "quarterly rollup", "quarter summary", "brag doc", "brag document", "Q1 summary", "performance review prep", "roll up my weeks", "summarize the quarter", or any request about aggregating weekly logs into a bigger picture — even casual ones like "let's do the quarter" or "wrap up Q1".
---

# Quarterly Rollup

Aggregate weekly logs into a quarterly summary that's useful for performance reviews, brag documents, and personal reflection. The output should tell the story of the quarter — not rehash every weekly bullet point.

## 1. Figure Out the Quarter

- Default to the most recently completed quarter (e.g., if it's April, default to Q1)
- If the current quarter is in progress, ask: "Q is still in progress — roll up what we have so far, or do the previous quarter?"
- Quarter boundaries: Q1 = W01–W13, Q2 = W14–W26, Q3 = W27–W39, Q4 = W40–W52
- Check if `quarters/YYYY/YYYY-QX.md` already exists — if so, ask whether to update or start fresh

## 2. Read All Weekly Logs

Read every `weeks/YYYY/YYYY-WXX.md` file that falls within the quarter. Note which weeks are missing — mention them so the user is aware of gaps.

## 3. Synthesize — Don't Summarize

The goal is synthesis, not summary. Reading every weekly bullet back-to-back is useless. Instead:

**Identify themes.** What were the big threads across the quarter? Group related work that spans multiple weeks into coherent narratives. Examples:
- "Pre-harvest decommission" might span 3 weeks (investigation → PR → cleanup → prod release)
- "AI integration" might be a thread that runs through the entire quarter
- "Support rotation" might be an ongoing responsibility worth quantifying

**Extract impact.** The weekly logs already have some impact framing — pull it up to the quarter level. Aggregate where possible:
- "Closed 15 BSR support tickets across the quarter"
- "Merged 12 PRs in first 4 weeks"
- "Wrote 4 Confluence spike/investigation docs"

**Note the arc.** Quarters have a shape — ramping up, hitting stride, shifting focus. Call this out in the intro.

## 4. Have a Conversation

Present the draft themes and ask:
- "These are the threads I see across the quarter. Anything missing or that you'd frame differently?"
- "Which of these felt most impactful to you?"
- "Anything that happened outside of what's in the logs?"

This matters because weekly logs capture what happened but not always the full significance. A 1-line item in W11 might have been the most important thing in the quarter.

## 5. Write the Rollup

Read `references/examples.md` for tone and format guidance, then:

1. `mkdir -p quarters/YYYY/`
2. Draft with these sections:
   - **Overview** — 2-3 sentences capturing the quarter's arc
   - **Key Threads** — Numbered narrative items, each telling a multi-week story with linked tickets, PRs, and Confluence pages
   - **By the Numbers** — Quick stats (PRs merged, tickets closed, docs written, etc.)
   - **Growth & Learning** — Skills developed, processes improved, recognition received
   - **Looking Ahead** — What's carrying over into next quarter
3. Present draft for approval
4. Write to `quarters/YYYY/YYYY-QX.md`

## Style

- **Keep it short.** The whole doc should be readable in 2-3 minutes. Each key thread gets 2-4 lines max. Combine smaller items into one thread when they're related.
- **Only say what the logs actually said.** Don't invent phrases like "became the go-to person" or "full ownership" unless the user said that. The rollup synthesizes — it doesn't embellish. If the logs say "handled support tickets", don't upgrade that to "owned the support rotation end-to-end."
- **Always link Jira tickets and Confluence pages** — same as weekly logs.
- **Tell stories, not lists.** Connect multi-week work into a single narrative thread, but keep it factual.
- **Lead with impact** — only where the weekly logs already captured it. Don't fabricate impact.
- **Quantify when possible.** Numbers from the logs: PRs merged, tickets closed, docs written.
- **Don't inflate.** Honest framing builds trust. If support ate the quarter, say so — that's valuable work too.
