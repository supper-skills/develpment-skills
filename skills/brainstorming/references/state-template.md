# State File Template

This document provides the template structure for brainstorming session state files, used to solve the attention loss problem in multi-round conversations.

---

## State File Path

```
design/specs/YYYY-MM-DD-<topic>-state.md
```

---

## Complete Template

```markdown
# Brainstorming Session State

## Metadata

- **Session Topic**: [Brief requirement description]
- **Created**: YYYY-MM-DD HH:mm
- **Last Updated**: YYYY-MM-DD HH:mm

## Current Phase

Phase X/8: [Phase Name]

## Confirmed Specifications

<!-- Content explicitly confirmed by user -->

### Goal Positioning

- ...

### Constraints

- ...

### Success Criteria

- ...

## Pending Decisions

<!-- Questions queue to ask user -->

1. [ ] Question 1
2. [ ] Question 2

## Decisions Made

<!-- Record all decisions and their rationale -->

- Decision: ... | Rationale: ...

## Next Action

[Specific action description]
```

---

## Usage Instructions

### At the Start of Each Conversation Round

1. Read the state file
2. Restore context based on state file
3. Declare current phase

### After Each User Confirmation

1. Update the state file
2. Check if can proceed to next phase
