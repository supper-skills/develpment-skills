# Session State File Template

This template is used to track progress in multi-round conversations, solving the attention loss problem.

---

## File Path

```
design/.session-state.md
```

All skills share the same state file, updated by phase.

---

## Template

```markdown
# Session State

## Basic Information

- **Skill**: [brainstorming / writing-plan / executing-plans]
- **Topic**: [Feature name or task description]
- **Start Time**: YYYY-MM-DD HH:mm
- **Last Updated**: YYYY-MM-DD HH:mm

## Current Status

- **Phase**: [Current phase name]
- **Previous Step**: [Content just completed]
- **Next Step**: [Next step to execute]

## Confirmed Content

<!-- Record key decisions and information confirmed by user -->

- [Decision/Information 1]
- [Decision/Information 2]

## Pending Issues

<!-- Issues that need to be asked to user or resolved -->

- [ ] [Issue 1]
- [ ] [Issue 2]
```

---

## Usage Rules

### Creation Timing

Create when skill activates, path is `design/.session-state.md` under project root.

### Update Timing

Update after each user confirmation or phase completion.

### Recovery Timing

Read at the start of each conversation round to restore context and continue.

### During Skill Transitions

When transitioning between skills, update the "Skill" field, preserve confirmed content, and update current status.
