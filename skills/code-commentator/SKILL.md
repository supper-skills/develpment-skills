---
name: code-commentator
description: Code comment supplementation and standardization expert. Automatically identifies code file types and adds professional bilingual comments to functions, classes, methods, properties, and other code elements. Triggered when users mention "add comments", "supplement comments", "standardize comments", "code comments", "annotate code", "add comments", or need to add documentation comments to code.
license: MIT
metadata:
  version: "1.0.0"
---

# Code Commentator Skill

This skill provides systematic code comment supplementation and standardization capabilities. It automatically identifies code file types, applies corresponding comment standards, and ensures generated comments are accurate, complete, and meet bilingual requirements.

## Trigger Conditions

Activate this skill when detecting the following situations:

- User mentions adding or supplementing comments: "add comments", "supplement comments", "increase comments"
- User mentions standardizing comments: "standardize comments", "unify comment style", "comment standards"
- User mentions code comment needs: "add comments to code", "code lacks comments", "incomplete comments"
- User mentions specific comment types: "function comments", "class comments", "JSDoc", "docstring"
- English triggers: "add comments", "annotate code", "code documentation", "JSDoc"

---

## Core Principles

### Absolute Prohibitions

**Modifying any code content is strictly prohibited**. This skill can only add or modify comments, and must not:

- Modify code logic
- Modify variable names, function names, class names, or other identifiers
- Modify code structure (such as adding, deleting, or rearranging code lines)
- Modify code formatting (such as indentation, line breaks, spaces)

The only permitted operation is adding comments to code or modifying existing comments.

### Bilingual Comment Requirements

All comments must simultaneously include both English and Chinese explanations.

---

## Phase 1: Project and File Analysis

Before executing comment supplementation, comprehensively analyze the project and target files.

### 1.1 Identify Programming Language

Identify programming language based on file extension and select corresponding comment style:

| Language | File Extensions | Multi-line Comment Style | Single-line Comment Style |
|----------|----------------|-------------------------|-------------------------|
| JavaScript/TypeScript | `.js`, `.jsx`, `.ts`, `.tsx`, `.mjs`, `.cjs` | `/** ... */` | `// ...` |
| Python | `.py` | `""" ... """` or `''' ... '''` | `# ...` |
| Java | `.java` | `/** ... */` | `// ...` |
| C/C++ | `.c`, `.cpp`, `.h`, `.hpp` | `/** ... */` | `// ...` |
| Go | `.go` | `/** ... */` | `// ...` |
| Rust | `.rs` | `/// ...` (documentation comment) | `// ...` |
| PHP | `.php` | `/** ... */` | `// ...` |
| Ruby | `.rb` | `=begin ... =end` | `# ...` |
| Swift | `.swift` | `/** ... */` | `// ...` |
| Kotlin | `.kt`, `.kts` | `/** ... */` | `// ...` |
| C# | `.cs` | `/** ... */` | `// ...` |
| Scala | `.scala` | `/** ... */` | `// ...` |
| Lua | `.lua` | `--[[ ... --]]` | `-- ...` |
| Shell | `.sh`, `.bash` | `: ' ... '` | `# ...` |

### 1.2 Analyze Code Structure

Parse code files and identify code elements that need comments.

**Core Principles for Comments**: Comments are meant to enhance code readability, not to comment for the sake of commenting. Excessive comments can反而 harm readability. If the code itself is simple and clear enough to self-explain its intent, no comments are needed.

**Elements that must have multi-line comments**:

- Functions/methods
- Classes/structs/interfaces
- Public properties/fields
- Enums and their members
- Type definitions
- Modules/namespaces

**Elements that need evaluation for single-line comments**:

Only add comments when code logic is not intuitive and cannot self-explain:

- **Complex conditional logic**: When condition checking involves multiple variables, complex operations, or business rules
- **Complex loop structures**: When loop logic is not intuitive or has special edge cases
- **Complex expressions**: When expressions involve multi-step operations or special algorithms
- **Important variable declarations**: When variable purpose is not obvious or involves special business meaning

**Cases where comments are not needed**:

The following cases are clear enough from the code itself, no comments needed:

- Simple conditional checks (such as `if (isvalid)`)
- Simple loops (such as `for (const item of items)`)
- Declarations where variable names clearly express purpose (such as `const userName = user.name`)
- Standard getter/setter methods
- Obvious assignment statements

**Judgment Criteria**:

