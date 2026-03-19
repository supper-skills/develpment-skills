---
name: code-commentator
description: Code comment supplementation and standardization expert. Automatically identifies code file types and adds professional bilingual comments to functions, classes, methods, properties, and other code elements. Triggered when users mention "add comments", "supplement comments", "standardize comments", "code comments", "annotate code", "add comments", or need to add documentation comments to code.
license: MIT
metadata:
  version: "1.1.0"
---

# Code Commentator Skill

This skill provides systematic code comment supplementation and standardization capabilities, automatically identifying code file types, applying corresponding comment standards, and ensuring generated comments are accurate, complete, and meet bilingual requirements.

## Trigger Conditions

Activate this skill when detecting the following situations:

- User mentions adding or supplementing comments: "add comments", "supplement comments", "increase comments"
- User mentions standardizing comments: "standardize comments", "unify comment style", "comment standards"
- User mentions code comment needs: "add comments to code", "code lacks comments", "incomplete comments"
- User mentions specific comment types: "function comments", "class comments", "JSDoc", "docstring"
- English triggers: "add comments", "annotate code", "code documentation", "JSDoc"

---

## Absolute Prohibitions ⚠️

**Modifying any code content is strictly prohibited**. This skill can only add or modify comments, and must not:

- ❌ Modify code logic
- ❌ Modify variable names, function names, class names, or other identifiers
- ❌ Modify code structure (such as adding, deleting, or rearranging code lines)
- ❌ Modify code formatting (such as indentation, line breaks, spaces)

**The only permitted operation**: Adding comments to code or modifying existing comments.

---

## Bilingual Comment Requirements

All comments must simultaneously include both **English and Chinese explanations**, in the format:

- English description first
- Empty line separator
- Chinese description after

---

## Comment Format Reference

Detailed multi-language comment format examples have been moved to the references directory:

| Reference File | Content |
|----------------|---------|
| [comment-formats.md](references/comment-formats.md) | Comment format code examples for various programming languages |
| [writing-style.md](references/writing-style.md) | Tone and voice standards, language and grammar requirements |
| [quality-checklist.md](references/quality-checklist.md) | Comment quality verification checklist |

**Important**: Before adding comments, read [comment-formats.md](references/comment-formats.md) to ensure using the correct language format.

---

## Core Comment Principles

### Elements That Must Have Multi-line Comments

The following code elements **must** have multi-line documentation comments:

- ✅ Functions/methods
- ✅ Classes/structs/interfaces
- ✅ Public properties/fields
- ✅ Enums and their members
- ✅ Type definitions
- ✅ Modules/namespaces

### Elements That Need Evaluation for Comments

Only add single-line comments when code logic is not intuitive:

- ⚠️ Complex conditional branch logic
- ⚠️ Complex loop structures
- ⚠️ Complex expressions
- ⚠️ Important variable declarations (when purpose is not obvious)

### Cases Where Comments Are Not Needed

Code itself is clear enough, no comments needed:

- ❌ Simple conditional checks (such as `if (isValid)`)
- ❌ Simple loops (such as `for (const item of items)`)
- ❌ Declarations where variable names clearly express purpose (such as `const userName = user.name`)
- ❌ Standard getter/setter methods
- ❌ Obvious assignment statements

### Judgment Criteria

**Before adding comments, ask yourself**:

1. Can I quickly understand this code's intent without reading comments?
2. Is the code naming clear enough?
3. Does the comment provide information that the code itself cannot express?

If the answers indicate the code is clear enough, no comments are needed.

---

## Comment Insertion Rules

| Element Type | Insertion Position | Requirement |
|--------------|-------------------|-------------|
| Function/method comments | Immediately above function declaration | No blank line |
| Class comments | Immediately above class declaration | No blank line |
| Property comments | Immediately above property declaration | No blank line |
| Single-line comments | Above the code line | Maintain same indentation |

---

## Function/Method Comment Requirements

Function/method comments must include:

1. **Function Description**: Clearly describe the function's purpose and usage
2. **Parameter Description**: Type and purpose of each parameter
3. **Return Value Description**: Type and meaning of return value
4. **Exception Description**: Possible exceptions and their conditions (if any)
5. **Usage Examples**: At least one basic usage example

### Union Type Parameters

When parameter types are union types, **must** detail each type:

```typescript
@param input - The input data to process. Can be:
  - `string`: A string value to parse / 要解析的字符串值
  - `Buffer`: A buffer containing raw data / 包含原始数据的缓冲区
  - `ReadableStream`: A stream to read data from / 要读取数据的流
```

### Multiple Parameter Passing Styles

When supporting multiple parameter passing styles, provide **usage examples for different scenarios**:

```typescript
@example
// Create user with name only
const user = createUser('John');

// Create user with options object
const user = createUser({ name: 'John', age: 25, email: 'john@example.com' });
```

---

## Execution Workflow

### File Scanning Workflow

1. Receive user-specified files or directories
2. Recursively scan all code files
3. Group by language type for processing
4. Generate processing plan

### Single File Processing Workflow

1. Read file content
2. Parse code structure (AST or regex matching)
3. Identify code elements that need comments
4. Check completeness of existing comments
5. Generate comments that conform to standards
6. Insert comments into correct positions
7. Write updated file

### Progress Reporting Format

Report progress in real-time during processing:

```markdown
## Comment Processing Progress

### Completed (3/10)

- ✅ src/utils/helper.ts (added 5 function comments)
- ✅ src/models/user.ts (added 2 class comments, 8 property comments)
- ✅ src/api/client.ts (added 3 function comments)

### In Progress

- 🔄 src/services/auth.ts

### Pending (6/10)

- ⏳ src/config/index.ts
- ...
```

---

## Quick Reference

### Comment Format Quick Reference

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

### Key Points to Remember

1. **Only add comments**: Strictly prohibit modifying any code content
2. **Maintain consistency**: Comment style within the same file must be consistent
3. **Accuracy first**: Comment content must accurately reflect code functionality
4. **Avoid over-commenting**: If code is clear enough, no comments needed
5. **Concise and clear**: Comments should have practical value
6. **Examples must be runnable**: All usage examples must be actual runnable code

---

## Reference Documents

- 📄 [comment-formats.md](references/comment-formats.md) - Detailed format examples
- 📄 [writing-style.md](references/writing-style.md) - Writing style guide
- 📄 [quality-checklist.md](references/quality-checklist.md) - Quality verification checklist
