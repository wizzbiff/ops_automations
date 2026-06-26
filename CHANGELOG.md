# Changelog

Versioned history of the standards. Config changes by individuals are not tracked here. Only changes to `standards/` (shared or per domain) and to the repo structure belong in this file, because those affect everyone.

## 1.3.0

Added the weekly leadership rollup, the fourth engineering task and the first weekly one.

* standards/engineering/flow.md: new standard defining the weekly flow and risk view: the trailing business week window, throughput (done and net new this week), cycle time, aging work in flight, persistent blockers, week-over-week trend, and a weekly escalation lens broader than the daily one. Reuses the status buckets, thresholds, classification, and escalation in definitions.md by pointer rather than restating them.
* tasks/weekly_leadership_rollup: weekly flow and risk summary across teams for leadership, posted to Slack. Computes this week from Jira and derives trend by comparing to the previous run's saved output, degrading to "no prior week to compare" on a first run. Required connectors are Atlassian (read, including status history) and Slack; no Atlassian write.
* config/connectors.md: added weekly_leadership_rollup to the Atlassian and Slack rows.

## 1.2.0

Added ticket research, the third engineering task and the first on-demand, parameterized one.

* standards/engineering/research.md: new standard defining what a ready-to-start brief contains and how to gather it: ticket resolution and one-hop link following, Confluence and Slack discovery, GitHub matching by ticket-key convention scoped to an allowlist with an evidence rule for unconfirmed matches, fact-versus-inference synthesis, and per-section caps with clear-state reporting. Reuses the status buckets in definitions.md by pointer.
* tasks/ticket_research: on-demand task that takes a ticket key or URL, assembles the brief, writes it to output, and posts a short pointer comment back to the ticket. Required connector is Atlassian (Jira) read; Confluence, GitHub, and Slack are enrichment that degrade gracefully.
* config/connectors.md: restored Atlassian (Jira) write, used only by ticket_research to post one comment on the input ticket, and activated the Confluence and GitHub rows for it.

## 1.1.0

Added the daily personal brief, the second engineering task.

* standards/engineering/personal_triage.md: new standard defining what counts as needing your attention across email, Slack, Jira, and calendar, plus dedup precedence, deterministic "Start here" ranking, and per-section item caps. Reuses the Blocked, At risk, and Stale thresholds from definitions.md by pointer rather than restating them.
* tasks/daily_personal_brief: personal morning digest of email, Slack, Jira, and calendar, delivered as a Slack DM to self. Mail source (Gmail or Microsoft 365) and calendar source (Google Calendar or Outlook) are config-selectable.
* config/connectors.md: added Gmail, Microsoft 365, and Google Calendar rows for the new task.

## 1.0.0

Initial release.

* Structure: standards split into a shared house layer (standards/shared/) and per domain standards (standards/engineering/), so additional domains such as executive ops can be added without disturbing existing ones.
* standards/engineering/definitions.md: blocked, at risk, stale, completed yesterday, net new, needs review. Thresholds set: at risk window 2 business days, stale 3 business days, escalation age 2 business days, escalation date window 3 days.
* standards/shared/style.md: shared tone and formatting rules.
* tasks/morning_ticket_report: first task. Morning report of ticket health by team, posted to Slack.
* config: shared adopter config for teams, status mapping, and distribution. connectors reference.
* _task_template: copyable shape for new tasks.