Before adding comments, ask yourself:

1. Can I quickly understand this code's intent without reading comments?
2. Is the code naming clear enough?
3. Does the comment provide information that the code itself cannot express?

If the answers indicate the code is clear enough, no comments are needed.

### 1.3 Detect Existing Comments

Analyze existing comments in the code:

- Identify code elements that already have comments
- Check if existing comments conform to standards
- Mark comments that need supplementation or correction

---

## Phase 2: Comment Format Standards

### 2.1 Multi-line Comment Format

#### JavaScript/TypeScript Format

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
 * // Basic usage
 * const result = functionName('value');
 *
 * // With optional parameter
 * const result = functionName('value', { option: true });
 */
function functionName(paramName: string, options?: Options): Result {
  // implementation
}
```

#### Python Format

```python
"""
English description of the function.

中文描述函数的功能。

Args:
    param_name (str): English description / 中文描述

Returns:
    Result: English description / 中文描述

Raises:
    ErrorType: English description / 中文描述

Example:
    >>> # Basic usage
    >>> result = function_name('value')
    >>>
    >>> # With optional parameter
    >>> result = function_name('value', option=True)
"""
def function_name(param_name: str, options: Optional[Options] = None) -> Result:
    # implementation
```

#### Java Format

```java
/**
 * English description of the method.
 *
 * 中文描述方法的功能。
 *
 * @param paramName English description / 中文描述
 * @return English description / 中文描述
 * @throws ExceptionType English description / 中文描述
 * @example
 * // Basic usage
 * Result result = methodName("value");
 *
 * // With optional parameter
 * Result result = methodName("value", options);
 */
public Result methodName(String paramName, Options options) {
    // implementation
}
```

#### Go Format

```go
// FunctionName English description of the function.
//
// 中文描述函数的功能.
//
// Parameters:
//   - paramName: English description / 中文描述
//
// Returns:
//   - result: English description / 中文描述
//
// Example:
//
//	// Basic usage
//	result := FunctionName("value")
//
//	// With optional parameter
//	result := FunctionName("value", options)
func FunctionName(paramName string, options *Options) *Result {
    // implementation
}
```

#### Rust Format

```rust
/// English description of the function.
///
/// 中文描述函数的功能.
///
/// # Arguments
///
/// * `param_name` - English description / 中文描述
///
/// # Returns
///
/// English description / 中文描述
///
/// # Errors
///
/// Returns an error if...
///
/// # Examples
///
/// ```
/// // Basic usage
/// let result = function_name("value");
///
/// // With optional parameter
/// let result = function_name("value", Some(options));
/// ```
pub fn function_name(param_name: &str, options: Option<Options>) -> Result<Result, Error> {
    // implementation
}
```

### 2.2 Single-line Comment Format

#### Short Description Format

```typescript
// english description / 中文描述
if (condition) {}

// english description / 中文描述
const variable = value;
```

#### Long Description Format

```typescript
// This is a longer english description that explains
// the purpose of the following code block.
//
// 这是较长的中文描述，解释以下代码块的用途。
if (complexCondition) {
  // english description / 中文描述
  doSomething();
}
```

#### Python Single-line Comments

```python
# english description / 中文描述
if condition:
    pass

# This is a longer english description that explains
# the purpose of the following code block.
#
# 这是较长的中文描述，解释以下代码块的用途。
for item in items:
    # english description / 中文描述
    process(item)
```

---

## Phase 3: Comment Content Standards

### 3.1 Function/Method Comment Requirements

Function/method comments must include:

1. **Function Description**: Clearly describe the function's purpose and usage
2. **Parameter Description**: Type and purpose of each parameter
3. **Return Value Description**: Type and meaning of return value
4. **Exception Description**: Possible exceptions and their conditions (if any)
5. **Usage Examples**: At least one basic usage example

#### Handling Union Types in Parameters

When parameter types are union types, use unordered lists to detail each type:

```typescript
/**
 * Processes the input data.
 *
 * 处理输入数据。
 *
 * @param input - The input data to process. Can be:
 *   - `string`: A string value to parse / 要解析的字符串值
 *   - `Buffer`: A buffer containing raw data / 包含原始数据的缓冲区
 *   - `ReadableStream`: A stream to read data from / 要读取数据的流
 * @returns The processed result / 处理后的结果
 * @example
 * // Process a string
 * const result = process('hello');
 *
 * // Process a buffer
 * const result = process(Buffer.from('hello'));
 */
