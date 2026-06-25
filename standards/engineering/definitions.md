# Definitions, the shared standard

This is the common standard every adopter runs against. It contains no personal values. Team names, project keys, and status names come from `config.md`. The thresholds below are the agreed org standard. To change one, change it here so everyone gets the update, not in any individual config.

## Status buckets

The report works in four buckets. Each adopter maps their real Jira status names onto these in `config.md` under the status mapping.

* Active work: the `active_statuses` from config. Work currently in flight.
* Waiting: the `waiting_statuses` from config. Work that is stuck.
* Done: the `done_statuses` from config. Finished work.
* Backlog: the `backlog_statuses` from config. Not started.

## Thresholds (org standard)

* At risk window: 2 business days.
* Stale threshold: 3 business days with no movement.
* Escalation age: a blocked item older than 2 business days.
* Escalation date window: a delivery date inside 3 days.

## Classification rules

Apply these in order to every issue pulled.

**Blocked.** True if any of the following holds:
* its status is in the Waiting bucket, or
* it carries a flag, or
* it has an open "is blocked by" link to an issue that is not yet Done.

**At risk.** An Active work issue that is not blocked but is in danger:
* it has a due date within the at risk window and is not in the final Active status, or
* it sits in a sprint ending within the at risk window with meaningful work remaining.

**Stale.** An Active work issue with no status change and no comment for the stale threshold or longer. Stale is not blocked. It usually means forgotten, not impeded, and is surfaced separately.

**Completed yesterday.** Any issue moved into the Done bucket since the previous business day.

**Net new.** Any issue created since the previous business day that is already in the Active work bucket. Signals unplanned work entering mid sprint.

**Needs review.** If an issue does not fit cleanly, place it here with a one line reason rather than guessing. A short needs review list shows where the taxonomy is fuzzy.

## Escalation rules

An item belongs in the escalation section only if it is blocked AND either older than the escalation age or tied to a delivery date inside the escalation date window. For each escalation, name the team, the issue, why it is stuck, and the one action that would unblock it. Do not list every blocked ticket here, only the ones that need a leader to act.

## Audience framing

The report is read by leaders who care about flow of work and risk, not individual activity. Never include per engineer performance framing in any leader facing section. The report is about where work is stuck, not about who is fast or slow.

## JQL patterns

Generic query shapes. Substitute the project key for each team from config, and the status names from the config mapping.

* Active work: `project = KEY AND status in (active_statuses)`
* Changed since yesterday: `project = KEY AND updated >= -1d`
* Done since yesterday: `project = KEY AND status changed to (done_statuses) after -1d`
* Flagged or waiting: `project = KEY AND (Flagged is not EMPTY OR status in (waiting_statuses))`

If a query returns nothing for a team, record the team as clear rather than dropping it. Absence of data and a clear board are different states and leaders need to know which they are looking at.
