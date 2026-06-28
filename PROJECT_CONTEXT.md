# Project Context and Build Roadmap

Read this first at the start of any build session. It is the map and the roadmap. It does not replace the repo's own README.md and CONTRIBUTING.md, which remain the authoritative description of structure and conventions. When this file and those files disagree, the repo files win, and this file should be corrected.

## How to use this file in a Claude Code session

The primary build surface is Claude Code, working directly against this git repo.

1. At the start of a session, read CLAUDE.md, then this file, then CONTRIBUTING.md.
2. Build from the files in the working tree. Extend them. Do not recreate them from memory.
3. Pick the next item marked PLANNED in the roadmap below.
4. Commit changes directly to the repo in small, reviewable steps. The git tree, not a chat snapshot, is the source of truth, so there is nothing to re sync.

Cowork remains the run and validate surface. Claude Code authors the files but cannot execute the automations. After building an item, install or run it in Cowork to confirm it works.

## What exists today

Two parallel artifacts, both already built.

* **ops_automations** (the folder library). This is the source of truth and the baseline repo. You edit and run this. Structure: a shared layer plus per domain standards and tasks.
* **ops_marketplace** (the plugin marketplace). A parallel packaging of the same content as a Cowork plugin marketplace. Parked. Do not treat it as source of truth. Promote it later, as its own separate repo, only when both promotion conditions below are true.

The first engineering automation, morning_ticket_report, was originally the only one built in both. **As of 2026-06-28 the marketplace was brought back to full parity with the library.** All four engineering tasks (morning_ticket_report, daily_personal_brief, ticket_research, weekly_leadership_rollup) and the executive board_metrics task now exist as plugins: engineering_ops 2.0.0 (its three new tasks ported as commands plus the personal_triage, research, and flow standards as skills) and the new executive_ops 1.0.0 (board_metrics standard as a skill, board_pack command). Delivered via wizzbiff/ops_marketplace PR #1.

The marketplace is still parked and still not the source of truth; this sync was a deliberate choice to keep parity even though the promotion gate below (standards settled, more than one runner) is not yet met. Two things were decided in the sync and may want revisiting: the per-command config (personal, research, board) was folded into the marketplace's single shared config.example.md as self-contained sections rather than separate per-plugin files, to match the marketplace's one-local-config model; and because standards are still moving, expect to re-sync the marketplace whenever a library standard changes.

## Marketplace sync model

ops_marketplace is downstream of this library, not a peer. The relationship, written down so a future session does not have to reconstruct it:

