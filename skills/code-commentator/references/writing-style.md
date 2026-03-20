# Comment Writing Style Guide

This guide standardizes comment writing style and language specifications to ensure professional and consistent comments.

## Table of Contents

- [Tone Standards](#tone-standards)
- [Language and Grammar Specifications](#language-and-grammar-specifications)
- [Example Improvements](#example-improvements)

---

## Tone Standards

### Perspective and Tense

- **Addressing**: Use "you" to address readers
- **Voice**: Use active voice
- **Tense**: Use present tense (e.g., "function returns..." not "function will return...")

### Tone Requirements

- **Professional**: Avoid colloquial and informal expressions
- **Friendly**: Maintain helpful tone, but not verbose
- **Direct**: Get to the point, avoid beating around the bush

### Clarity Requirements

- **Vocabulary**: Use simple words, avoid excessive use of technical jargon
- **Slang**: Avoid slang and colloquial expressions
- **Marketing Language**: Avoid promotional and exaggerated language

### Requirement Levels

Clearly distinguish different levels of instructions:

| Level | Words | Description |
| -------- | ------------------ | ------------------------------ |
| Mandatory | **Must**, **Forbidden** | Rules that must be followed, violations cause errors |
| Strong Suggestion | **Recommended**, **Suggested** | Best practices that are recommended |
| Optional | **Can**, **Consider** | Suggestions that can be chosen based on situation |

**Avoid using**: "should", "ought to" and other vague expressions.

### Word Choice

| Avoid | Recommended |
| -------- | -------- |
| Please | (omit) |
| Allows you | Can |
| Allows you to | You can |
| Function thinks | Function checks |
| Array contains | Array has |

**Abbreviations can be used**: don't, it's, it has, it will, etc.

---

## Language and Grammar Specifications

### Abbreviation Usage

| Avoid | Recommended |
| ------ | --------- |
| e.g. | for example |
| i.e. | that is |
| etc. | and so on |
| vs. | compared to |
| et al. | and others |

### Punctuation

- **Serial commas**: Use commas in lists (e.g., "a, b, c")
- **Chinese quotes**: Use `""` instead of `""`
- **English quotes**: Use `""` instead of ''

### Date Format

Use clear format, for example:

- ✅ "January 22, 2026"
- ✅ "2026年1月22日"
- ❌ "2026/1/22"
- ❌ "1/22/26"

### Conciseness

| Avoid | Recommended |
| ---------------- | ---- |
| Allows you/you | Can |
| Let's look at | Look |
| Next we will | We |
| The function's role is | Function |

### Verb Selection

Use precise, specific verbs:

| Vague Verbs | Precise Verbs |
| -------- | ---------------------- |
| Handle | Parse, Transform, Calculate, Validate |
| Get | Read, Fetch, Extract, Request |
| Set | Configure, Assign, Initialize |

---

## Example Improvements

### Before (Not Recommended)

```typescript
/**
 * 这个函数可以帮助我们对用户输入的数据进行处理。
 * 它会返回一个处理后的结果。
 *
 * @param input - 输入的数据
 * @returns 返回处理后的结果
 */
function processData(input: any) {}

/**
 * 这个类是用来管理用户的。
 * 它可以帮助我们进行用户认证。
 */
class UserManager {}
```

### After (Recommended)

```typescript
/**
 * Processes user input data.
 *
 * 处理用户输入数据。
 *
 * @param input - User input data to process / 要处理的用户输入数据
 * @returns Processed result / 处理后的结果
 */
function processData(input: Data): Result {}

/**
 * Manages user authentication and session handling.
 *
 * 管理用户认证和会话处理。
 *
 * @example
 * const manager = new UserManager();
 * const session = await manager.login('user@example.com', 'password');
 */
class UserManager {}
```

### Key Improvements

1. **Direct function description**: Start by directly describing what the function/class does, not "this function is..."
2. **Use verbs to start**: Function descriptions start with verbs (e.g., Process, Calculate, Validate)
3. **Avoid redundancy**: Remove redundant expressions like "can help us", "this"
4. **Be concise**: Keep each line within reasonable length

---

## Comment Principles

### Don't Over-comment

Comments are meant to enhance readability, not to comment for the sake of commenting. Too many comments actually reduce code readability.

**Before adding comments, ask yourself**:

1. Can I quickly understand this code's intent without reading comments?
2. Are the code names clear enough?
3. Do comments provide information that the code itself cannot express?

If the answers indicate the code is already clear enough, no comments are needed.

### Be Concise and Clear

- Avoid redundant comments
- Comments should have practical value
- Provide information that code itself cannot express

### Example Requirements

- All usage examples must be runnable code
- Use meaningful names in examples
- Avoid meaningless placeholders like "foo", "bar"
