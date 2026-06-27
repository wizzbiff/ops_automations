# Weekly Rollup Template, the shared standard

The task generates the rollup in this exact shape. Ordering matters: what a leader reads first comes first. Keep the whole rollup under 600 words. Brevity is the standard. A rollup nobody finishes is a rollup nobody trusts.

Replace bracketed guidance with real content at generation time. Do not print the guidance.

---

# Engineering Weekly Rollup, week ending [Weekday, Month Day]

## Summary

[Two or three sentences. Headline flow numbers across all teams: done this week, net new, and how many are blocked, at risk, or stale, each with its trend arrow against last week where there is one. Then the single most important thing leadership should know this week. If there is no prior week, say "no prior week to compare" here and drop the arrows. If everything is healthy and flowing, say so plainly.]

## Risks needing leadership action

[The short list of items and teams that need a leader to act, per the weekly escalation lens in flow.md: persistent blockers blocked all week, items tied to a slipping delivery date, and teams trending worse. For each: team, the issue key and title or the measure, why it needs attention, and the one action that would change it. If nothing qualifies, write "Nothing needs leadership action this week" and move on.]

## Flow by team

[One compact block per team in config.md.]

### [Team name], [Manager]

* Done: [n] ([trend])   Net new: [n]   Avg cycle time: [n days or "no completions"] ([trend])
* Risk: Blocked [n] ([trend])   At risk [n]   Stale [n]
* Oldest in flight: [key, short title, age in days. Omit the line if nothing is aging.]
* Persistent blocker: [key, short title, one phrase on why, if anything was blocked all week. Omit if none.]
* Sprint health: [only if the team runs sprints in config: days left, percent of points remaining, on track or not. Omit otherwise.]

## Aging and stale work

[In-flight work getting old and work gone quiet, grouped by team, key and title and age only. The nudge list. No commentary.]

## Net new and unplanned

[Work that entered the active bucket mid-week, grouped by team, key and title only. Signals unplanned load. Omit the section if there was none.]

## Needs review

[Anything that could not be classified, one line reason each. Omit the section if empty.]

---

## Tone

Follow standards/shared/style.md. It holds the tone and formatting rules shared by every report in this repo, so they are not repeated here.
