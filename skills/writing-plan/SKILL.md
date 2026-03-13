---
name: writing-plan
description: Implementation plan creation skill for multi-step tasks. Use this skill BEFORE touching any code when you have specifications or requirements. Creates comprehensive implementation plans assuming engineers have zero knowledge of the codebase. Triggers when users mention "create plan", "implementation plan", "write plan", "planning", "task breakdown", or when starting complex multi-step development work with existing specs.
license: MIT
metadata:
  version: "1.0.0"
---

# Writing Plan Skill

This skill creates comprehensive implementation plans for multi-step development tasks. Use this BEFORE directly touching any code when you have specifications or requirements.

## Trigger Conditions

Activate this skill proactively when:

- User mentions "create plan", "implementation plan", "write plan"
- User mentions "task breakdown", "break down tasks", "decompose tasks"
- Starting complex multi-step development work with existing specifications
- User provides requirements/specifications and wants to plan before implementation
- User asks for detailed steps to implement a feature
- If brainstorming is also triggered, prioritize brainstorming skill

### Called by Other Skills

When called by brainstorming skill:

1. Receives parameter: specification document path
2. Skips trigger condition check
3. Proceeds directly to Phase 1

---

## Core Principles

### Start Declaration

Always begin by declaring:

> "I am using the writing-plan skill to create an implementation plan."

### Target Audience Assumptions

Assume the engineer reading this plan:

- Has **zero knowledge** of our codebase
- Has **questionable taste** in software design
- Is a **skilled developer** but unfamiliar with our toolset or problem domain
- Is **not well-versed** in good test design

Your plan must document everything they need to know.

### Core Values

