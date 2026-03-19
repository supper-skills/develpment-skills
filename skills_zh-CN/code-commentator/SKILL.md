---
name: code-commentator
description: 代码注释补充与规范化专家，自动识别代码文件类型，为函数、类、方法、属性等代码元素添加专业双语注释。当用户提及"添加注释"、"补充注释"、"规范化注释"、"代码注释"、"annotate code"、"add comments"或需要为代码添加文档注释时使用本技能。
license: MIT
metadata:
  version: "1.1.0"
---

# 代码注释补充与规范化技能

本技能提供代码注释的系统性补充与规范化处理能力，自动识别代码文件类型，应用相应的注释规范，确保生成的注释准确、完整且符合双语要求。

## 触发条件

当检测到以下情况时，主动激活此技能：

- 用户提及添加或补充注释："添加注释"、"补充注释"、"增加注释"
- 用户提及规范化注释："规范化注释"、"统一注释风格"、"注释规范"
- 用户提及代码注释需求："给代码加注释"、"代码缺少注释"、"注释不完整"
- 用户提及特定注释类型："函数注释"、"类注释"、"JSDoc"、"docstring"
- 英文触发词："add comments"、"annotate code"、"code documentation"、"JSDoc"

---

## 绝对禁止事项 ⚠️

**严禁修改任何代码内容**。本技能只能添加或修改注释，不得：

- ❌ 修改代码逻辑
- ❌ 修改变量名、函数名、类名等标识符
- ❌ 修改代码结构（如添加、删除、重排代码行）
- ❌ 修改代码格式（如缩进、换行、空格）

**唯一允许的操作**：为代码添加注释或修改现有注释。

---

## 双语注释要求

所有注释必须同时包含**中英文双语说明**，格式为：

- 英文描述在前
- 空行分隔
- 中文描述在后

---

## 注释格式参考

详细的多语言注释格式示例已迁移到 references 目录：

| 参考文件                                                | 内容                           |
| ------------------------------------------------------- | ------------------------------ |
| [comment-formats.md](references/comment-formats.md)     | 各种编程语言的注释格式代码示例 |
| [writing-style.md](references/writing-style.md)         | 语气与口吻规范、语言语法要求   |
| [quality-checklist.md](references/quality-checklist.md) | 注释质量验证清单               |

**重要**：添加注释前，先阅读 [comment-formats.md](references/comment-formats.md) 确保使用正确的语言格式。

---

## 核心注释原则

### 必须添加多行注释的元素

以下代码元素**必须**添加多行文档注释：

- ✅ 函数/方法
- ✅ 类/结构体/接口
- ✅ 公共属性/字段
- ✅ 枚举及其成员
- ✅ 类型定义
- ✅ 模块/命名空间

### 需要评估是否添加注释

仅在代码逻辑不够直观时才添加单行注释：

- ⚠️ 复杂的条件分支逻辑
- ⚠️ 复杂的循环结构
- ⚠️ 复杂的表达式
- ⚠️ 重要的变量声明（用途不明显时）

### 不需要添加注释的情况

代码本身已足够清晰，无需添加注释：

- ❌ 简单的条件判断（如 `if (isValid)`）
- ❌ 简单的循环（如 `for (const item of items)`）
- ❌ 变量名已清晰表达用途的声明（如 `const userName = user.name`）
- ❌ 标准的 getter/setter 方法
- ❌ 一目了然的赋值语句

### 判断标准

**添加注释前，先问自己**：

1. 不看注释，能否快速理解这段代码的意图？
2. 代码命名是否足够清晰？
3. 注释是否提供了代码本身无法表达的信息？

如果以上问题的答案表明代码已足够清晰，则不需要添加注释。

---

## 注释插入规则

| 元素类型      | 插入位置           | 要求               |
| ------------- | ------------------ | ------------------ |
| 函数/方法注释 | 紧贴在函数声明上方 | 不留空行           |
| 类注释        | 紧贴在类声明上方   | 不留空行           |
| 属性注释      | 紧贴在属性声明上方 | 不留空行           |
| 单行注释      | 放在代码行上方     | 与代码保持相同缩进 |

---

## 函数/方法注释要点

函数/方法注释必须包含：

1. **功能描述**：清晰描述函数的功能和用途
2. **入参说明**：每个参数的类型和用途
3. **出参说明**：返回值的类型和含义
4. **异常说明**：可能抛出的异常及其条件（如有）
5. **使用示例**：至少一个基本使用示例

### 联合类型参数

当参数为联合类型时，**必须**详细说明每个类型：

```typescript
@param input - The input data to process. Can be:
  - `string`: A string value to parse / 要解析的字符串值
  - `Buffer`: A buffer containing raw data / 包含原始数据的缓冲区
  - `ReadableStream`: A stream to read data from / 要读取数据的流
```

### 多种传参方式

支持多种传参方式时，提供**不同场景的使用示例**：

```typescript
@example
// Create user with name only
const user = createUser('John');

// Create user with options object
const user = createUser({ name: 'John', age: 25, email: 'john@example.com' });
```

---

## 执行流程

### 文件扫描流程

1. 接收用户指定的文件或目录
2. 递归扫描所有代码文件
3. 按语言类型分组处理
4. 生成处理计划

### 单文件处理流程

1. 读取文件内容
2. 解析代码结构（AST 或正则匹配）
3. 识别需要注释的代码元素
4. 检查现有注释的完整性
5. 生成符合规范的注释
6. 将注释插入到正确位置
7. 写入更新后的文件

### 进度报告格式

处理过程中实时报告进度：

```markdown
## 注释处理进度

### 已完成 (3/10)

- ✅ src/utils/helper.ts (添加了 5 个函数注释)
- ✅ src/models/user.ts (添加了 2 个类注释, 8 个属性注释)
- ✅ src/api/client.ts (添加了 3 个函数注释)

### 处理中

- 🔄 src/services/auth.ts

### 待处理 (6/10)

- ⏳ src/config/index.ts
- ...
```

---

## 快速参考

### 注释格式速查

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

### 注意事项速记

1. **只添加注释**：严禁修改任何代码内容
2. **保持一致性**：同一文件内注释风格必须一致
3. **准确性优先**：注释内容必须准确反映代码功能
4. **避免过度注释**：如果代码本身足够清晰，则不需要添加注释
5. **简洁明了**：注释应有实际价值
6. **示例可运行**：所有使用示例必须是可运行的代码

---

## 参考文档

- 📄 [comment-formats.md](references/comment-formats.md) - 详细格式示例
- 📄 [writing-style.md](references/writing-style.md) - 写作风格指南
- 📄 [quality-checklist.md](references/quality-checklist.md) - 质量验证清单