function process(input: string | Buffer | ReadableStream): Result {}
```

#### Functions Supporting Multiple Parameter Styles

For functions that support multiple parameter types or counts, provide usage examples for different scenarios:

```typescript
/**
 * Creates a new user instance.
 *
 * 创建新的用户实例。
 *
 * @param nameOrOptions - Can be:
 *   - `string`: The user's name / 用户名称
 *   - `UserOptions`: Full user configuration object / 完整的用户配置对象
 * @param age - User's age (required when first param is string) / 用户年龄（第一个参数为字符串时必填）
 * @returns The created user instance / 创建的用户实例
 * @example
 * // Create user with name only
 * const user = createUser('John');
 *
 * // Create user with name and age
 * const user = createUser('John', 25);
 *
 * // Create user with options object
 * const user = createUser({ name: 'John', age: 25, email: 'john@example.com' });
 */
function createUser(nameOrOptions: string | UserOptions, age?: number): User {}
```

### 3.2 Class Comment Requirements

Class comments must include:

1. **Function Description**: Class purpose and responsibilities
2. **Property Description**: Description of important public properties
3. **Usage Examples**: Examples of creating and using class instances

```typescript
/**
 * Manages user authentication and session handling.
 *
 * 管理用户认证和会话处理。
 *
 * @example
 * // Create a new auth manager
 * const auth = new AuthManager({
 *   apiKey: 'your-api-key',
 *   endpoint: 'https://api.example.com'
 * });
 *
 * // Authenticate a user
 * const session = await auth.login('user@example.com', 'password');
 */
class AuthManager {
  /**
   * Current active session.
   *
   * 当前活动会话。
   */
  public session: Session | null;

  /**
   * Creates a new AuthManager instance.
   *
   * 创建新的 AuthManager 实例。
   *
   * @param config - Configuration options / 配置选项
   */
  constructor(config: AuthConfig) {}
}
```

### 3.3 Property/Field Comment Requirements

```typescript
class User {
  /**
   * User's unique identifier.
   *
   * 用户的唯一标识符。
   */
  public id: string;

  /**
   * User's display name.
   *
   * 用户的显示名称。
   */
  public name: string;

  /**
   * User's email address.
   *
   * 用户的电子邮件地址。
   */
  public email: string;
}
```

### 3.4 Enum Comment Requirements

```typescript
/**
 * Defines the status of a task.
 *
 * 定义任务的状态。
 */
enum TaskStatus {
  /**
   * Task is waiting to be processed.
   *
   * 任务等待处理。
   */
  Pending = 'pending',

  /**
   * Task is currently being processed.
   *
   * 任务正在处理中。
   */
  InProgress = 'in_progress',

  /**
   * Task has been completed successfully.
   *
   * 任务已成功完成。
   */
  Completed = 'completed',

  /**
   * Task has failed.
   *
   * 任务已失败。
   */
  Failed = 'failed',
}
```

### 3.5 Type Definition Comment Requirements

```typescript
/**
 * Configuration options for the API client.
 *
 * API 客户端的配置选项。
 */
interface ApiClientOptions {
  /**
   * API base URL.
   *
   * API 基础 URL。
   */
  baseUrl: string;

  /**
   * Request timeout in milliseconds.
   *
   * 请求超时时间（毫秒）。
   */
  timeout?: number;

  /**
   * Custom headers to include in requests.
   *
   * 请求中包含的自定义请求头。
   */
  headers?: Record<string, string>;
}
```

---

## Phase 4: Tone and Voice Standards

### 4.1 Tone Standards

Use a professional, friendly, conversational help tone:

- **Perspective and Tense**: Address the reader as "you". Use active voice and present tense (e.g., "The function returns...").
- **Tone**: Professional, friendly, and direct.
- **Clarity**: Use simple words. Avoid jargon, slang, and marketing language.
- **Requirements**: Clearly distinguish requirements ("must") from suggestions ("we recommend"). Avoid "should".
- **Word Choice**: Avoid "please" and personification (e.g., "the function thinks"). Use contractions (like "don't", "it's").

### 4.2 Language and Grammar Standards

- **Abbreviations**: Avoid Latin abbreviations; use "for example" (not "e.g.") and "that is" (not "i.e.").
- **Punctuation**: Use serial commas. Chinese content should use `""` instead of `""`.
- **Dates**: Use explicit formats (e.g., "January 22, 2026").
- **Conciseness**: Use "lets you" instead of "allows you". Choose precise, specific verbs.
- **Examples**: Use meaningful names in examples; avoid meaningless placeholders like "foo" or "bar".

---

## Phase 5: Comment Text Formatting Standards

### 5.1 Line Wrapping Rules

Comment text should wrap at approximately 100 characters (except for special content like long links or tables):

```typescript
/**
 * This is a very long description that needs to be wrapped at approximately
 * 100 characters to maintain readability and consistency across the codebase.
 *
 * 这是一个很长的描述，需要在约100个字符处换行，以保持代码库的可读性和一致性。
 */
