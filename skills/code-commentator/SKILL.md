---
name: code-commentator
description: Code annotation supplementation and standardization expert. Automatically identifies code file types and adds professional bilingual comments for functions, classes, methods, properties, and other code elements. Activate when user mentions "add comments", "supplement comments", "standardize comments", "code comments", "annotate code", "add comments", or needs documentation comments for code. This skill can also be automatically invoked by other skills (such as executing-plans) after code is completed.
license: MIT
metadata:
  version: "1.2.0"
---

# Code Commentator Skill

This skill provides systematic code comment supplementation and standardization capabilities. It automatically identifies code file types, applies corresponding comment standards, and ensures generated comments are accurate, complete, and meet bilingual requirements.

## Trigger Conditions

Activate this skill when detecting the following situations:

**Direct User Invocation**:

- User mentions adding or supplementing comments: "add comments", "supplement comments", "increase comments"
- User mentions standardizing comments: "standardize comments", "unify comment style", "comment standards"
- User mentions code comment needs: "add comments to code", "code lacks comments", "incomplete comments"
- User mentions specific comment types: "function comments", "class comments", "JSDoc", "docstring"
- English triggers: "add comments", "annotate code", "code documentation", "JSDoc"

**Automatic Invocation by Other Skills**:

- `executing-plans` skill automatically invokes after task completion (if code needs comments)
- In automated workflow after tests pass and before code submission

---

## Invocation by Other Skills

When invoked by `executing-plans` or other skills:

**Received Parameters**:

- `target_files`: List of file paths requiring comments (required)
- `comment_priority`: Comment priority (optional: high/medium/low)
- `focus_areas`: Key comment areas (optional: e.g., "public APIs", "core logic")

**Execution Mode**:

- Skip user confirmation, execute directly
- Use default bilingual comment format
- Automatically identify code complexity, add comments intelligently
- Return processing result summary after completion

---

## Absolute Prohibitions ⚠️

**Modifying any code content is strictly prohibited**. This skill can only add or modify comments, it must NOT:

- ❌ Modify code logic
- ❌ Modify variable names, function names, class names, or other identifiers
- ❌ Modify code structure (adding, deleting, reordering code lines)
- ❌ Modify code formatting (indentation, line breaks, spaces)

**Only Permitted Action**: Add comments to code or modify existing comments.

---

## Bilingual Comment Requirements

All comments must include **both English and Chinese bilingual explanations**, in this format:

- English description first
- Blank line separator
- Chinese description following

---

## Comment Format Reference

Detailed multilingual comment format examples have been moved to the references directory:

| Reference File | Content |
| ------------------------------------------------------- | ------------------------------ |
| [comment-formats.md](references/comment-formats.md) | Comment format code examples for various programming languages |
| [writing-style.md](references/writing-style.md) | Tone and manner guidelines, language and grammar requirements |
| [quality-checklist.md](references/quality-checklist.md) | Comment quality verification checklist |

**Important**: Before adding comments, read [comment-formats.md](references/comment-formats.md) to ensure correct language format is used.

---

## Core Comment Principles

### Elements That Must Have Multi-line Comments

The following code elements **must** have multi-line documentation comments:

- ✅ Functions/Methods
- ✅ Classes/Structs/Interfaces
- ✅ Public properties/Fields
- ✅ Enums and their members
- ✅ Type definitions
- ✅ Modules/Namespaces

### Elements That Need Evaluation

Add single-line comments only when code logic is not intuitive enough:

- ⚠️ Complex conditional branching logic
- ⚠️ Complex loop structures
- ⚠️ Complex expressions
- ⚠️ Important variable declarations (when purpose is unclear)

### Elements That Don't Need Comments

Code is already clear enough, no comments needed:

- ❌ Simple conditionals (e.g., `if (isValid)`)
- ❌ Simple loops (e.g., `for (const item of items)`)
- ❌ Variable declarations where names clearly express purpose (e.g., `const userName = user.name`)
- ❌ Standard getter/setter methods
- ❌ Obvious assignment statements

### Judgment Criteria

**Before adding comments, ask yourself**:

1. Can I quickly understand this code's intent without reading comments?
2. Are the code names clear enough?
3. Do comments provide information that the code itself cannot express?

If the answers indicate the code is already clear enough, no comments are needed.

---

## Comment Insertion Rules

| Element Type | Insertion Position | Requirements |
| ------------- | ------------------ | ------------------ |
| Function/Method Comments | Immediately above function declaration | No blank line |
| Class Comments | Immediately above class declaration | No blank line |
| Property Comments | Immediately above property declaration | No blank line |
| Single-line Comments | Above code line | Maintain same indentation as code |

---

## Function/Method Comment Requirements

Function/Method comments must include:

1. **Function Description**: Clear description of function's functionality and purpose
2. **Parameter Description**: Type and purpose of each parameter
3. **Return Value Description**: Type and meaning of return value
4. **Exception Description**: Possible exceptions and conditions (if any)
5. **Usage Examples**: At least one basic usage example

### Union Type Parameters

When a parameter is a union type, **must** describe each type in detail:

```typescript
@param input - The input data to process. Can be:
  - `string`: A string value to parse / 要解析的字符串值
  - `Buffer`: A buffer containing raw data / 包含原始数据的缓冲区
  - `ReadableStream`: A stream to read data from / 要读取数据的流
```

### Multiple Parameter Passing Ways

When supporting multiple parameter passing ways, provide **different scenario usage examples**:

```typescript
@example
// Create user with name only
const user = createUser('John');

// Create user with options object
const user = createUser({ name: 'John', age: 25, email: 'john@example.com' });
```

---

## Execution Flow

### File Scanning Flow

1. Receive user-specified files or directories
2. Recursively scan all code files
3. Group by language type for processing
4. Generate processing plan

### Single File Processing Flow

1. Read file content
2. Parse code structure (AST or regex matching)
3. Identify code elements needing comments
4. Check completeness of existing comments
5. Generate comments conforming to standards
6. Insert comments to correct positions
7. Write updated file

### Progress Report Format

Report progress in real-time during processing:

```markdown
## Comment Processing Progress

### Completed (3/10)

- ✅ src/utils/helper.ts (added 5 function comments)
- ✅ src/models/user.ts (added 2 class comments, 8 property comments)
- ✅ src/api/client.ts (added 3 function comments)

### Processing

- 🔄 src/services/auth.ts

### Pending (6/10)

- ⏳ src/config/index.ts
- ...
```

---

## Quick Reference

### Comment Format Cheat Sheet

```typescript
/**
 * English description of the function.
 *
 * 中文描述函数的功能。
 *
 * @param paramName - English description / 中文描述
 * @returns English description / 中文描述
 * @throws {ErrorType} English description / 中文描述
 * @example
 * const result = functionName('value');
 */
function functionName(paramName: string): Result {}
```

### Quick Notes

1. **Only add comments**: Strictly prohibited from modifying any code content
2. **Maintain consistency**: Comment style must be consistent within the same file
3. **Accuracy first**: Comment content must accurately reflect code functionality
4. **Avoid over-commenting**: If code is clear enough, no comments needed
5. **Be concise**: Comments should have practical value
6. **Examples must be runnable**: All usage examples must be executable code

---

## Reference Documents

- 📄 [comment-formats.md](references/comment-formats.md) - Detailed format examples
- 📄 [writing-style.md](references/writing-style.md) - Writing style guide
- 📄 [quality-checklist.md](references/quality-checklist.md) - Quality verification checklist
