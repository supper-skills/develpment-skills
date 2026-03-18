# Workflow Examples

This document provides detailed workflow examples for the executing-plans skill, for Agent reference during execution.

---

## Example 1: Standard Execution

```
User: Execute the plan in design/plans/2024-01-15-auth.md

Agent:
1. Declare: "I am using the executing-plans skill to implement this plan."
2. 【Execution Phase 1/3】Currently executing: Load and Review Plan
3. Load plan from design/plans/2024-01-15-auth.md
4. Critically review plan - No concerns found
5. Create execution state file
6. Create todo list with 8 tasks
7. 【Execution Phase 2/3】Currently executing: Execute Tasks
8. Execute each task:
   - Task 1: Write test → Run → Fail ✓
   - Task 1: Write code → Run → Pass ✓
   - Task 2: Write test → Run → Fail ✓
   - ... (continue)
9. 【Execution Phase 3/3】Currently executing: Completion and Reporting
10. All tasks complete
11. Run final verification
12. Report completion with summary
```

---

## Example 2: Resume Execution

```
User: Continue executing the plan

Agent:
1. Declare: "I am using the executing-plans skill to continue implementing this plan."
2. Read execution state file: design/plans/2024-01-15-auth-execution-state.md
3. 【Execution Phase 2/3】Currently executing: Execute Tasks
   Current processing: Task 3 (of 8 tasks)
4. Execute task 3
5. Test unexpectedly fails
6. Stop and report:
   "Blocked on task 3: test requires 'lodash' but it's not installed.
    I should:
    a) Add lodash to dependencies
    b) Wait for you to install
    c) Modify the approach"
7. Update execution state file to record issue
8. Wait for guidance
```

---

## Example 3: Plan Concerns

```
User: Execute the plan in plans/feature-x.md

Agent:
1. Declare: "I am using the executing-plans skill to implement this plan."
2. 【Execution Phase 1/3】Currently executing: Load and Review Plan
3. Load plan
4. Review and find concerns:
   - File path references non-existent directory
   - Test command uses wrong framework
5. Update execution state file to record concerns
6. Stop and ask user:
   "I found issues in the plan:
    - Path 'src/lib/' does not exist. Should it be 'src/utils/'?
    - Plan uses 'jest' but project uses 'vitest'
    Should I continue and fix, or wait for plan revision?"
7. Wait for user guidance
```

---

## Example 4: Multi-Subsystem Execution

```
User: Execute the plan in design/plans/2024-01-15-feature-outline.md

Agent:
1. Declare: "I am using the executing-plans skill to implement this multi-subsystem plan."
2. Read outline file: design/plans/2024-01-15-feature-outline.md
3. Identified 3 subsystems: A (no dependency), B (depends on A), C (depends on A, B)
4. Create top-level execution state file
5. Create Subsystem A state file

Subsystem A Execution:
6. 【Execution Phase 0/3】Currently executing: Multi-Subsystem Handling
   - Subsystem A: 🔄 In Progress
7. 【Execution Phase 1/3】Currently executing: Load and Review Plan (Subsystem A)
8. Read Subsystem A plan: design/plans/2024-01-15-subsystem-a.md
9. Critically review plan - No concerns found
10. 【Execution Phase 2/3】Currently executing: Execute Tasks (Subsystem A)
11. Execute Subsystem A tasks 1-3
12. 【Execution Phase 3/3】Currently executing: Completion and Reporting (Subsystem A)
13. Mark Subsystem A complete ✅
14. Update top-level state file: Subsystem A ✅ Complete

Subsystem B Execution (depends on A):
15. Check dependency: Subsystem A ✅ Complete
16. 【Execution Phase 0/3】Currently executing: Multi-Subsystem Handling
   - Subsystem B: 🔄 In Progress
17. 【Execution Phase 1/3】Currently executing: Load and Review Plan (Subsystem B)
18. Read Subsystem B plan: design/plans/2024-01-15-subsystem-b.md
19. Critically review plan - No concerns found
20. 【Execution Phase 2/3】Currently executing: Execute Tasks (Subsystem B)
21. Execute Subsystem B tasks 4-6
22. 【Execution Phase 3/3】Currently executing: Completion and Reporting (Subsystem B)
23. Mark Subsystem B complete ✅
24. Update top-level state file: Subsystem B ✅ Complete

Subsystem C Execution (depends on A, B):
25. Check dependency: Subsystem A ✅ Complete, Subsystem B ✅ Complete
26. 【Execution Phase 0/3】Currently executing: Multi-Subsystem Handling
   - Subsystem C: 🔄 In Progress
27. 【Execution Phase 1/3】Currently executing: Load and Review Plan (Subsystem C)
28. Read Subsystem C plan: design/plans/2024-01-15-subsystem-c.md
29. Critically review plan - No concerns found
30. 【Execution Phase 2/3】Currently executing: Execute Tasks (Subsystem C)
31. Execute Subsystem C tasks 7-8
32. 【Execution Phase 3/3】Currently executing: Completion and Reporting (Subsystem C)
33. Mark Subsystem C complete ✅
34. Update top-level state file: Subsystem C ✅ Complete

All Subsystems Complete:
35. Run cross-subsystem integration tests
36. Generate final report
```

---

## Workflow Overview Diagram

```txt
┌─────────────────────────────────────────────────────────────────┐
│                        Execute Plans Workflow                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  [Multi-subsystem detection] ──→ Identify subsystem count, execute by dependency order │
│         │                                                       │
│         ▼                                                       │
│  Phase 1/3  Load and Review Plan ──→ Critical review, decision point │
│         │                                                       │
│         ▼                                                       │
│  Phase 2/3  Execute Tasks ──→ Task execution, progress persistence, recovery mechanism │
│         │                                                       │
│         ▼                                                       │
│  Phase 3/3  Completion and Reporting ──→ Final verification, completion report │
│                                                                 │
│  ─────────────────────────────────────────────────────────────  │
│                                                                 │
│  Multi-subsystem execution flow:                                │
│                                                                 │
│  Subsystem A ──→ Subsystem B ──→ Subsystem C                   │
│      │            │            │                               │
│      ▼            ▼            ▼                               │
│   Phase 1-3   Phase 1-3   Phase 1-3                            │
│      │            │            │                               │
│      ▼            ▼            ▼                               │
│   ✅ Complete   ✅ Complete   ✅ Complete                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```
