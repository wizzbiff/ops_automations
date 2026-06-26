# Weekly Leadership Rollup config, optional

Most adopters need nothing here. This task reads the shared config/config.md for teams, status mapping, and distribution. Use this file only to send the weekly rollup somewhere other than the morning report's channel, for example a leadership-only channel, or to run it against a subset of teams.

Copy to config.md in this folder if you need it. It is ignored by git like the shared config. If you do not need overrides, delete this file from your copy of the task.

```yaml
# overrides only. anything not set here falls back to config/config.md
rollup_slack_channel: {{OVERRIDE_ROLLUP_CHANNEL}}
teams_filter:         [{{ONLY_THESE_TEAMS}}]
```

`rollup_slack_channel` is where the weekly rollup posts. Leave this file out and it falls back to `report_slack_channel` in config/config.md. `teams_filter` limits the rollup to the named teams; leave the brackets empty or delete the line to include every team in config.
