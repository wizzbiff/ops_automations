# Board Metrics config

Copy this file to `config.md` in this same folder, then fill in every value. `config.md` is ignored by git, so your real ids, financials, and targets never get committed. This task reads only this file, not the shared `config/config.md`: its values (teams, Jira status mapping) do not apply to a board pack.

Each value is written as `{{UPPER_SNAKE_CASE}}`. Replace the whole token, braces included.

## Period

```yaml
fiscal_year_start_month: {{FISCAL_YEAR_START_MONTH}}   # 1-12, the month your fiscal year begins
runway_floor_months:     {{RUNWAY_FLOOR_MONTHS}}       # board-attention trigger when runway falls below this
```

## Metric sources

Looker supplies growth and product metrics; NetSuite supplies financials. List the look or explore reference for each metric and the NetSuite report or saved search to pull. Use the exact identifiers as they appear in each system.

```yaml
looker:
  base_url:            {{LOOKER_BASE_URL}}
  growth_looks:        # metric name -> look id or explore reference
    new_arr:           {{LOOK_NEW_ARR}}
    expansion_arr:     {{LOOK_EXPANSION_ARR}}
    net_revenue_retention: {{LOOK_NRR}}
    churn:             {{LOOK_CHURN}}
    qualified_pipeline: {{LOOK_PIPELINE}}
  product_looks:
    active_accounts:   {{LOOK_ACTIVE_ACCOUNTS}}
    leading_indicator: {{LOOK_LEADING_INDICATOR}}

netsuite:
  account:             {{NETSUITE_ACCOUNT_ID}}
  financial_report:    {{NETSUITE_REPORT_REF}}          # report or saved search for monthly financials
```

## OKRs

OKRs are read from Jira. Name the project that holds them, the issue types for objectives and key results, the field that marks the quarter, and the fields that carry each key result's target and current value.

```yaml
okrs:
  jira_project:        {{OKR_JIRA_PROJECT}}
  objective_issuetype: {{OKR_OBJECTIVE_TYPE}}
  key_result_issuetype: {{OKR_KR_TYPE}}
  quarter_field:       {{OKR_QUARTER_FIELD}}
  target_field:        {{OKR_TARGET_FIELD}}
  current_field:       {{OKR_CURRENT_FIELD}}
```

## Plan

The plan or target each metric is judged against for the period. Definitions live in the standard; only the numbers are here.

```yaml
plan:
  revenue:             {{PLAN_REVENUE}}
  gross_margin:        {{PLAN_GROSS_MARGIN}}
  burn:                {{PLAN_BURN}}
  new_arr:             {{PLAN_NEW_ARR}}
  expansion_arr:       {{PLAN_EXPANSION_ARR}}
  net_revenue_retention: {{PLAN_NRR}}
  churn:               {{PLAN_CHURN}}
  qualified_pipeline:  {{PLAN_PIPELINE}}
```

## Distribution

```yaml
board_slack_channel: {{BOARD_SLACK_CHANNEL}}
direct_recipients:   [{{DIRECT_RECIPIENTS}}]
```

`board_slack_channel` is where the summary and board-attention pointer post. Keep it a private leadership channel; the pack holds sensitive data. `direct_recipients` is optional. Leave the brackets empty to post only to the channel.
