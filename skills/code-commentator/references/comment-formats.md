# Comment Format Reference Guide

This document provides detailed comment format examples for various programming languages, for reference when adding comments.

## Table of Contents

- [Programming Language Identification](#programming-language-identification)
- [Multi-line Comment Formats](#multi-line-comment-formats)
- [Single-line Comment Formats](#single-line-comment-formats)
- [Comment Text Formatting](#comment-text-formatting)

---

## Programming Language Identification

Identify programming language based on file extension, choose corresponding comment style:

| Language | File Extensions | Multi-line Comment Style | Single-line Comment Style |
| --------------------- | -------------------------------------------- | ------------------------------ | ------------ |
| JavaScript/TypeScript | `.js`, `.jsx`, `.ts`, `.tsx`, `.mjs`, `.cjs` | `/** ... */` | `// ...` |
| Python | `.py` | `""" ... """` or `''' ... '''` | `# ...` |
| Java | `.java` | `/** ... */` | `// ...` |
| C/C++ | `.c`, `.cpp`, `.h`, `.hpp` | `/** ... */` | `// ...` |
| Go | `.go` | `/** ... */` | `// ...` |
| Rust | `.rs` | `/// ...` (doc comments) | `// ...` |
| PHP | `.php` | `/** ... */` | `// ...` |
| Ruby | `.rb` | `=begin ... =end` | `# ...` |
| Swift | `.swift` | `/** ... */` | `// ...` |
| Kotlin | `.kt`, `.kts` | `/** ... */` | `// ...` |
| C# | `.cs` | `/** ... */` | `// ...` |
| Scala | `.scala` | `/** ... */` | `// ...` |
| Lua | `.lua` | `--[[ ... --]]` | `-- ...` |
| Shell | `.sh`, `.bash` | `: ' ... '` | `# ...` |

---

## Multi-line Comment Formats

### JavaScript/TypeScript Format

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

### Python Format

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

### Java Format

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

### Go Format

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
// // Basic usage
// result := FunctionName("value")
//
// // With optional parameter
// result := FunctionName("value", options)
func FunctionName(paramName string, options *Options) *Result {
    // implementation
}
```

### Rust Format

````rust
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
````

### PHP Format

```php
/**
 * English description of the function.
 *
 * 中文描述函数的功能。
 *
 * @param string $paramName English description / 中文描述
 * @param array|null $options English description / 中文描述
 * @return Result English description / 中文描述
 * @throws ExceptionType English description / 中文描述
 * @example
 * // Basic usage
 * $result = functionName('value');
 *
 * // With optional parameter
 * $result = functionName('value', ['option' => true]);
 */
function functionName(string $paramName, ?array $options = null): Result {
    // implementation
}
```

### Ruby Format

```ruby
=begin
English description of the method.

中文描述方法的功能。

Parameters:
- param_name: English description / 中文描述
- options: English description / 中文描述

Returns:
- result: English description / 中文描述

Example:
  # Basic usage
  result = method_name('value')

  # With optional parameter
  result = method_name('value', option: true)
=end
def method_name(param_name, options = {})
  # implementation
end
```

### Swift Format

````swift
/// English description of the function.
///
/// 中文描述函数的功能.
///
/// - Parameters:
///   - paramName: English description / 中文描述
///   - options: English description / 中文描述
/// - Returns: English description / 中文描述
/// - Throws: English description / 中文描述
///
/// ## Example
/// ```swift
/// // Basic usage
/// let result = functionName("value")
///
/// // With optional parameter
/// let result = functionName("value", option: true)
/// ```
func functionName(paramName: String, options: Options? = nil) throws -> Result {
    // implementation
}
````

### Kotlin Format

```kotlin
/**
 * English description of the function.
 *
 * 中文描述函数的功能。
 *
 * @param paramName English description / 中文描述
 * @param options English description / 中文描述
 * @return English description / 中文描述
 * @throws ExceptionType English description / 中文描述
 *
 * @example
 * // Basic usage
 * val result = functionName("value")
 *
 * // With optional parameter
 * val result = functionName("value", Options())
 */
fun functionName(paramName: String, options: Options? = null): Result {
    // implementation
}
```

---

## Single-line Comment Formats

### Short Description Format

```typescript
// english description / 中文描述
if (condition) {
}

// english description / 中文描述
const variable = value;
```

### Long Description Format

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

### Python Single-line Comments

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

## Special Comment Scenarios

### Union Type Parameter Handling

When a parameter type is a union type, use unordered lists to describe each type in detail:

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

### Functions Supporting Multiple Parameter Passing Ways

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

---

## Comment Text Formatting

### Line Wrapping Rules

Comment text should wrap at approximately 100 characters (except for special content like long links or tables):

```typescript
/**
 * This is a very long description that needs to be wrapped at approximately
 * 100 characters to maintain readability and consistency across the codebase.
 *
 * 这是一个很长的描述，需要在约100个字符处换行，以保持代码库的可读性和一致性。
 */
```

### English/Chinese Separation

In bilingual comments, English description comes first, Chinese description follows, separated by a blank line:

```typescript
/**
 * English description comes first.
 *
 * 中文描述紧随其后。
 */
```

### Parameter Description Format

Parameter descriptions use slashes to separate English and Chinese:

```typescript
@param paramName - English description / 中文描述
```