* **One source of truth.** Author standards and tasks here, in ops_automations. The marketplace is a derived packaging of the same content as Cowork plugins (standards become skills, tasks become commands). Never author in the marketplace and back-port; that would make the copy the source.
* **One-directional, manual, unenforced.** Nothing links the two repos. A change here does not propagate; it leaves the marketplace silently stale until someone re-ports it by hand. There is no error and no warning on drift, so a library edit is also an implicit to-do against the marketplace.
* **A re-sync is a transformation, not a copy.** A standard becomes a SKILL.md with a load-trigger description; a task.md plus its template become one command file; repo-relative path pointers become skill-name references; and the per-task config.md files collapse into the marketplace's single shared config.md as sections. Judgement each time, so it cannot be fully scripted.
* **"In sync" is a snapshot.** Parity holds only at the moment of a sync (most recent: 2026-06-28, wizzbiff/ops_marketplace PR #1). The next library change makes it stale again.
* **Parked by design.** Per the promotion gate in Key decisions below, the marketplace stays parked while standards are still moving. Accept that it lags; catch it up deliberately in a dedicated sync rather than paying the port tax on every edit. Re-sync when standards settle, or when you decide to promote.

## Repo structure and the scaling rule (summary, see README and CONTRIBUTING for detail)

The rule: anything shared across domains lives in the shared layer; anything specific to one domain lives in that domain's files.

Shared, common to every domain:
* standards/shared/style.md, tone and formatting for every report.
* config/, holding config.example.md (teams, status mapping, distribution) and connectors.md. Each adopter copies config.example.md to a local config.md that is gitignored. Real keys are never committed.

Domain specific:
* standards/<domain>/, definitions and thresholds for that domain, for example standards/engineering/definitions.md.
* tasks/<domain>/<task>/, one self contained folder per automation, grouped by domain to mirror standards/: task.md (orchestration), an output template, a README. It reads the shared style, its domain standard, and config. It never copies them. Generated output stays flat at output/<task>/.

Generated output goes to output/<task>/, gitignored.

**Adding a workflow to an existing domain:** copy tasks/_task_template/ to tasks/<domain>/<name>/, fill it in, point it at standards/shared/style.md and the domain standard, list connectors in config/connectors.md, and add a row to the task catalog in README.

**Adding a domain:** create standards/<domain>/ and write its definitions, add its tasks under tasks/<domain>/, reuse standards/shared/style.md for voice, and update the catalog and CHANGELOG. Nothing in an existing domain changes.

**Resolved when the executive domain landed: tasks are now grouped by domain.** When board_metrics added the executive domain, the previously deferred decision was taken: tasks moved from the flat tasks/<task>/ layout to tasks/<domain>/<task>/ (tasks/engineering/ and tasks/executive/) for symmetry with standards/. Output deliberately stayed flat at output/<task>/, since task names are unique and the dirs are gitignored, so nothing about output paths actually had to change. tasks/_task_template/ stayed at the tasks/ root because it is domain agnostic. The four engineering tasks' internal path references were rewritten in the same move.

**Open decision on personal_triage.md placement:** standards/engineering/personal_triage.md is personal triage logic that is not strictly engineering. It lives in the engineering domain because its only consumer, daily_personal_brief, is filed there. If a second personal-triage task lands in another domain, graduate this standard to a cross-cutting location rather than copying it.

## Roadmap

This traces back to the original list from the colleagues plus the domains we discussed.

### Engineering domain

* **morning_ticket_report. BUILT.** Morning report of blocked, at risk, and stale tickets by team, posted to Slack. Connectors: Atlassian, Slack. (Colleague item: the morning team report sent to leaders.)
* **daily_personal_brief. BUILT.** A personal triage digest of the email, Slack messages, Jira items, and calendar events that need your attention, produced each morning. The output is a digest to yourself, delivered as a Slack DM to self, not a team report. Mail source (Gmail or Microsoft 365, read only) and calendar source (Google Calendar or Outlook) are config-selectable. Connectors: Gmail or Microsoft 365, Slack, Atlassian, Google Calendar or Outlook. Adds the standard standards/engineering/personal_triage.md, which reuses the Jira thresholds in definitions.md. (Colleague items: the daily brief, and doing everything through Claude rather than logging into each app.)
* **ticket_research. BUILT.** On demand. Given a ticket, gather its linked Confluence docs, related issues, GitHub pull requests and code context, and relevant Slack threads, then produce a ready to start brief, written to output and posted as a short pointer comment back to the ticket. The first parameterized task (takes a ticket key or URL at run time) and the first that writes to a source system. Connectors: Atlassian, GitHub, Confluence, Slack. Adds the standard standards/engineering/research.md, which reuses the status buckets in definitions.md. (Colleague item: the automation that researches a ticket so you can begin work.)
* **weekly_leadership_rollup. BUILT.** Weekly flow and risk summary across teams for leadership, posted to Slack. Computes the trailing business week from Jira, throughput, cycle time, aging work in flight, and persistent blockers, and derives week-over-week trend by comparing to the previous run's saved output (degrading to "no prior week to compare" on a first run). Connectors: Atlassian, Slack. Adds the standard standards/engineering/flow.md, which reuses the buckets, thresholds, and escalation in definitions.md by pointer. Artifacts ready to install and test in Cowork.

### Executive operations domain (new)

* **board_metrics. BUILT.** Assembles the monthly board metrics pack and posts the summary and board-attention pointer to a private leadership channel. Sources resolved: growth and product metrics from Looker, financials from NetSuite, OKRs from Jira. The standard standards/executive/board_metrics.md defines each metric, key-result health by pace to target, month-over-month trend, the needs-board-attention lens, and the source-query patterns; it incorporates the OKR framework as the framing for the strategic-progress section while a separate metrics section carries the hard numbers. Reuses standards/shared/style.md for voice. First task to read a BI layer and a finance system, and the first not to use the shared config/config.md. Connectors: Looker, NetSuite, Atlassian, Slack. Looker and NetSuite are not in the default connector set and must be added in Cowork before the task runs. Artifacts ready to install and test in Cowork.

### Future domains

Other operational domains can follow the same pattern, each as standards/<domain>/ plus its tasks. Add a domain only when there is a real automation to build, not speculatively.

## Mapping back to the original colleague list

For traceability, the five things the colleagues described map as follows:

* Daily brief of emails, Slack, and tickets needing attention, to daily_personal_brief.
* Morning team ticket report sent to leaders, to morning_ticket_report (built).
* Automation that researches a ticket, to ticket_research (built).
* Doing everything through Claude instead of logging into each app, covered by the connector set the automations above use, not a separate task.
* Keeping context in markdown and pointing Claude at the file, which is the method this whole repo and this file embody, not a task.

## Key decisions and constraints to remember

* **Build surface.** Claude Code is the primary surface for authoring and committing this repo. Cowork is the only surface that runs the automations. Claude Code cannot validate runtime behavior, so treat its output as ready to install and test, not as verified working. CLAUDE.md holds the session rules.
* **Plugin vs folder.** Stay on the folder library while the patterns are still settling. Promote to the plugin marketplace only when both are true: the standards have stopped changing week to week, and more than a few people need to run the tasks rather than just read the output. The marketplace must be its own separate repo, because Cowork reads a marketplace from a repo whose root holds .claude-plugin/marketplace.json.
* **Scheduling.** A scheduled report is a per user Cowork action via /schedule. It runs only while that person's computer is awake and the desktop app is open. Scheduling is not packaged by a plugin and does not run server side. Reliable unattended timing is a separate problem to solve if it becomes a hard requirement.
* **Distribution.** Reports distribute through Slack, not Outlook. The Microsoft 365 connector is read only and cannot send mail. If a result must reach inboxes, post to a channel people watch or forward it manually.
* **Connectors.** Connectors are MCP based, authorized once via OAuth, and respect existing permissions. Claude only sees what the connected account can see.
* **Atlassian write scope.** Atlassian (Jira) was narrowed to read while only the report tasks existed, then restored to read and write when ticket_research landed. The write is used by ticket_research alone, only to post one pointer comment on the ticket being researched. Every other task reads from Atlassian. Keep the grant matched to actual use: narrow it again if ticket_research is ever removed.
* **Config safety.** Only config.example.md is committed. The real config.md is local per user and gitignored. No project keys, board ids, channels, or handles in committed files.
* **Conventions.** Placeholders are written {{UPPER_SNAKE_CASE}}. Identifiers (folders, task names, plugin and skill names) use underscores. In the plugin version only, the fence lines at the top of each SKILL.md and command file are mandatory YAML frontmatter syntax.
* **Research preview.** Cowork plugin support is a research preview and its format moves, especially how connectors attach. Verify the plugin manifests against current Cowork docs before relying on them. This is one more reason the folder library is the safer working surface today.

## Working agreement

* The git working tree is the source of truth. Read it first, extend it, do not regenerate from memory.
* Keep all logic and config in repo files. Nothing important should live only in a chat or terminal session.
* Every change that adds or renames a task or domain updates three places in the same commit: the README catalog, CHANGELOG.md, and the item status here.
* Keep this roadmap current. As automations move from PLANNED to BUILT, update their status.
* Claude Code authors and commits. Cowork installs, runs, and validates. Do not mark an item done on the strength of the files alone. Confirm it in Cowork.
