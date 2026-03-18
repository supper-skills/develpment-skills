# Quality Checklist

Use this checklist for final inspection before Phase 6 user confirmation of the plan.

---

## Table of Contents

- [Plan Completeness](#plan-completeness)
- [Task Quality](#task-quality)
- [Chunk Quality](#chunk-quality)
- [Scope Verification](#scope-verification)
- [Outline File Verification](#outline-file-verification)
- [Review Verification](#review-verification)
- [Key Principles Quick Reference](#key-principles-quick-reference)

---

## Plan Completeness

- [ ] Plan title complete, includes goal, architecture, tech stack
- [ ] File structure recorded before tasks
- [ ] All file paths precise and clear
- [ ] All code snippets complete (not placeholders)
- [ ] All commands precise with expected output

---

## Task Quality

- [ ] Each task has clear file references (create/modify/test)
- [ ] Each step granularity moderate (2-5 minutes)
- [ ] Tests precede implementation
- [ ] Each task independently testable

---

## Chunk Quality

- [ ] Each chunk 300-500 lines and logically self-contained
- [ ] Inter-chunk dependencies clear
- [ ] No isolated references to other chunks

---

## Scope Verification

- [ ] Plan covers single cohesive feature/subsystem
- [ ] If multiple subsystems, outline file completely filled
- [ ] Inter-subsystem dependency relationships recorded

---

## Outline File Verification

- [ ] Outline file created and updated
- [ ] Session state information complete
- [ ] Decision records complete
- [ ] Change history updated (if changes occurred)
- [ ] All subsystem progress recorded (if applicable)

---

## Review Verification

- [ ] All chunks passed chunk-level review
- [ ] All subsystems passed subsystem review (if applicable)
- [ ] Final review completed

---

## Key Principles Quick Reference

| Principle | Description |
|-----------|-------------|
| Unified Outline | Use outline file to uniformly manage session state, decision records, project information |
| Traceable Decisions | All important decisions recorded to prevent repeated discussion |
| Controllable Changes | Changes undergo impact analysis and review to ensure consistency |
| Pattern Reuse | Common scenarios use predefined patterns to improve efficiency |
| Multi-Level Review | Chunk-level, subsystem-level, final review ensures quality |
| Phase Declaration | Declare current phase at start of each conversation |
| Chunked Output | Each chunk 300-500 lines, logically self-contained |
| Process One by One | Process subsystems one by one, update outline after completion |
| Precise and Complete | Precise paths, complete code, precise commands |
| Test First | Each implementation step followed by test |
| Language Adaptation | All examples use project programming language |
