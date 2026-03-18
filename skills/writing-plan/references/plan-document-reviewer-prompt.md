# Plan Document Reviewer Prompt

This document provides guidance for reviewing implementation plans, including phase reviews and chunk reviews.

---

## Table of Contents

- [Review Purpose](#review-purpose)
- [Review Trigger Matrix](#review-trigger-matrix)
- [Scope Review Checklist (Phase 1)](#scope-review-checklist-phase-1)
- [Structure Review Checklist (Phase 2)](#structure-review-checklist-phase-2)
- [Task Review Checklist (Phase 4)](#task-review-checklist-phase-4)
- [Chunk-Level Review Checklist](#chunk-level-review-checklist)
- [Subsystem Review Checklist](#subsystem-review-checklist)
- [Final Review Checklist](#final-review-checklist)
- [Change Review Checklist](#change-review-checklist)
- [Review Output Format](#review-output-format)
- [Review Guidance](#review-guidance)
- [Common Issues to Watch For](#common-issues-to-watch-for)
- [Escalation](#escalation)
- [Review Flowchart](#review-flowchart)
- [Quick Checklist](#quick-checklist)

---

## Review Purpose

Ensure plans meet quality standards at all phases, identify issues early, and avoid rework.

---

## Review Trigger Matrix

| Trigger Point | Review Type | Review Scope | Review Focus | Review Method |
|--------------|-------------|-------------|-------------|--------------|
| Phase 1 complete | Scope Review | Subsystem identification, dependency relationships | Subsystem division, execution order, decision reasonableness | User confirmation |
| Phase 2 complete | Structure Review | File structure | Structure reasonableness, clear responsibilities, pattern consistency | User confirmation |
| Phase 4 complete | Task Review | Task definition | Task completeness, granularity, TDD process | User confirmation |
| Each chunk complete | Chunk Review | Current chunk | Code completeness, test coverage, precise paths | Sub-agent review |
| Subsystem complete | Subsystem Review | Entire subsystem | Overall consistency, dependency satisfaction, shared components | Sub-agent review |
| All complete | Final Review | All plans | Overall quality, execution order, outline completeness | User confirmation |
| Change occurs | Change Review | Change impact scope | Impact analysis, dependency update, consistency | Sub-agent review |

---

## Scope Review Checklist (Phase 1)

### 1. Subsystem Identification Verification

- [ ] Is subsystem division reasonable?
- [ ] Are there missing or redundant subsystems?
- [ ] Are subsystem boundaries clear?
- [ ] Do subsystem identification criteria meet requirements?

### 2. Dependency Relationship Verification

- [ ] Are dependency relationships correct?
- [ ] Is execution order reasonable?
- [ ] Are there circular dependencies?
- [ ] Is dependency analysis complete?

### 3. Decision Reasonableness Verification

- [ ] Is technology selection appropriate?
- [ ] Are architecture decisions justified?
- [ ] Are decisions recorded in outline file?
- [ ] Are decision impact scopes clear?

### 4. Outline File Completeness

- [ ] Is session state complete?
- [ ] Is project overview clear?
- [ ] Is subsystem division recorded?
- [ ] Is execution order recorded?

---

## Structure Review Checklist (Phase 2)

### 1. Structure Reasonableness Verification

- [ ] Does file division follow single responsibility principle?
- [ ] Is file size moderate (context friendly)?
- [ ] Are file names clear?
- [ ] Is directory structure reasonable?

### 2. Responsibility Clarity Verification

- [ ] Is each file's responsibility clear?
- [ ] Are there responsibility overlaps between files?
- [ ] Are there missing files?
- [ ] Do test files correspond to source files?

### 3. Pattern Consistency Verification

- [ ] Does it follow existing codebase patterns?
- [ ] Are new/modify/test files clearly separated?
- [ ] Do file extensions match project language?
- [ ] Are shared components marked if any?

---

## Task Review Checklist (Phase 4)

### 1. Task Completeness Verification

- [ ] Do tasks cover all functional points?
- [ ] Are there missing tasks?
- [ ] Is task order reasonable?
- [ ] Do tasks correspond to file structure?

### 2. Task Granularity Verification

- [ ] Can each step be completed in 2-5 minutes?
- [ ] Are tasks too complex and need splitting?
- [ ] Are tasks too simple and need merging?
- [ ] Is step division reasonable?

### 3. TDD Process Verification

- [ ] Does each task start with testing?
- [ ] Do tests cover key scenarios?
- [ ] Is implementation minimal?
- [ ] Are test commands precise?

### 4. Code Quality Verification

- [ ] Are code snippets complete and runnable?
- [ ] Are commands precise?
- [ ] Are file paths accurate?
- [ ] Do code examples use project programming language?

---

## Chunk-Level Review Checklist

### 1. Title Completeness

- [ ] Plan has required title with goal, architecture, tech stack
- [ ] Goal is a clear one-sentence statement
- [ ] Architecture provides 2-3 sentences about approach
- [ ] Tech stack lists key technologies/libraries
- [ ] If subsystem plan, has outline file path reference

### 2. File Structure

- [ ] File structure recorded before tasks
- [ ] All file paths precise and clear
- [ ] New files, modify files, and test files clearly separated
- [ ] Each file has clear responsibility description
- [ ] File extensions match project programming language
- [ ] Shared components marked with using subsystems if any

### 3. Task Quality

- [ ] Each task has clear file references (create/modify/test)
- [ ] Each step has moderate granularity (2-5 minutes per step)
- [ ] Tests precede implementation (TDD approach)
- [ ] Each task is independently testable

### 4. Code Completeness

- [ ] All code snippets complete (not placeholders)
- [ ] No vague instructions like "add validation"
- [ ] Code syntax is correct
- [ ] Code follows language conventions
- [ ] Code examples use project's programming language

### 5. Command Precision

- [ ] All commands precise and runnable
- [ ] Expected output recorded
- [ ] Test commands specify exact test name/path
- [ ] Commands suit project's language/framework

### 6. Chunk Quality

- [ ] Chunk within 300-500 lines
- [ ] Chunk is logically self-contained
- [ ] No isolated references to other chunks
- [ ] Tasks within chunk have clear logical relationship

---

## Subsystem Review Checklist

### 1. Overall Consistency Check

- [ ] Is file structure complete?
- [ ] Do tasks cover all functional points?
- [ ] Is testing sufficient?
- [ ] Have all chunks passed chunk-level review?

### 2. Dependency Satisfaction Check

- [ ] Are dependent subsystems completed?
- [ ] Are shared components defined?
- [ ] Do interfaces match?
- [ ] Are dependency relationships recorded in outline file?

### 3. Shared Component Check

- [ ] Are shared components defined in the earliest using subsystem?
- [ ] Do subsequent subsystems correctly reference shared components?
- [ ] Are shared component interfaces clear?
- [ ] Do shared components have independent tests?

### 4. Outline File Consistency

- [ ] Do subsystem scope and outline description match?
- [ ] Are dependency relationships correct?
- [ ] Are shared component locations correct?
- [ ] Does execution order follow dependency relationships?

---

## Final Review Checklist

### 1. Overall Quality Check

- [ ] Are all plan documents complete?
- [ ] Have all chunks passed review?
- [ ] Are all decisions recorded?

### 2. Execution Order Verification

- [ ] Are dependency relationships correct?
- [ ] Is execution order reasonable?
- [ ] Are there circular dependencies?

### 3. Outline Completeness Check

- [ ] Is session state complete?
- [ ] Are decision records complete?
- [ ] Is change history updated?
- [ ] Are all subsystem progress recorded?

### 4. Multi-Subsystem Project Check

- [ ] Have all subsystem plans completed?
- [ ] Are inter-subsystem dependency relationships correct?
- [ ] Are shared component definitions complete?
- [ ] Is execution order clear?

---

## Change Review Checklist

### 1. Change Completeness

- [ ] Has change been recorded in outline file "Change History"?
- [ ] Is change impact analysis complete?
- [ ] Have impacted tasks been updated?

### 2. Impact Analysis Verification

- [ ] Are directly impacted tasks completely identified?
- [ ] Are indirectly impacted tasks completely identified?
- [ ] Are impacted subsystems completely identified?

### 3. Consistency Check

- [ ] Is updated plan consistent with other plans?
- [ ] Are dependency relationships still correct?
- [ ] Are shared component references correct?

### 4. New Decision Records

- [ ] Have new decisions related to change been recorded?
- [ ] Are decision rationales sufficient?
- [ ] Are impact scopes clear?

---

## Review Output Format

After review, provide output in the following format:

```markdown
## Review Result: [✅ Approved / ❌ Issues Found]

### Review Type
[Scope Review / Structure Review / Task Review / Chunk-Level Review / Subsystem Review / Final Review / Change Review]

### Summary
[Review brief summary]

### Issues Found (if any)
1. [Issue description]
   - Location: [Specific section/line]
   - Suggestion: [How to fix]

### Strengths
- [What's done well]

### Suggestions
- [Optional improvements]
```

---

## Review Guidance

1. **Thorough but Fair** - Focus on issues that would block execution
2. **Explain Why** - When marking issues, explain why they matter
3. **Constructive** - Provide specific suggestions
4. **Consider Context** - Plans are for engineers unfamiliar with the codebase
5. **Value Precision** - Vague plans lead to execution failures
6. **Language Awareness** - Ensure examples match project programming language
7. **Chunk Awareness** - Ensure each chunk can be independently understood and executed
8. **Decision Consistency** - Check consistency with decision records in outline file
9. **Identify Issues Early** - The purpose of phase reviews is to identify issues early and avoid rework

---

## Common Issues to Watch For

### Vague Instructions

❌ Incorrect: "Add error handling"
✅ Correct: "Add try-except block, catch ValueError and return ErrorResult"

### Missing Test Steps

❌ Incorrect: Implementation step without preceding test
✅ Correct: Test step → Run test (fail) → Implement → Run test (pass)

### Imprecise Paths

❌ Incorrect: "Update configuration file"
✅ Correct: "Modify: `src/config/settings.py:45-52`"

### Placeholder Code

❌ Incorrect: "// Implement logic here"
✅ Correct: Complete, runnable code snippet

### Wrong Language Examples

❌ Incorrect: Python examples in TypeScript project
✅ Correct: TypeScript examples match project language

### Chunk Too Large

❌ Incorrect: Single chunk exceeds 500 lines
✅ Correct: Split chunk into smaller logical units

### Cross-Chunk Dependencies Undocumented

❌ Incorrect: Chunk references components from other chunks without explanation
✅ Correct: Clearly mark dependency relationships and reference locations

### Decisions Unrecorded

❌ Incorrect: Made technical decisions in plan but not recorded in outline file
✅ Correct: Record decisions in outline file "Decision Records" table

### Changes Untracked

❌ Incorrect: Modified plan but not recorded in outline file
✅ Correct: Record changes in outline file "Change History" table

### Subsystem Identification Errors

❌ Incorrect: Combined features that should be split into one subsystem
✅ Correct: Identify subsystems by independent data models, independent interfaces, independent deployment standards

### Unclear File Responsibilities

❌ Incorrect: One file takes on multiple unrelated responsibilities
✅ Correct: Each file has a single clear responsibility

---

## Escalation

If the same review loop exceeds 5 iterations, escalate to human guidance with:

1. Issue summary
2. Attempted methods
3. Specific areas of disagreement

---

## Review Flowchart

```txt
┌─────────────────────────────────────────────────────────────────┐
│                        Review Flow                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Phase 1 complete ──→ Scope Review (User confirmation)          │
│         │                                                         │
│         ▼                                                         │
│  Phase 2 complete ──→ Structure Review (User confirmation)       │
│         │                                                         │
│         ▼                                                         │
│  Phase 3 complete ──→ Skip (Simple content)                      │
│         │                                                         │
│         ▼                                                         │
│  Phase 4 complete ──→ Task Review (User confirmation)            │
│         │                                                         │
│         ▼                                                         │
│  Phase 5 in progress ──→ Chunk Review (Sub-agent)              │
│         │                                                         │
│         ▼                                                         │
│  Subsystem complete ──→ Subsystem Review (Sub-agent)             │
│         │                                                         │
│         ▼                                                         │
│  Phase 6 complete ──→ Final Review (User confirmation)           │
│         │                                                         │
│         ▼                                                         │
│  Change occurs ──→ Change Review (Sub-agent)                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Quick Checklist

| Check Item | Standard | Priority | Review Type |
|-----------|----------|---------|-------------|
| Subsystem division | Reasonable, no omissions | High | Scope |
| Dependency relationships | Correct, no cycles | High | Scope |
| Decision reasonableness | Justified | High | Scope |
| File structure | Single responsibility | High | Structure |
| Responsibility clarity | No overlaps | High | Structure |
| Task completeness | Covers functionality | High | Task |
| Task granularity | 2-5 minutes | Medium | Task |
| TDD process | Test first | High | Task |
| Title completeness | Goal, architecture, tech stack | High | Chunk |
| File paths precise | No vague references | High | Chunk |
| Code complete | No placeholders | High | Chunk |
| Commands precise | Directly runnable | High | Chunk |
| Chunk size | 300-500 lines | Medium | Chunk |
| Language match | Consistent with project | Medium | Chunk |
| Dependency satisfaction | Dependencies completed | High | Subsystem |
| Shared components | Definitions complete | High | Subsystem |
| Outline consistency | Information consistent | Medium | Subsystem |
| Decision records | Recorded | Medium | Final |
| Change history | Updated | Medium | Change |
