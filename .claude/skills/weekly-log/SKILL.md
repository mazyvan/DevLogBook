---
name: weekly-log
description: Interactive weekly engineering log generator for the IvanLogBook project. Use whenever the user wants to create, update, or review their weekly progress log. Triggers on "weekly log", "log my week", "daybook", "what did I do this week", "write my log", "log book", "week summary", or any request about tracking weekly engineering progress — even casual ones like "let's do the log" or "time to log".
---

# Weekly Engineering Log

Help the user write their weekly log. This is a personal reference — not a status report, not a standup summary. The log should capture what took time, what had impact, and enough context to reconstruct what happened months later.

Think weeknotes, not Jira export.

## 1. Figure Out the Week

- Default to the current ISO week (Mon–Fri)
- If it's Monday or Tuesday, ask whether they mean this week or last
- Compute the ISO week number, date range, and YYYY-MM-DD bounds for queries
- Check if `weeks/YYYY/YYYY-WXX.md` already exists — if so, ask whether to update or start fresh
- **Read the previous 2 weeks' logs** (if they exist) before starting. This serves two purposes:
  1. **Avoid duplication** — if a ticket was already logged as merged in a previous week, don't log it again just because its status changed (e.g., moved to Done/Closed).
  2. **Continuity** — pick up threads from "Up Next" and in-progress items. If last week said "starting VP-3774 next week", ask about it. If a multi-week investigation was in progress, connect this week's update to the previous one.

## 2. Gather Context (All at Once)

Pull from all sources in parallel while asking what happened. The tools provide supporting evidence — the user's perspective is the source of truth.

**Jira** — Atlassian MCP tools (cloudId: `producepay.atlassian.net`)
- `assignee = "712020:f969c7d9-4a70-41e1-b6aa-e1e91b7cdaba" AND updated >= "YYYY-MM-DD" AND updated <= "YYYY-MM-DD" ORDER BY updated DESC`
- `assignee = "712020:f969c7d9-4a70-41e1-b6aa-e1e91b7cdaba" AND status changed DURING ("YYYY-MM-DD", "YYYY-MM-DD") ORDER BY updated DESC`
- Deduplicate by ticket key across both queries
- **Ticket lifecycle**: Tickets go through steps — the one that matters for the log is **Merged** (code reviewed and approved). After that comes QA and eventually Closed/Done when released to prod. Don't log a ticket just because it moved to Done/Closed that week if the actual work (the merge) happened in a previous week. Unless the user specifically says a prod release was noteworthy, treat "Merged" as the milestone worth logging.

**GitHub** — CLI
```bash
gh search prs --author=mazyvan --merged-at=YYYY-MM-DD..YYYY-MM-DD --owner=producepay --json title,repository,url,closedAt
```

**Confluence** — Atlassian MCP tools
- `creator = "712020:f969c7d9-4a70-41e1-b6aa-e1e91b7cdaba" AND created >= "YYYY-MM-DD" AND created <= "YYYY-MM-DD" ORDER BY created DESC`

**Google Calendar** — use `gcal_list_events`
- calendarId: `primary` (ivan.sanchez@producepay.com)
- timeMin: `YYYY-MM-DDT00:00:00` (Monday)
- timeMax: `YYYY-MM-DDT23:59:59` (Friday)
- timeZone: `America/Mexico_City`
- Filter results: Keep PTO, OOO, days off, one-off notable meetings. Drop recurring events (check `recurringEventId`) like standups, 1:1s, daily syncs, sprint ceremonies.

## 3. Have a Conversation

This is the core of the skill. The goal is a natural back-and-forth, not a rigid walkthrough of data sources. Start by asking what stood out, then use the gathered data to fill gaps and jog memory.

**Start open:** Ask what the main things were this week — what took time, what had impact, what was interesting.

**Then present the data as a whole picture.** Don't walk through Jira, then PRs, then Confluence as separate interrogations. Instead, synthesize everything into a coherent view and present it. Group related things together (a ticket + its Confluence doc + its PR are one thing, not three). Call out anything the tools found that wasn't mentioned — it might be something forgotten, or something too small to include. Let the user decide.

**Always show Confluence pages explicitly** — they represent significant work and are easy to miss.

**Ask about the invisible work** — things that don't show up in tools: code reviews, helping teammates, investigations that didn't result in a ticket, important conversations, support rotation. This is often where the most interesting log entries come from.

**Dig into impact.** For the bigger items, ask follow-up questions to capture *why it mattered* — not just what was done. "Fixed financing fee on 23 orders" is fine, but "Fixed financing fee on 23 orders — unblocked billing for those accounts" is what's needed for perf reviews and brag documents. Good follow-ups:
- "Who was this blocking or what did it unblock?"
- "Why was this urgent / why now?"
- "What would have happened if this hadn't been done?"
Don't ask these for every item — use judgment:
- **Straightforward impact** (e.g., "bug was blocking operations") — just include it in the draft without asking. No need to interrupt the conversation for obvious stuff.
- **Unclear or significant impact** — ask the follow-up question.
- **Housekeeping / small items** — skip impact entirely. Not everything needs a "so what."

**Always ask about next week** — this becomes the "Up Next" section. Also ask about blockers, learnings, or anything noteworthy — these go in an optional "Notes" section if there's anything worth recording.

**Adapt to the week.** Some weeks have a clear theme ("incident week", "deep focus week", "support-heavy week"). Some are scattered. The conversation should match. If the answers are short, don't push — it might just be a light week.

## 4. Write the Log

Once the conversation is done:

1. Read `references/examples.md` (in this skill's directory) for tone and format guidance
2. `mkdir -p weeks/YYYY/`
3. Draft the log with three sections:
   - **Recap** — `# WXX — Mon DD–Fri DD`, a one-line intro capturing the week's tone, then numbered items organized by narrative thread. Related tickets, PRs, and Confluence pages go inline with their story.
   - **Up Next** — what's coming next week. Always included.
   - **Notes** — learnings, recognition, observations. Optional — only when there's something worth recording.
4. Present the draft for approval. The user may want to reword, reorder, add, or cut.
5. Write to `weeks/YYYY/YYYY-WXX.md`
6. **Quarter check** — After writing the log, check if this week is the last week of a quarter (W13, W26, W39, W52) or if the quarter just ended. If so, check whether `quarters/YYYY/YYYY-QX.md` exists. If not, remind the user: "This wraps up QX — want to do a quarterly rollup while it's fresh? You can run `/quarterly-rollup`."

## Style

- **Always link Jira tickets**: `[KEY-123](https://producepay.atlassian.net/browse/KEY-123)`. Every ticket reference gets a clickable link.
- Organize by what happened, not by category. Each item tells a mini-story.
- Connect the dots — a ticket that led to a doc that led to a PR is one item, not three.
- Lead with what matters. Trivial ticket updates don't deserve the same space as a 2-day investigation.
- Terse but with enough context to understand what it was about months later.
- **Include impact on significant items.** Don't just say what was done — say why it mattered, who it unblocked, or what it prevented.
- Short prose is fine. A one-line intro setting the week's tone helps when scanning later.
- Some weeks have 3 items, some have 7. Match the format to the week.
- **Make days off impossible to miss.** If there was a holiday, PTO, OOO, or any time off, call it out prominently — either in the intro line or as a dedicated callout right after the heading (e.g., "> **Monday off — public holiday**"). Don't bury it in the middle of an item where it's easy to skip.
