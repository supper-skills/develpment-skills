# Workflow Examples

Flowcharts and examples to help understand the complete plan writing process.

---

## Table of Contents

- [Workflow Overview Diagram](#workflow-overview-diagram)
- [Multi-Subsystem Handling Flowchart](#multi-subsystem-handling-flowchart)
- [Workflow Examples](#workflow-examples)
- [Common Issue Handling](#common-issue-handling)

---

## Workflow Overview Diagram

```txt
┌─────────────────────────────────────────────────────────────────┐
│                      Plan Writing Workflow                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1/7 Context and Scope Analysis ──→ Create outline, identify subsystems, record decisions    │
│         │                                                       │
│         ▼                                                       │
│  2/7 File Structure Planning ──→ Plan new/modify/test files    │
│         │                                                       │
│         ▼                                                       │
│  3/7 Plan Document Title ──→ Write goal, architecture, tech stack │
│         │                                                       │
│         ▼                                                       │
│  4/7 Task Definition ──→ Define TDD tasks, write code snippets │
│         │                                                       │
│         ▼                                                       │
│  5/7 Chunking Output and Review ──→ Chunk output, multi-level review │
│         │                                                       │
│         ▼                                                       │
│  6/7 Plan Save and Confirmation ──→ Save plan, final review, user confirmation    │
│         │                                                       │
│         ▼                                                       │
│  7/7 Execution Handover ──→ Ask execution intent, invoke executing-plans      │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Multi-Subsystem Handling Flowchart

```txt
┌─────────────────────────────────────────────────────────────────┐
│                  Multi-Subsystem Handling Flow                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Identify subsystems ──→ Analyze dependency relationships        │
│         │                                                         │
│         ▼                                                         │
│  Enhance outline file ──→ Record subsystems, dependencies, execution order, decisions   │
│         │                                                         │
│         ▼                                                         │
│  ┌─────────────────────────────────────────┐                   │
│  │  Loop: Process subsystems one by one     │                   │
│  │                                           │                   │
│  │  Read outline ──→ Confirm dependencies satisfied│             │
│  │       │                                 │                   │
│  │       ▼                                 │                   │
│  │  Write subsystem plan ──→ Chunk output   │                   │
│  │       │                                 │                   │
│  │       ▼                                 │                   │
│  │  Chunk review ──→ Subsystem review      │                   │
│  │       │                                 │                   │
│  │       ▼                                 │                   │
│  │  Update outline status ──→ Record decisions│                │
│  │       │                                 │                   │
│  │       ▼                                 │                   │
│  │  Still have subsystems?──yes──→ Continue loop│              │
│  │       │                                 │                   │
│  │       no                                │                   │
│  └───────┼─────────────────────────────────┘                   │
│           │                                                     │
│           ▼                                                     │
│  Save all plans ──→ Final review                                │
│         │                                                         │
│         ▼                                                         │
│  User confirms plan ──→ Ask execution intent                    │
│         │                                                         │
│         ▼                                                         │
│  User chooses to execute?──yes──→ Invoke executing-plans        │
│         │                                                         │
│         no                                                        │
│         │                                                         │
│         ▼                                                         │
│    End this skill                                                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Workflow Examples

### Example 1: Single Subsystem Project

```
User: I need to implement user authentication using JWT tokens. Here's my specification...

Agent:
1. Declare: "I am using the writing-plan skill to create an implementation plan."
2. 【Phase 1/7】Create outline file, confirm single subsystem
3. Record decision: Choose JWT solution | Rationale: Stateless, easy to scale
4. Ask save location (default: design/plans/)
5. 【Phase 2/7】Plan file structure
6. 【Phase 3/7】Write plan title
7. 【Phase 4/7】Reference "Authentication Module" pattern, write tasks
8. 【Phase 5/7】Chunk output, review each chunk
9. 【Phase 6/7】Save plan, final review, ask user to confirm plan
10. 【Phase 7/7】Ask execution intent
    - User selects "Execute now" → Invoke executing-plans skill
    - User selects "Execute later" → End this skill
```

### Example 2: Multi-Subsystem Project

```
User: I need to build an e-commerce system with user management, product management, order management. Here's my specification...

Agent:
1. Declare: "I am using the writing-plan skill to create an implementation plan."
2. 【Phase 1/7】Create outline file
3. Identify 3 subsystems: User management, Product management, Order management
4. Analyze dependencies: Orders depend on users and products
5. Record decision: Microservices architecture | Rationale: Independent deployment, flexible tech stack
6. Enhance outline file, record execution order
7. 【Phase 2-5/7】Process Subsystem A (User management):
   - Read outline to confirm no dependencies
   - Reference "CRUD Module" pattern
   - Plan file structure
   - Write plan
   - Chunk review → Subsystem review
   - Update outline status, record decisions
8. 【Phase 2-5/7】Process Subsystem B (Product management):
   - Read outline to confirm no dependencies
   - Plan file structure
   - Write plan
   - Chunk review → Subsystem review
   - Update outline status
9. 【Phase 2-5/7】Process Subsystem C (Order management):
   - Read outline to confirm A, B completed
   - Plan file structure (reference shared components from A, B)
   - Write plan
   - Chunk review → Subsystem review
   - Update outline status
10. 【Phase 6/7】Save all plans, final review, ask user to confirm plans
11. 【Phase 7/7】Ask execution intent
    - User selects "Execute now" → Invoke executing-plans skill
    - User selects "Execute later" → End this skill
```

### Example 3: Change Handling

```
User: I need to add a cache layer to user management.

Agent:
1. Register change: Add cache layer | Impact scope: User management | Reason: Performance optimization
2. Impact analysis:
   - Directly impacted: User query tasks
   - Indirectly impacted: API response time
3. Record decision: Use Redis | Rationale: High performance, supports expiration
4. Update plan documents:
   - Add cache configuration task
   - Modify user query tasks
5. Change review
6. Notify user: Change complete, impact on user management module
```

---

## Common Issue Handling

### Q: What if the specification document is too large?

Handling:

1. Identify subsystem boundaries in Phase 1
2. Enhance outline file to decompose project
3. Process subsystems one by one
4. Each subsystem independently undergoes plan writing

### Q: What if there are complex dependencies between subsystems?

Handling:

1. Record dependency relationships in detail in outline file
2. Determine correct execution order
3. Define shared components in the earliest using subsystem
4. Subsequent subsystems reference already-defined shared components

### Q: How to resume after conversation interruption?

Handling:

1. Read outline file `design/plans/YYYY-MM-DD-<topic>-outline.md`
2. Check "Decision Records" to understand decisions already made
3. Declare current phase
4. Continue based on "Next Action" in "Session State"

### Q: What if user requests modification of completed parts?

Handling:

1. Execute change management process
2. Conduct impact analysis
3. Update related plan documents
4. Update outline file to record changes and decisions
5. Conduct change review

### Q: How to avoid repeated discussion of already decided issues?

Handling:

1. At the start of each conversation, read "Decision Records" in outline file
2. When encountering related issues, first check if there's already a decision
3. If there's a decision, reference decision record and explain rationale
4. If decision needs modification, handle through change management process
