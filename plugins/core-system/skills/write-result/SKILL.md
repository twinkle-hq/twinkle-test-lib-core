---
name: write-result
description: "QA fixture skill. Points at the runner's twinkle:result skill, which is the one statement of task/result.md."
---

This fixture states nothing about `task/result.md`. Its format is declared once,
in `lib/protocol/result-contract.json`, and the runner renders the session's
`twinkle:result` skill from it — read that skill before you write the file.

This file exists so the smoke lane CAP-flows-22 has a seeded skill body to serve
by path; it must never grow a status name or a field of its own.
