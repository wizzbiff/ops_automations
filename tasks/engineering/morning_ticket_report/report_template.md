# Report Template, the shared standard

The task generates the report in this exact shape. Ordering matters: what a leader reads first comes first. Keep the whole report under 500 words. Brevity is the standard. A report nobody finishes is a report nobody trusts.

Replace bracketed guidance with real content at generation time. Do not print the guidance.

---

# Engineering Morning Report, [Weekday, Month Day]

## Summary

[Two or three sentences. Headline numbers across all teams: how many active, how many blocked, how many closed since yesterday. Then the single most important thing a leader should know today. If everything is healthy, say so plainly.]

## Needs escalation

[The short list of items that need a leader to act, per the escalation rules in definitions.md. For each: team, issue key and title, why it is stuck, and the one action that would unblock it. If nothing qualifies, write "Nothing needs escalation today" and move on.]

## By team

[One compact block per team in config.md.]

### [Team name], [Manager]

* Active: [n]   Blocked: [n]   At risk: [n]   Closed since yesterday: [n]
* Blocked: [issue key, short title, one phrase on why. Omit the line if zero.]
* At risk: [issue key, short title, one phrase on the risk. Omit if zero.]
* Sprint health: [only if the team runs sprints in config: days left, percent of points remaining, on track or not. Omit otherwise.]

## Stale work

[Issues gone quiet, grouped by team, key and title only. The gentle nudge list. No commentary.]

## Needs review

[Anything that could not be classified, one line reason each. Omit the section if empty.]

---

## Tone

Follow standards/shared/style.md. It holds the tone and formatting rules shared by every report in this repo, so they are not repeated here.