- **DRY** (Don't Repeat Yourself) - No redundant information
- **YAGNI** (You Aren't Gonna Need It) - Only implement what's needed
- **TDD** (Test-Driven Development) - Write tests first
- **Frequent Commits** - Commit after each working step

---

## Phase 1: Context and Scope Analysis

### 1.1 Context Setup

This skill should run in a dedicated working tree (created by brainstorming skill if available).

### 1.2 Scope Check

**Critical**: Before proceeding, evaluate if the specification covers multiple independent subsystems.

If the specification spans multiple independent subsystems:

1. **Stop and recommend splitting** into separate sub-project specifications
2. Each plan should produce runnable, testable files
3. Each subsystem gets its own plan

If not split, suggest decomposition into independent plans - one per subsystem.

### 1.3 Ask for Save Location

Ask the user where to save the plan:

- Default directory: `design/plans/`
- File name format: `YYYY-MM-DD-<feature-name>.md`

Always inform the user of the default directory as an option.

---

## Phase 2: File Structure Planning

**Before defining tasks**, plan which files will be created or modified and their responsibilities.

### 2.1 Design Principles

Design units with clear boundaries and well-defined interfaces:

- **Single Responsibility**: Each file should have one clear responsibility
- **Context-Friendly**: Code that can be understood in one context window
- **Focused Files**: Prefer small, focused files over large, multi-function files
- **Co-location**: Files that change together should be placed together
- **Split by Responsibility**: Organize by responsibility, not by technical layer

### 2.2 Existing Codebase Patterns

In existing codebases:

- Follow established patterns
- Don't unilaterally refactor large files
- If modifying a bloated file, **ask the developer** whether to include splitting in the plan
- Only add file splitting to the plan after receiving explicit confirmation from the developer

### 2.3 File Structure Template

Document the planned file structure (adapt file extensions to the project's language):

```markdown
## File Structure

### New Files
- `path/to/new/file.<ext>` - Description of responsibility
- `path/to/another/file.<ext>` - Description of responsibility

### Modified Files
- `path/to/existing/file.<ext>` - What will be modified
- `path/to/another/existing.<ext>` - What will be modified

### Test Files
- `tests/path/to/test_file.<ext>` - Test responsibilities
```

---

## Phase 3: Plan Document Header

Every plan must start with this header:

```markdown
# [Feature Name] Implementation Plan

> **For agentic workers:** REQUIRED: Use executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

---

## Phase 4: Task Definition

### 4.1 Task Granularity

Each step should correspond to **one operation** (taking 2-5 minutes):

- "Write failing test" - one step
- "Run test to confirm failure" - one step
- "Run test and ensure pass" - one step

### 4.2 Task Structure Template

Each task follows this structure. Adapt the code examples and test commands to the project's programming language:

```markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.<ext>`
- Modify: `exact/path/to/existing.<ext>#L123-145`
- Test: `tests/exact/path/to/test.<ext>`

- [ ] **Step 1: Write the failing test**

```<language>
// Example: TypeScript
describe('functionName', () => {
  it('should return expected result for given input', () => {
    const result = functionName(input);
    expect(result).toBe(expected);
  });
});
```

- [ ] **Step 2: Run test to verify it fails**

Run: `<test-command>` (e.g., `npm test`, `pytest`, `cargo test`)
Expected: FAIL with appropriate error message

- [ ] **Step 3: Write minimal implementation**

```<language>
// Minimal implementation to pass the test
export function functionName(input: InputType): OutputType {
  return expected;
}
```

- [ ] **Step 4: Run test to verify it passes**

Run: `<test-command>`
Expected: PASS

### 4.3 Language-Specific Test Commands

Common test commands by language:

| Language | Test Framework | Command |
|----------|---------------|---------|
| TypeScript/JavaScript | Jest | `npm test` or `jest tests/path/test.ts` |
| TypeScript/JavaScript | Vitest | `vitest run tests/path/test.ts` |
| Python | pytest | `pytest tests/path/test.py::test_name -v` |
| Rust | cargo test | `cargo test test_name` |
| Go | go test | `go test ./path/to/package -run TestName` |
| Java | JUnit | `mvn test -Dtest=TestClassName` |
| C# | xUnit/NUnit | `dotnet test --filter TestName` |

### 4.4 Task Requirements

- **Exact file paths** - No vague references
- **Complete code in plan** - Not "add validation" but actual code
- **Precise commands** - Exact commands with expected output
- **Test-first approach** - Every task starts with a failing test
- **Language-appropriate** - Use the project's programming language for all examples

---

## Dependency Management Planning

Must explicitly define dependency management strategy in the plan to ensure smooth implementation.

### Dependency Identification

**Types of dependencies to identify:**

| Dependency Type | Description | Examples |
|-----------------|-------------|----------|
| Runtime Dependencies | Packages required for application to run | `express`, `lodash`, `axios` |
| Development Dependencies | Packages only needed in development environment | `typescript`, `jest`, `eslint` |
| Peer Dependencies | Packages that need to be provided by consumers | `react`, `vue` |
| Optional Dependencies | Non-essential but enhancing packages | Profiling tools, debugging tools |

### Dependency Installation Plan

Include the following in the plan:

```markdown
### Prerequisites: Dependency Installation

**New Dependencies:**
- `package-name@version` - Purpose description
- `another-package@^1.2.0` - Purpose description

**Installation Commands:**
- [ ] Install runtime dependencies
  Run: `pnpm add package-name@version`
  Expected: Dependency added to package.json and installed successfully

- [ ] Install development dependencies
  Run: `pnpm add -D dev-package@version`
  Expected: Dependency added to devDependencies and installed successfully
```

### Version Management Strategy

**Version Locking Principles:**

- Use exact versions or locked ranges for production dependencies
- Use looser ranges (`^` or `~`) for development dependencies
- Document reasons for choosing specific versions

**Version Compatibility Checks:**

- Check compatibility of new dependencies with existing ones
- Identify potential version conflicts
- Document solutions for conflicts

---

## Environment Configuration Planning

Define configuration strategies for different environments to ensure code runs correctly in each.

### Environment Types

| Environment | Purpose | Configuration Characteristics |
|-------------|---------|------------------------------|
| Development | Local development debugging | Detailed logs, hot reload, mock data |
| Testing | Automated testing | Isolated data, deterministic configuration |
| Staging | Pre-production validation | Near-production config, real data subset |
| Production | Official operation | Performance optimized, security hardened, minimal logs |

### Configuration File Planning

**Configuration File Structure:**

```markdown
### Environment Configuration Files

**Create:**
- `.env.example` - Environment variable template (commit to version control)
- `.env.development` - Development environment config (do not commit)
- `.env.test` - Test environment config (optional commit)
- `.env.production` - Production environment config (do not commit, inject via CI/CD)

**Configuration Items:**
- `DATABASE_URL` - Database connection address
- `API_KEY` - Third-party service key
- `LOG_LEVEL` - Log level
- `FEATURE_FLAGS` - Feature toggles
```

### Configuration Task Template

````markdown
### Task: Environment Configuration

**Files:**
- Create: `.env.example`
- Create: `src/config/index.ts`

- [ ] **Step 1: Create environment variable template**

```
# .env.example
DATABASE_URL=postgresql://localhost:5432/dbname
API_KEY=your-api-key-here
LOG_LEVEL=debug
```

- [ ] **Step 2: Create configuration loading module**

```typescript
// src/config/index.ts
export const config = {
  database: {
    url: process.env.DATABASE_URL || 'postgresql://localhost:5432/dev',
  },
  api: {
    key: process.env.API_KEY,
  },
  log: {
    level: process.env.LOG_LEVEL || 'info',
  },
};
```
````

### Sensitive Information Handling

**Security Principles:**

- Never commit sensitive information (keys, passwords) to version control
- Use environment variables or secret management services
- Clearly mark which configurations require manual user setup in the plan

---

## Rollback Strategy Planning

Prepare rollback plans for implementation failures or unexpected situations to reduce risk.

### Rollback Scenario Identification

| Scenario | Trigger Condition | Rollback Strategy |
|----------|-------------------|-------------------|
| Dependency installation failure | Version conflicts, network issues | Restore package.json/lock files |
| Persistent test failures | Unfixable test errors | Revert to last passing state |
| Feature incompatibility | Integration with existing system fails | Undo related code changes |
| Performance regression | Performance metrics not met | Revert performance-related changes |
| Security issues | Security vulnerabilities discovered | Immediate rollback and fix |

### Rollback Plan Template

Include a rollback section in the plan:

````markdown
## Rollback Plan

### Checkpoints

| Checkpoint | Completed Tasks | Rollback Command |
|------------|-----------------|------------------|
| CP-1 | Dependency installation complete | `git checkout package.json pnpm-lock.yaml && pnpm install` |
| CP-2 | Auth module complete | `git checkout src/auth/ tests/auth/` |
| CP-3 | API integration complete | `git checkout src/api/ tests/api/` |

### Rollback Steps

**If implementation fails and rollback is needed:**

1. **Stop current task**
   - Document failure reason
   - Save current progress

2. **Determine rollback point**
   - View recent checkpoints
   - Confirm rollback scope

3. **Execute rollback**
   ```bash
   # Rollback to specified checkpoint
   git reset --hard <checkpoint-commit>
   
   # Or selective file rollback
   git checkout <commit> -- path/to/files
   ```

4. **Verify rollback**
   - Run tests to ensure system is normal
   - Check if functionality is restored

5. **Document issues**
   - Record failure reason in design document
   - Update plan to avoid repeating issues
````

### Git Branch Strategy

**Recommended Branch Model:**

```
main (production)
  └── develop (development)
        └── feature/xxx (feature branch)
```

**Rollback-Friendly Practices:**

- Create commit after each task completion
- Use descriptive commit messages
- Tag at key checkpoints
- Keep commits atomic (one commit per logical change)

---

## Phase 5: Plan Review Cycle

### 5.1 Chunk Boundaries

Divide the plan into chunks using `## Chunk N: <name>` headers:

- Each chunk should be ≤1000 lines
- Each chunk should be logically self-contained

### 5.2 Review Process

After completing each plan chunk:

1. **Dispatch plan-document-reviewer subagent** to review the current chunk
   - Provide: chunk content, specification document path

2. **If issues found (❌):**
   - Fix issues in that code block
   - Re-assign reviewer to that code block
   - Repeat until approval (✅)

3. **If approved (✅):**
   - Continue to next part (or hand off for execution if last part)

### 5.3 Review Guidelines

- Fixes made by the same agent that created the plan (preserves context)
- If review loop exceeds 5 iterations, request human guidance
- Review feedback is advisory - if you disagree, explain reasoning

---

## Phase 6: Execution Handoff

### 6.1 Save the Plan

After plan completion:

1. Save plan to user-specified directory (default: `design/plans/`)
2. Use filename format: `YYYY-MM-DD-<feature-name>.md`

### 6.2 Handoff Message

After saving, inform the user:

> "Plan completed and saved to `design/plans/<filename>.md`. Ready to execute?"

### 6.3 Execution Options

- Execute plan in current session using executing-plans skill
- Use batch execution mode with checkpoints for review

---

## Phase 7: Quality Checklist

### 7.1 Plan Completeness

- [ ] Plan header is complete with Goal, Architecture, Tech Stack
- [ ] File structure is documented before tasks
- [ ] All file paths are exact and precise
- [ ] All code snippets are complete (not placeholders)
- [ ] All commands are precise with expected outputs

### 7.2 Task Quality

- [ ] Each task has clear file references (Create/Modify/Test)
- [ ] Each step is granular (2-5 minutes)
- [ ] Tests come before implementation
- [ ] Each task is independently testable

### 7.3 Scope Validation

- [ ] Plan covers single cohesive feature/subsystem
- [ ] If multiple subsystems, recommendation to split was made
- [ ] Each chunk is ≤1000 lines and self-contained

---

## Workflow Examples

### Example 1: TypeScript Project

```
User: I need to implement user authentication with JWT tokens. Here's my spec...

Agent:
1. Declares: "I am using the writing-plan skill to create an implementation plan."
2. Asks where to save (default: design/plans/)
3. Analyzes scope - confirms single subsystem
4. Plans file structure:
   - Create: src/auth/jwtHandler.ts
   - Create: src/auth/middleware.ts
   - Modify: src/config/settings.ts
   - Test: tests/auth/jwtHandler.test.ts
5. Writes plan with TDD approach using TypeScript/Jest
6. Divides into chunks (≤1000 lines each)
7. Runs review cycle on each chunk
8. Saves final plan
9. Asks: "Ready to execute?"
```

### Example 2: Rust Project

```
User: I need to implement a caching layer for our API. Here's my spec...

Agent:
1. Declares: "I am using the writing-plan skill to create an implementation plan."
2. Asks where to save (default: design/plans/)
3. Analyzes scope - confirms single subsystem
4. Plans file structure:
   - Create: src/cache/mod.rs
   - Create: src/cache/memory.rs
   - Create: src/cache/redis.rs
   - Modify: src/api/handler.rs
   - Test: tests/cache_test.rs
5. Writes plan with TDD approach using Rust/cargo test
6. Divides into chunks (≤1000 lines each)
7. Runs review cycle on each chunk
8. Saves final plan
9. Asks: "Ready to execute?"
```

### Example 3: Python Project

```
User: I need to implement a data processing pipeline. Here's my spec...

Agent:
1. Declares: "I am using the writing-plan skill to create an implementation plan."
2. Asks where to save (default: design/plans/)
3. Analyzes scope - confirms single subsystem
4. Plans file structure:
   - Create: src/pipeline/processor.py
   - Create: src/pipeline/transformers.py
   - Modify: src/config/settings.py
   - Test: tests/pipeline/test_processor.py
5. Writes plan with TDD approach using Python/pytest
6. Divides into chunks (≤1000 lines each)
7. Runs review cycle on each chunk
8. Saves final plan
9. Asks: "Ready to execute?"
```

---

## Notes

1. **Always declare skill usage** at the start
2. **Never touch code** during planning - this is pre-implementation
3. **Be precise** - exact paths, complete code, precise commands
4. **Test-first always** - every implementation step follows a test
5. **Chunk appropriately** - ≤1000 lines per chunk for review efficiency
6. **Review iteratively** - fix issues before moving to next chunk
7. **Save before execution** - plan must be persisted before handoff
8. **Language-agnostic** - adapt all examples to the project's programming language
