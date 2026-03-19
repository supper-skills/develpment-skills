# Comment Writing Style Guide

This guide standardizes the writing style and language norms for comments, ensuring comments are professional and consistent.

## Table of Contents

- [Tone Standards](#tone-standards)
- [Language and Grammar Norms](#language-and-grammar-norms)
- [Example Improvements](#example-improvements)

---

## Tone Standards

### Perspective and Tense

- **Address**: Address the reader as "you"
- **Voice**: Use active voice
- **Tense**: Use present tense (e.g., "The function returns..." not "The function will return...")

### Tone Requirements

- **Professional**: Avoid colloquial and informal expressions
- **Friendly**: Maintain a helpful tone, but not verbose
- **Direct**: Get to the point, avoid beating around the bush

### Clarity Requirements

- **Vocabulary**: Use simple words, avoid overusing technical jargon
- **Slang**: Avoid slang and colloquial expressions
- **Marketing Language**: Avoid promotional and exaggerated language

### Requirement Levels

Clearly distinguish different levels of instructions:

| Level | Words | Description |
|--------|------|------|
| Mandatory Requirement | **must**, **strictly prohibited** | Rules that must be followed, violation causes errors |
| Strong Recommendation | **recommend**, **suggest** | Recommended best practices |
| Optional Suggestion | **can**, **consider** | Suggestions that can be chosen based on situation |

**Avoid using**: "should", "ought to" and other vague expressions.

### Word Choice

| Avoid | Recommend |
|-------|-------|
| please | (omit) |
| allows you to | can |
| enables you to | you can |
| the function thinks | the function checks |
| the array contains | the array has |

**Can use contractions**: don't, it's, it has, it will, etc.

---

## Language and Grammar Norms

### Abbreviation Usage

| Avoid | Recommend |
|-------|-------|
| e.g. | for example |
| i.e. | that is |
| etc. | etc |
| vs. | compared with |
| et al. | et al |

### Punctuation

- **Serial comma**: Use commas to separate items in lists (e.g., "a, b, c")
- **Chinese quotation marks**: Use `""` instead of `""`
- **English quotation marks**: Use `""` instead of ''

### Date Format

Use explicit formats, for example:

- ✅ "January 22, 2026"
- ✅ "2026年1月22日"
- ❌ "2026/1/22"
- ❌ "1/22/26"

### Conciseness

| Avoid | Recommend |
|-------|-------|
| allows you to | can |
| let's look at | look at |
| next we will | we will |
| this function's purpose is | the function |

### Verb Selection

Use precise, specific verbs:

| Vague Verb | Precise Verbs |
|------------|---------------|
| process | parse, transform, calculate, validate |
| get | read, fetch, extract, request |
| set | configure, assign, initialize |

---

## Example Improvements

### Before Improvement (Not Recommended)

```typescript
/**
 * This function can help us process user input data.
 * It will return a processed result.
 *
 * @param input - Input data
 * @returns Returns the processed result
 */
function processData(input: any) {}

/**
 * This class is used to manage users.
 * It can help us perform user authentication.
 */
class UserManager {}
```

### After Improvement (Recommended)

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

### Key Improvement Points

1. **Directly describe functionality**: Start by directly stating function/class purpose, not "this function is..."
2. **Start with verb**: Function descriptions start with a verb (e.g., Process, Calculate, Validate)
3. **Avoid redundancy**: Remove redundant expressions like "can help us", "this"
4. **Keep concise**: Keep each line within reasonable length

---

## Comment Principles

### Don't Over-comment

Comments are meant to enhance readability, not to comment for the sake of commenting. Too many comments can actually harm code readability.

**Before adding comments, ask yourself**:

1. Can I quickly understand this code's intent without reading comments?
2. Is the code naming clear enough?
3. Does the comment provide information that the code itself cannot express?

If the answers indicate the code is clear enough, no comments are needed.

### Concise and Clear

- Avoid redundant comments
- Comments should have practical value
- Provide information that code itself cannot express

### Example Requirements

- All usage examples must be actually runnable code
- Use meaningful names in examples
- Avoid using meaningless placeholders like "foo", "bar"
