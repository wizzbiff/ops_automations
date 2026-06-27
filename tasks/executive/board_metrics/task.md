# Board Metrics, task

This is the instruction the task runs. Paste it as the task body when you run by hand, and use the same text when you set up `/schedule`. Run it once a month, after the month's books are closed, on the same day each month so the periods tile cleanly. Paths are written from the repo root so they resolve no matter where this file sits.

---

Run the monthly board metrics pack.

**Step 1. Load everything.** Read these files in full before doing anything else, and treat them as the source of truth:
* tasks/executive/board_metrics/config.md, for the metric source pointers, OKR source, targets and plan, fiscal year start, runway floor, and the board channel. This task does not use the shared config/config.md; its values live here.
* standards/executive/board_metrics.md, for the metric catalog, key result health, trend, the needs-board-attention lens, cadence, and the source-query patterns.
* standards/shared/style.md, for tone and formatting.
* tasks/executive/board_metrics/pack_template.md, for the output shape.

If tasks/executive/board_metrics/config.md does not exist, stop and say so. The system is not configured.

**Step 2. Fix the period.** From the standard, set the closed month, the prior month, and the current fiscal quarter, using the fiscal year start from config. State the period you settled on at the top of the pack so a reader can check it.

**Step 3. Read last month for trend.** Before pulling anything new, read output/board_metrics/latest.md if it exists, and keep its headline metrics and each key result's bucket as last month's baseline. If the file is absent or cannot be parsed, treat this as a run with no prior month to compare, per the standard, and carry no baseline.

**Step 4. Gather from the three sources**, each through its connector, using the source-query patterns in the standard and the ids and names from config:
* **Looker** for the growth and product metrics: run the configured look or explore for each metric, scoped to the closed month.
* **NetSuite** for the financial metrics: pull the configured report or saved search for the closed month's period, and read revenue, margin inputs, burn, and cash.
* **Jira** for the OKRs: query the configured OKR project and issue types for the current quarter's objectives and key results, reading each key result's target and current value from the configured fields.
If any source is unavailable, mark its section unavailable and note it at the top of the pack rather than dropping it silently.

**Step 5. Compute** using the standard:
* Each metric's value, its month-over-month change against the baseline, and its standing versus plan; runway against the runway floor.
* Each key result's health by pace to target, and each objective's health from its key results.
* Trend for the headline metrics and key result buckets against last month's baseline. Show direction only where a real prior figure exists. If there is no baseline, state "no prior month to compare" and omit trend.
* The needs-board-attention list, applying the escalation lens. Keep it to what the board must know or act on.

**Step 6. Generate** the pack using pack_template.md exactly, following style.md for tone. Lead with the executive summary and the board-attention list. Numbers up front. Keep it to roughly two screens; a board pack is denser than the engineering reports but is still read fastest when it leads with what matters.

**Step 7. Write output.** Save to output/board_metrics/pack_YYYY_MM.md using the closed month, and overwrite output/board_metrics/latest.md with the same content. Write latest.md only after you have read last month's copy in Step 3, so next month's run has this month as its baseline.

**Step 8. Distribute.** The board pack is primarily the written artifact in output/board_metrics/. Post the Executive summary and Needs board attention sections to `board_slack_channel` from config, with a short pointer to the full pack, so leadership sees the headline and a person can carry the pack to the board. Board members are not assumed to be in Slack.

**Rules.**
* Only include data the recipients can access.
* If a required connector is unavailable, follow the standard: mark that source's section unavailable and flag it at the top. If NetSuite, Looker, and Jira are all unavailable, stop, write a short note to output/board_metrics/latest.md explaining what failed, and distribute nothing. Do not overwrite a good prior latest.md with an empty pack.
* Financial and OKR data are sensitive. Distribute only to the configured board channel and recipients, never more widely.
* Metrics, retention, usage, and key results are company and system measures, never individual performance. Keep per-person framing out of every section.
* If you had to guess at anything material, or trend or a source is unavailable, say so at the top of the pack.

---

## Where fixes go

* Wrong metric definitions, key result health, trend, or escalation logic: fix standards/executive/board_metrics.md, so every adopter gets the correction.
* Wrong look ids, report ids, OKR project or fields, targets, plan, fiscal start, runway floor, or board channel: fix your own tasks/executive/board_metrics/config.md.
* Wrong pack shape or length: fix this folder's pack_template.md.
* Wrong tone across all reports: fix standards/shared/style.md.
