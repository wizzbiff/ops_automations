# Ops Automations

A versioned library of Claude Cowork automations across operational domains. Each automation reads your tools, applies a shared standard, and produces a report or a result. Engineering operations is the first domain. Others, such as executive operations, drop in beside it without disturbing what already works.

Suggested repo name: `ops_automations`. Rename the root folder to whatever fits your org.

## The rule that makes this scale

Anything shared across domains lives in the shared layer. Anything specific to one domain lives in that domain's own files. That single boundary is what keeps the repo from turning into copies of the same definitions drifting apart as it grows.

It produces four kinds of content:

* **Shared standard** (`standards/shared/`). Identical for every domain. Tone and formatting that every report should follow. Nobody edits this to adopt the system.
* **Domain standard** (`standards/<domain>/`). The definitions and thresholds for one domain, for example engineering ticket health. A domain's tasks read its own standard, not another domain's.
* **Config** (`config/`). The only thing an adopter fills in. Teams, status mapping, distribution. Ignored by git so real keys never get committed.
* **Tasks** (`tasks/`). One self contained folder per automation. Its instruction, its output shape, its README. Reads from the standards and config, never copies them.

## Layout

```
ops_automations/
  README.md                       this file: the catalog and the rules
  CONTRIBUTING.md                 how to change a standard, add a task, add a domain
  CHANGELOG.md                    versioned history of the standards
  .gitignore

  config/
    config.example.md             copy to config.md and fill in. the only file you edit
    connectors.md                 which connectors each task needs, and setup notes

  standards/
    shared/
      style.md                    tone and formatting for every report, every domain
    engineering/
      definitions.md              blocked, at risk, stale, escalation, thresholds
    (executive/ and other domains land here as siblings)

  tasks/
    _task_template/               copy this folder to start a new task
      task.md
      output_template.md
      README.md
      config.example.md           optional per task overrides
    engineering/                  tasks grouped by domain, mirroring standards/
      morning_ticket_report/      an engineering domain task
        task.md                   the instruction the scheduled task runs
        report_template.md        this task's output shape
        README.md                 what it does, cadence, connectors
    executive/
      board_metrics/              the executive domain's metrics pack

  output/                        generated results, per task subfolder. ignored by git
    .gitkeep
```

## Task catalog

| Task | Domain | What it does | Cadence | Connectors |
|------|--------|-------------|---------|------------|
| morning_ticket_report | engineering | morning report of blocked, at risk, and stale tickets by team | weekday mornings | Atlassian, Slack |
| daily_personal_brief | engineering | personal triage digest of email, Slack, Jira, and calendar that need your attention | weekday mornings | Gmail or M365, Slack, Atlassian, Google Calendar or Outlook |
| ticket_research | engineering | gathers everything needed to start a ticket: linked docs, related issues, pull requests and code, and Slack threads, into a ready-to-start brief | on demand | Atlassian, Confluence, GitHub, Slack |
| weekly_leadership_rollup | engineering | weekly flow and risk rollup across teams: throughput, cycle time, aging, and week-over-week trend for leadership | weekly | Atlassian, Slack |
| _planned_ board_metrics | executive | assembles the metrics pack for the board | monthly | to be decided |

Keep this table current. It is the first thing a new adopter reads.

## Adopt the library

1. Clone the repo. Open the folder as a Cowork Project and give the Project file access to it.
2. Authorize the connectors listed in config/connectors.md.
3. Copy config/config.example.md to config/config.md and fill it in once. Every task reads it.
4. Pick a task, open its README, and follow its run steps.

## Add a new task to an existing domain

1. Copy `tasks/_task_template/` to `tasks/<domain>/your_task_name/`.
2. Fill in task.md, the output template, and the README. Reuse `standards/shared/style.md` and that domain's standard rather than writing new definitions, so vocabulary stays consistent.
3. List any new connectors in config/connectors.md.
4. Add a row to the task catalog above.

## Add a new domain, for example executive ops

1. Create `standards/your_domain/` and write its definitions there, for example `standards/executive/board_metrics.md`. Reuse `standards/shared/style.md` for tone rather than restating it.
2. Add that domain's tasks under `tasks/your_domain/`, each one copied from `_task_template` and pointed at the new domain standard.
3. Add the new rows to the task catalog and a CHANGELOG note.

Nothing in the engineering domain changes when you add another. See CONTRIBUTING.md for the full conventions.
