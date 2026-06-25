---
description: Verify repo consistency before committing
---

Run the consistency checks from CLAUDE.md and report results. Do not change files unless I ask.

1. grep the tree for references to standards/ and tasks/ paths and confirm each referenced file exists. Report any reference that points at a missing path.
2. Search committed standards and task logic for leftover {{...}} placeholders. Report any found.
3. Confirm no real config.md is tracked, and that nothing under config/ except config.example.md and connectors.md is staged.
4. Confirm the README task catalog and CHANGELOG match the current set of tasks and domains in the tree.
5. Confirm identifiers use underscores, with no hyphenated file or folder names introduced.

Report each check as pass, or list the specific files that fail. End with a one line verdict: ready to commit, or not yet.
