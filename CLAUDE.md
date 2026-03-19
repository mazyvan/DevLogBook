# Engineering Log Book

Weekly engineering progress log.

## Structure
- `weeks/YYYY/YYYY-WXX.md` — one file per ISO week (Mon–Fri)
- `quarters/YYYY/YYYY-QX.md` — one file per quarter (aggregated from weekly logs)
- `.claude/skills/weekly-log/references/examples.md` — example weekly logs for tone/format guidance
- `.claude/skills/quarterly-rollup/references/examples.md` — example quarterly rollups

## Style
- Narrative threads, not rigid categories — each item tells a mini-story with related tickets/PRs/docs inline
- Concise but with enough context for future reference
- No fluff — just what happened, what matters
- Weeks run Monday to Friday

## Data Sources for Weekly Logs
- **Jira**: Tickets assigned to the user (all projects)
- **GitHub**: PRs opened by the user that were merged (focus on big/important ones)
- **Confluence**: Pages created by the user during the week
- **Google Calendar**: Days off and non-recurring important meetings only
- **No Slack scanning**

## Weekly Log Process
The `/weekly-log` skill is interactive. It should:
1. Ask questions about the week rather than auto-generating everything
2. Pull data from Jira/GitHub/Calendar as supporting context
3. Let the user confirm, edit, or add to each section before writing the file
