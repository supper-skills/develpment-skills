# FAQ

This document provides guidance on handling common issues during the brainstorming phase.

---

## Q: User insists on skipping design and proceeding directly to implementation?

Response:

> "I understand you want to move quickly. However, according to the process, the design document can be very brief (just a few sentences for simple projects), but it must be documented and approved by you. This ensures we have shared understanding of the goals and avoids rework later."

---

## Q: Project scope is too large?

Handling:

1. Mark as multi-subsystem project
2. Help user decompose into independent subprojects
3. Start brainstorming with the first subproject
4. Each subproject independently undergoes the spec → plan → implement cycle

---

## Q: How to resume after conversation interruption?

Handling:

1. Read state file `design/specs/YYYY-MM-DD-<topic>-state.md`
2. Declare current phase
3. Continue based on "Next Action" in the state file

---

## Q: Review loop exceeds 5 iterations?

Escalation:

1. Summarize all issues found across iterations
2. Document attempted solutions
3. Identify specific points of disagreement
4. Submit to human for guidance with complete context
