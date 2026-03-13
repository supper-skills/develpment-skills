# 实施计划模板

此模板展示实施计划的标准结构。根据项目编程语言调整所有文件扩展名、代码示例和测试命令。

---

# [功能名称] 实施计划

> **对于代理工作者：** 必需：使用 executing-plans 来实施此计划。步骤使用复选框（`- [ ]`）语法进行跟踪。

**目标：** [一句话描述此功能构建什么]

**架构：** [2-3 句关于方法]

**技术栈：** [关键技术/库]

---

## 文件结构

### 新建文件
- `path/to/new/file.<ext>` - 职责描述
- `path/to/another/file.<ext>` - 职责描述

### 修改文件
- `path/to/existing/file.<ext>` - 将被修改的内容
- `path/to/another/existing.<ext>` - 将被修改的内容

### 测试文件
- `tests/path/to/test_file.<ext>` - 测试职责

---

## Chunk 1: [组件名称]

### 任务 1：[组件名称]

**文件：**
- 创建：`exact/path/to/file.<ext>`
- 修改：`exact/path/to/existing.<ext>#L123-145`
- 测试：`tests/exact/path/to/test.<ext>`

- [ ] **步骤 1：编写失败测试**

```<language>
// 根据您的语言调整
// 示例：TypeScript with Jest
describe('functionName', () => {
  it('should return expected result for given input', () => {
    const result = functionName(input);
    expect(result).toBe(expected);
  });
});
```

- [ ] **步骤 2：运行测试验证失败**

运行：`<test-command>`（例如 `npm test`、`pytest`、`cargo test`）
预期：失败，显示适当的错误消息

- [ ] **步骤 3：编写最小实现**

```<language>
// 通过测试的最小实现
// 根据您的语言调整
export function functionName(input: InputType): OutputType {
  return expected;
}
```

- [ ] **步骤 4：运行测试验证通过**

运行：`<test-command>`
预期：通过

---

### 任务 2：[另一个组件]

**文件：**
- 创建：`exact/path/to/another.<ext>`
- 测试：`tests/exact/path/to/test_another.<ext>`

- [ ] **步骤 1：编写失败测试**

```<language>
// 根据您的语言调整
```

- [ ] **步骤 2：运行测试验证失败**

运行：`<test-command>`
预期：失败

- [ ] **步骤 3：编写最小实现**

```<language>
// 根据您的语言调整
```

- [ ] **步骤 4：运行测试验证通过**

运行：`<test-command>`
预期：通过

---

## Chunk 2: [集成/下一个组件]

[继续按相同模式添加更多任务...]

---

## 各语言示例

### TypeScript/JavaScript (Jest)

```typescript
describe('UserService', () => {
  it('should create a new user', () => {
    const user = UserService.create({ name: 'John' });
    expect(user.name).toBe('John');
  });
});
```

运行：`npm test` 或 `jest tests/path/test.ts`

### Python (pytest)

```python
def test_create_user():
    user = UserService.create(name='John')
    assert user.name == 'John'
```

运行：`pytest tests/path/test.py::test_create_user -v`

### Rust

```rust
#[test]
fn test_create_user() {
    let user = UserService::create("John");
    assert_eq!(user.name, "John");
}
```

运行：`cargo test test_create_user`

### Go

```go
func TestCreateUser(t *testing.T) {
    user := UserService.Create("John")
    if user.Name != "John" {
        t.Errorf("expected John, got %s", user.Name)
    }
}
```

运行：`go test ./path/to/package -run TestCreateUser`

---

## 注意事项

- 每个块应 ≤1000 行
- 每个任务遵循 TDD：测试 → 失败 → 实现 → 通过
- 每个通过的测试后提交
- 所有示例应根据项目编程语言进行调整
