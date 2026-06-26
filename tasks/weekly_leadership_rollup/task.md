# Weekly Leadership Rollup, task

This is the instruction the scheduled task runs. Paste it as the task body when you run by hand, and use the same text when you set up `/schedule`. Run it once a week on the same weekday so the week windows tile cleanly. Paths are written from the repo root so they resolve no matter where this file sits.

---

Run the weekly leadership flow and risk rollup.

**Step 1. Load everything.** Read these files in full before doing anything else, and treat them as the source of truth:
* config/config.md, for teams, status mapping, and distribution.
* standards/engineering/definitions.md, for the status buckets, classification, thresholds, and escalation this task builds on.
* standards/engineering/flow.md, for the week window, throughput, cycle time, aging, trend, and the weekly escalation lens.
* standards/shared/style.md, for tone and formatting.
* tasks/weekly_leadership_rollup/rollup_template.md, for the output shape.
* tasks/weekly_leadership_rollup/config.md, only if it exists, for a distribution override.

If config/config.md does not exist, stop and say so. The system is not configured.

**Step 2. Read last week for trend.** Before pulling anything new, read output/weekly_leadership_rollup/latest.md if it exists, and keep its headline figures (done, net new, blocked, at risk, stale, average cycle time) as last week's baseline. If the file is absent or cannot be parsed, treat this as a run with no prior week to compare, per flow.md, and carry no baseline.

**Step 3. Pull from Jira** through the Atlassian connector. For every team in config, query its project and board using the JQL patterns in flow.md and definitions.md, substituting that team's project key and the status names from the config mapping. For the trailing business week defined in flow.md, pull: work done this week, net new this week, active work in flight, and flagged or waiting issues. Read each issue's status-change history where you need it, so you can compute cycle time for issues done this week and age for work in flight. If a query returns nothing for a team, record the team as clear rather than dropping it.

**Step 4. Compute the week** using flow.md, and classify in-flight work using definitions.md:
* Throughput: done this week and net new this week, per team.
* Cycle time: the team average over issues done this week. If a team closed nothing, report no completions, not zero.
* Aging: the oldest one or two in-flight issues per team at or past the stale threshold.
* Carried risk: blocked, at risk, and stale counts per team, plus any persistent blocker that was blocked across the whole week.
* Trend: compare this week's headline figures to last week's baseline from Step 2. Show direction only where a real prior figure exists. If there is no baseline, state "no prior week to compare" and omit trend arrows.
Place anything that does not fit cleanly under needs review with a one line reason. Do not invent a status or a trend.

**Step 5. Generate** the rollup using rollup_template.md exactly, following style.md for tone. Lead with the summary and the leadership escalation list. Apply the weekly escalation lens in flow.md so the escalation section holds only what needs a leader to act: persistent blockers, slipping dates, and teams trending worse. Stay under the word limit in the template.

**Step 6. Write output.** Save to output/weekly_leadership_rollup/rollup_YYYY_MM_DD.md using today's date, and overwrite output/weekly_leadership_rollup/latest.md with the same content. Write latest.md only after you have read last week's copy in Step 2, so next week's run has this week as its baseline.

**Step 7. Distribute.** Post the Summary and Risks needing leadership action sections to the rollup channel, with a short pointer to the full rollup. Use `rollup_slack_channel` from this folder's config.md if set, otherwise `report_slack_channel` from config/config.md. Send to `direct_recipients` only if config lists any.

**Rules.**
* Only include data from boards and channels the recipients can access.
* If the Atlassian or Slack connector is unavailable, stop. Write a short note to output/weekly_leadership_rollup/latest.md explaining what failed and post nothing. Do not overwrite a good prior latest.md with a partial week; if you must write the failure note, say plainly that it replaces the prior rollup.
* Never include per engineer performance framing in any leader facing section. Throughput, cycle time, and aging are team and system measures, never individual scores.
* If you had to guess at anything material, or trend is unavailable, say so at the top of the rollup.

---

## Where fixes go

* Wrong week window, cycle time, aging, or trend logic: fix standards/engineering/flow.md, so every adopter gets the correction.
* Wrong things flagged as blocked, at risk, or stale, or wrong thresholds: fix standards/engineering/definitions.md.
* Wrong teams, keys, status names, or recipients: fix your own config/config.md.
* Wrong rollup shape or length: fix this folder's rollup_template.md.
* Wrong tone across all reports: fix standards/shared/style.md.