```

### 5.2 English/Chinese Separation

In bilingual comments, English description comes first, Chinese description follows, separated by an empty line:

```typescript
/**
 * English description comes first.
 *
 * 中文描述紧随其后。
 */
```

### 5.3 Parameter Description Format

Parameter descriptions use slashes to separate English and Chinese:

```typescript
@param paramName - English description / 中文描述
```

---

## Phase 6: Execution Workflow

### 6.1 File Scanning Workflow

1. Receive user-specified files or directories
2. Recursively scan all code files
3. Group by language type for processing
4. Generate processing plan

### 6.2 Single File Processing Workflow

1. Read file content
2. Parse code structure (AST or regex matching)
3. Identify code elements that need comments
4. Check completeness of existing comments
5. Generate comments that conform to standards
6. Insert comments into correct positions
7. Write updated file

### 6.3 Comment Insertion Rules

- **Function/method comments**: Immediately above function declaration, no blank line
- **Class comments**: Immediately above class declaration, no blank line
- **Property comments**: Immediately above property declaration, no blank line
- **Single-line comments**: Above the code line, maintain same indentation

### 6.4 Progress Reporting

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

## Phase 7: Quality Verification

### 7.1 Comment Completeness Check

- [ ] All public functions have comments
- [ ] All public classes have comments
- [ ] All public properties have comments
- [ ] All enums and their members have comments
- [ ] All type definitions have comments

### 7.2 Comment Content Check

- [ ] Function descriptions are clear and accurate
- [ ] Parameter descriptions are complete
- [ ] Return value descriptions are accurate
- [ ] Usage examples are runnable
- [ ] Union type parameters have detailed descriptions

### 7.3 Comment Format Check

- [ ] Conforms to language-specific comment style
- [ ] Bilingual format is correct
- [ ] Line wrapping position is reasonable
- [ ] Punctuation usage is correct

### 7.4 Code Completeness Check

- [ ] No code logic modified
- [ ] No identifiers modified
- [ ] No code structure modified
- [ ] No code formatting modified

---

## Workflow Examples

### Example 1: Add Comments to a Single File

```
User: Add comments to src/utils/helper.ts

Agent:
1. Read file content
2. Parse code structure, identify 5 functions
3. Check existing comments (found 2 functions lacking comments)
4. Generate bilingual comments for functions lacking comments
5. Insert comments into correct positions
6. Write updated file
7. Report: Added 3 function comments, modified 2 existing comments
```

### Example 2: Batch Add Comments to Directory

```
User: Add comments to all TypeScript files in src/ directory

Agent:
1. Scan src/ directory, find 15 .ts files
2. Sort by file size, generate processing plan
3. Process files one by one:
   - Parse code structure
   - Identify elements needing comments
   - Generate and insert comments
4. Report progress in real-time
5. Generate summary report after completion
```

### Example 3: Standardize Existing Comments

```
User: Standardize comment style for files in src/api/ directory

Agent:
1. Scan directory, find 8 code files
2. Analyze existing comment styles
3. Identify comments not conforming to standards
4. Correct comment format according to standards
5. Ensure all comments are bilingual
6. Report modifications
```

---

## Notes

1. **Only Add Comments**: Strictly prohibit modifying any code content, including logic, structure, formatting
2. **Maintain Consistency**: Comment style within the same file must be consistent
3. **Accuracy First**: Comment content must accurately reflect code functionality
4. **Avoid Over-commenting**: Comments are meant to enhance readability, not to comment for the sake of commenting. If code is clear enough, no comments needed
5. **Concise and Clear**: Avoid redundant comments; comments should have practical value, providing information that code itself cannot express
6. **Examples Must Be Runnable**: All usage examples must be actual runnable code
