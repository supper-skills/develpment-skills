# Session State File Template

This template is used to track progress in multi-round dialogues and solve attention loss problems.

---

## File Path

```
design/.session-state.md
```

All skills share the same state file, updating by phase.

---

## Template

```markdown
# Session State

## Basic Information

- **Skill**: [brainstorming / writing-plan / executing-plans]
- **Topic**: [Feature name or task description]
- **Start Time**: YYYY-MM-DD HH:mm
- **Last Updated**: YYYY-MM-DD HH:mm

## Current State

- **Phase**: [Current phase name]
- **Last Step**: [Just completed content]
- **Next Step**: [Next step to execute]

## Confirmed Content

<!-- Record key decisions and information confirmed by user -->

- [Decision/Information 1]
- [Decision/Information 2]

## Pending Issues

<!-- Issues to ask user or resolve -->

- [ ] [Issue 1]
- [ ] [Issue 2]
```

---

## Usage Rules

### When to Create

Create when skill is activated, with path at `design/.session-state.md` under project root.

### When to Update

Update after each user confirmation or phase milestone completion.

### When to Restore

Read at the start of each dialogue round to restore context.

### On Skill Switch

Update the "Skill" field on skill switch, keep confirmed content, update current state.
