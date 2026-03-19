# 注释格式参考指南

本文档提供各种编程语言的注释格式详细示例，供在添加注释时参考。

## 目录

- [编程语言识别](#编程语言识别)
- [多行注释格式](#多行注释格式)
- [单行注释格式](#单行注释格式)
- [注释文本格式](#注释文本格式)

---

## 编程语言识别

根据文件扩展名识别编程语言，选择对应的注释风格：

| 语言                  | 文件扩展名                                   | 多行注释风格                   | 单行注释风格 |
| --------------------- | -------------------------------------------- | ------------------------------ | ------------ |
| JavaScript/TypeScript | `.js`, `.jsx`, `.ts`, `.tsx`, `.mjs`, `.cjs` | `/** ... */`                   | `// ...`     |
| Python                | `.py`                                        | `""" ... """` 或 `''' ... '''` | `# ...`      |
| Java                  | `.java`                                      | `/** ... */`                   | `// ...`     |
| C/C++                 | `.c`, `.cpp`, `.h`, `.hpp`                   | `/** ... */`                   | `// ...`     |
| Go                    | `.go`                                        | `/** ... */`                   | `// ...`     |
| Rust                  | `.rs`                                        | `/// ...` (文档注释)           | `// ...`     |
| PHP                   | `.php`                                       | `/** ... */`                   | `// ...`     |
| Ruby                  | `.rb`                                        | `=begin ... =end`              | `# ...`      |
| Swift                 | `.swift`                                     | `/** ... */`                   | `// ...`     |
| Kotlin                | `.kt`, `.kts`                                | `/** ... */`                   | `// ...`     |
| C#                    | `.cs`                                        | `/** ... */`                   | `// ...`     |
| Scala                 | `.scala`                                     | `/** ... */`                   | `// ...`     |
| Lua                   | `.lua`                                       | `--[[ ... --]]`                | `-- ...`     |
| Shell                 | `.sh`, `.bash`                               | `: ' ... '`                    | `# ...`      |

---

## 多行注释格式

### JavaScript/TypeScript 格式

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

### Python 格式

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

### Java 格式

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

### Go 格式

```go
// FunctionName English description of the function.
//
// 中文描述函数的功能。
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

### Rust 格式

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

### PHP 格式

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

### Ruby 格式

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

### Swift 格式

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

### Kotlin 格式

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

## 单行注释格式

### 短描述格式

```typescript
// english description / 中文描述
if (condition) {
}

// english description / 中文描述
const variable = value;
```

### 长描述格式

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

### Python 单行注释

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

## 特殊注释场景

### 联合类型参数处理

当参数类型为联合类型时，使用无序列表详细说明每个类型：

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

### 支持多种传参方式的函数

对于支持多种传参类型或传参个数的函数，需提供不同场景的使用示例：

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

## 注释文本格式

### 换行规则

注释文本应在100个字符左右处换行（长链接或表格等特殊内容除外）：

```typescript
/**
 * This is a very long description that needs to be wrapped at approximately
 * 100 characters to maintain readability and consistency across the codebase.
 *
 * 这是一个很长的描述，需要在约100个字符处换行，以保持代码库的可读性和一致性。
 */
```

### 中英文分隔

双语注释中，英文描述在前，中文描述在后，中间用空行分隔：

```typescript
/**
 * English description comes first.
 *
 * 中文描述紧随其后。
 */
```

### 参数描述格式

参数描述使用斜杠分隔中英文：

```typescript
@param paramName - English description / 中文描述
```
