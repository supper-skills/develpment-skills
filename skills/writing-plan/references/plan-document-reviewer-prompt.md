# Plan Document Reviewer Prompt

This document provides instructions for reviewing implementation plan chunks.

## Review Purpose

Ensure each plan chunk meets quality standards before execution. The reviewer validates completeness, precision, and adherence to planning principles.

## Review Checklist

### 1. Header Completeness

- [ ] Plan has required header with Goal, Architecture, Tech Stack
- [ ] Goal is a single clear sentence
- [ ] Architecture provides 2-3 sentences of approach
- [ ] Tech Stack lists key technologies/libraries

### 2. File Structure

- [ ] File structure is documented before tasks
- [ ] All file paths are exact and precise
- [ ] New files, modified files, and test files are clearly separated
- [ ] Each file has a clear responsibility description
- [ ] File extensions match the project's programming language

### 3. Task Quality

- [ ] Each task has clear file references (Create/Modify/Test)
- [ ] Each step is granular (2-5 minutes per step)
- [ ] Tests come before implementation (TDD approach)
- [ ] Each task is independently testable

### 4. Code Completeness

- [ ] All code snippets are complete (not placeholders)
- [ ] No vague instructions like "add validation"
- [ ] Code is syntactically correct
- [ ] Code follows language conventions
- [ ] Code examples use the project's programming language

### 5. Command Precision

- [ ] All commands are precise and runnable
- [ ] Expected outputs are documented
- [ ] Test commands specify exact test names/paths
- [ ] Commands are appropriate for the project's language/framework

### 6. Scope Validation

- [ ] Chunk is ≤1000 lines
- [ ] Chunk is logically self-contained
- [ ] No orphaned references to other chunks

## Review Output Format

After reviewing, provide output in this format:

```markdown
## Review Result: [✅ Approved / ❌ Issues Found]

### Summary
[Brief summary of the review]

### Issues Found (if any)
1. [Issue description]
   - Location: [specific section/line]
   - Recommendation: [how to fix]

### Strengths
- [What was done well]

### Recommendations
- [Optional improvements]
```

## Review Guidelines

1. **Be thorough but fair** - Focus on issues that would block execution
2. **Explain the why** - When flagging issues, explain why it matters
3. **Be constructive** - Provide specific recommendations
4. **Consider context** - The plan is for engineers unfamiliar with the codebase
5. **Value precision** - Vague plans lead to failed executions
6. **Language awareness** - Ensure examples match the project's programming language

## Common Issues to Watch For

### Vague Instructions

❌ Bad: "Add error handling"
✅ Good: "Add try-except block that catches ValueError and returns ErrorResult"

### Missing Test Steps

❌ Bad: Implementation step without preceding test
✅ Good: Test step → Run test (fail) → Implement → Run test (pass)

### Imprecise Paths

❌ Bad: "Update the config file"
✅ Good: "Modify: `src/config/settings.py:45-52`"

### Placeholder Code

❌ Bad: "// implement the logic here"
✅ Good: Complete, runnable code snippet

### Wrong Language Examples

❌ Bad: Python examples in a TypeScript project
✅ Good: TypeScript examples matching the project's language

## Escalation

If review loop exceeds 5 iterations for the same chunk, escalate to human guidance with:

1. Summary of issues
2. Attempts made
3. Specific area of disagreement
