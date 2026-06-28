# Weekly Leadership Rollup

Once a week, pulls every team's Jira activity over the trailing business week, measures flow and risk against the shared standard, compares it to last week, writes a short rollup, and posts the leader facing summary to Slack. Where the morning report is a daily snapshot, this is the week: what flowed in and out, what risk is carrying over, and what is trending worse.

## At a glance

* Cadence: weekly, same weekday each week
* Requires connectors: Atlassian, Slack
* Reads standards: flow.md, definitions.md, style.md
* Reads config: config/config.md (optional per-task config.md for a channel override)
* Writes to: output/weekly_leadership_rollup/

## Run it

1. Authorize the Atlassian and Slack connectors in Cowork.
2. Copy config/config.example.md to config/config.md and fill it in, if you have not already. The same teams and status mapping the morning report uses.
3. Run by hand once: paste the body of task.md into a Cowork task and read the result. As with the morning report, the first run usually reveals that your real Jira status names do not match the config mapping. Fix config and rerun.
4. When the flow numbers and risk look right, schedule it with `/schedule` on a fixed weekday.

## Notes

* Trend appears only from the second run on. Trend compares this week to the previous run's saved output at output/weekly_leadership_rollup/latest.md. The first run has nothing to compare and says so; run it on the same weekday each week so the windows tile cleanly.
* Run weekly, not daily. Running it more than once a week overwrites latest.md with a partial window and corrupts next week's baseline.
* Cycle time and aging come from each issue's status-change history. A team that closed nothing this week shows no completions rather than a zero cycle time.
* The whole rollup stays under 600 words by standard. If it runs long, the template or the team count, not the task, is usually the cause.
* Distribution is Slack only. By default it posts to the same channel as the morning report; set rollup_slack_channel in a local config.md here to send it somewhere else. See config/connectors.md for the distribution rationale.
