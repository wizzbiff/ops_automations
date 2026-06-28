---
description: Scaffold a new automation task under an existing domain
---

Add a new task named $ARGUMENTS to an existing domain, following CONTRIBUTING.md and CLAUDE.md.

1. Confirm the target domain exists under standards/. If it does not, run /add_domain first. Tasks are grouped by domain: a task lives under tasks/<domain>/.
2. Copy tasks/_task_template/ to tasks/<domain>/$ARGUMENTS/.
3. Fill in task.md, the output template, and the README. Point the task at standards/shared/style.md and the domain's standard. Read config from the local config.md. Write output to output/$ARGUMENTS/ (output stays flat by task name, not nested by domain).
4. Replace every {{...}} and every bracketed placeholder. Leave none in the committed files.
5. List any new connectors in config/connectors.md.
6. Update the README task catalog, add a CHANGELOG entry, and set the item status in PROJECT_CONTEXT.md.
7. Run /check_repo, fix anything it flags, then commit on a new branch with a clear message.

Remember the build surface boundary: this scaffolds and commits the files. It does not run the automation. Tell me the artifacts are ready to install and test in Cowork.
