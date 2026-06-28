---
description: Scaffold a new operational domain
---

Add a new domain named $ARGUMENTS, following CONTRIBUTING.md and CLAUDE.md.

1. Create standards/$ARGUMENTS/ and write its definitions there. Reuse standards/shared/style.md for tone. Do not restate it.
2. Tasks are grouped by domain under tasks/<domain>/<task>/, mirroring standards/. Place this domain's tasks under tasks/<domain>/. Output stays flat at output/<task>/.
3. Add the domain's first task with /add_task.
4. Update the README catalog with the new domain and its tasks, add a CHANGELOG entry, and update the roadmap status in PROJECT_CONTEXT.md.
5. Run /check_repo, fix anything it flags, then commit on a new branch.

Nothing in an existing domain should change as a result of adding this one. If something does, stop and explain why.
