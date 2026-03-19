# Engineering Log Book

A personal engineering log system powered by Claude Code skills. Write weekly logs interactively and roll them up into quarterly summaries for performance reviews.

## How it works

Two Claude Code skills do the heavy lifting:

- **`/weekly-log`** — Pulls data from Jira, GitHub, Confluence, and Google Calendar, then walks you through an interactive conversation to write your weekly log. Asks about impact, invisible work, and what's coming next.
- **`/quarterly-rollup`** — Reads all weekly logs for a quarter and synthesizes them into a brag-doc-style summary with key threads, numbers, and growth notes.

## Setup

1. Fork this repo privately (your reports shouldn't be public)
2. In your private fork, remove the report exclusions from `.gitignore` so your logs get committed
3. Configure your identifiers by running this in Claude Code:

```
set LOGBOOK_JIRA_ACCOUNT_ID=your-jira-account-id
set LOGBOOK_ATLASSIAN_CLOUD_ID=your-site.atlassian.net
set LOGBOOK_GITHUB_USERNAME=your-github-username
set LOGBOOK_GITHUB_ORG=your-github-org
set LOGBOOK_CALENDAR_ID=primary
set LOGBOOK_TIMEZONE=America/Your_Timezone
```

This writes env vars to `.claude/settings.local.json` (gitignored — your values stay private). The skills read these at runtime.

To find your Jira account ID, run `/weekly-log` and check the Atlassian MCP tools, or ask Claude: "what's my Jira account ID?"

4. Update `CLAUDE.md` with your project details

## Structure

```
weeks/YYYY/YYYY-WXX.md       — one file per ISO week
quarters/YYYY/YYYY-QX.md     — one file per quarter
.claude/skills/               — Claude Code skills
.claude/settings.json         — env var template (committed)
.claude/settings.local.json   — your actual values (gitignored)
```

## Weekly log format

No rigid template. Each week is different. Logs are organized by narrative threads — not categories like "Accomplishments / Blockers / Next." Each item tells a mini-story with linked Jira tickets, PRs, and Confluence pages inline.

See `.claude/skills/weekly-log/references/examples.md` for examples.

## Quarterly rollup format

Synthesizes weekly logs into multi-week stories. Includes key threads, numbers (PRs merged, docs written, fixes shipped), growth notes, and what's ahead.

See `.claude/skills/quarterly-rollup/references/examples.md` for examples.

## Requirements

- [Claude Code](https://claude.ai/claude-code) with MCP integrations for:
  - Atlassian (Jira + Confluence)
  - Google Calendar
  - GitHub CLI (`gh`)
