# 实施计划模板

此模板展示实施计划的标准结构。根据项目编程语言调整所有文件扩展名、代码示例和测试命令。

---

## 目录

- [纲领文件模板](#纲领文件模板)
- [单一子系统计划模板](#单一子系统计划模板)
- [多子系统计划模板](#多子系统计划模板)
- [常见计划模式模板](#常见计划模式模板)
- [各语言示例](#各语言示例)
- [分块指南](#分块指南)
- [变更影响分析模板](#变更影响分析模板)
- [注意事项](#注意事项)

---

## 纲领文件模板

**路径**：`design/plans/YYYY-MM-DD-<topic>-outline.md`

纲领文件统一管理会话状态、决策记录、项目信息和子系统进度。

```markdown
# [项目名称] 实施计划纲领

## 会话状态

- **规格文档**: [来源规格文档路径]
- **当前阶段**: 阶段 X/7: [阶段名称]
- **当前处理**: [子系统名称 或 "单一子系统"]
- **下一步行动**: [具体行动]
- **待处理问题**: [问题列表，如无则留空]

## 决策记录

> 记录计划编写过程中的关键决策及其理由，防止重复讨论已决策问题。

| 决策                  | 理由                 | 影响范围 | 决策时间   |
| --------------------- | -------------------- | -------- | ---------- |
| 使用 JWT 而非 Session | 无状态、易扩展       | 认证模块 | YYYY-MM-DD |
| 选择 PostgreSQL       | 团队熟悉、JSON 支持  | 数据层   | YYYY-MM-DD |
| 采用微服务架构        | 独立部署、技术栈灵活 | 整体架构 | YYYY-MM-DD |

## 项目概述

[一句话描述项目目标]

## 子系统划分（多子系统项目填写）

### 子系统 A：[名称]

- **范围**：[功能范围描述]
- **依赖**：无
- **计划文档**：`design/plans/YYYY-MM-DD-subsystem-a.md`
- **状态**：⏳ 待编写 / 🔄 进行中 / ✅ 已完成

### 子系统 B：[名称]

- **范围**：[功能范围描述]
- **依赖**：子系统 A
- **计划文档**：`design/plans/YYYY-MM-DD-subsystem-b.md`
- **状态**：⏳ 待编写

### 子系统 C：[名称]

- **范围**：[功能范围描述]
- **依赖**：子系统 A、子系统 B
- **计划文档**：`design/plans/YYYY-MM-DD-subsystem-c.md`
- **状态**：⏳ 待编写

## 执行顺序（多子系统项目填写）

1. 子系统 A（无依赖，优先执行）
2. 子系统 B（依赖 A）
3. 子系统 C（依赖 A、B）

## 共享组件（多子系统项目填写）

| 组件     | 使用子系统 | 计划位置            |
| -------- | ---------- | ------------------- |
| [组件名] | A, B, C    | 子系统 A 计划中定义 |
| [组件名] | B, C       | 子系统 B 计划中定义 |

## 变更历史

> 记录计划的变更历史，便于追溯和影响分析。

| 变更时间   | 变更内容   | 影响范围 | 变更原因     |
| ---------- | ---------- | -------- | ------------ |
| YYYY-MM-DD | 增加缓存层 | 子系统 A | 性能优化需求 |

## 全局约束

- [适用于所有子系统/整个项目的约束]
- [技术栈要求]
- [编码规范要求]
```

**单一子系统项目**：只需填写"会话状态"、"决策记录"、"项目概述"、"全局约束"，其他部分省略。

---

## 单一子系统计划模板

**路径**：`design/plans/YYYY-MM-DD-<feature-name>.md`

````markdown
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
````

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

````

---

## 多子系统计划模板（子系统文档）

**路径**：`design/plans/YYYY-MM-DD-subsystem-<name>.md`

```markdown
# [子系统名称] 实施计划

> **对于代理工作者：** 必需：使用 executing-plans 来实施此计划。步骤使用复选框（`- [ ]`）语法进行跟踪。

**目标：** [一句话描述此子系统构建什么]

**架构：** [2-3 句关于方法]

**技术栈：** [关键技术/库]

**所属纲领：** `design/plans/YYYY-MM-DD-<project>-outline.md`

**依赖子系统：** [列出依赖的其他子系统，如无则为"无"]

---

## 文件结构

### 新建文件
- `path/to/new/file.<ext>` - 职责描述

### 修改文件
- `path/to/existing/file.<ext>` - 将被修改的内容

### 测试文件
- `tests/path/to/test_file.<ext>` - 测试职责

### 共享组件（供其他子系统使用）
- `path/to/shared/component.<ext>` - [使用子系统列表]

---

## Chunk 1: [组件名称]

### 任务 1：[组件名称]

**文件：**
- 创建：`exact/path/to/file.<ext>`
- 测试：`tests/exact/path/to/test.<ext>`

- [ ] **步骤 1：编写失败测试**

```<language>
// 根据您的语言调整
````

- [ ] **步骤 2：运行测试验证失败**

运行：`<test-command>`
预期：失败，显示适当的错误消息

- [ ] **步骤 3：编写最小实现**

```<language>
// 通过测试的最小实现
```

- [ ] **步骤 4：运行测试验证通过**

运行：`<test-command>`
预期：通过

---

[继续添加更多任务和块...]

````

---

## 常见计划模式模板

### 模式 1：CRUD 模块

**适用场景**：数据增删改查操作

**引用方式**：

```markdown
### 任务组：[实体名称] CRUD

> 引用模式：CRUD 模块
> 实体：[EntityName]

**文件：**
- 创建：`src/models/[entity].ts` - 数据模型定义
- 创建：`src/repositories/[entity]Repository.ts` - 数据访问层
- 创建：`src/services/[entity]Service.ts` - 业务逻辑层
- 创建：`src/controllers/[entity]Controller.ts` - API 控制器
- 创建：`tests/[entity].test.ts` - 测试文件

[基于模式模板编写具体任务...]
````

### 模式 2：认证模块

**适用场景**：用户认证授权

**引用方式**：

```markdown
### 任务组：用户认证

> 引用模式：认证模块

**文件：**

- 创建：`src/auth/jwtHandler.ts` - JWT 令牌处理
- 创建：`src/auth/middleware.ts` - 认证中间件
- 创建：`src/auth/refreshHandler.ts` - 令牌刷新
- 创建：`src/services/userService.ts` - 用户服务
- 创建：`tests/auth.test.ts` - 认证测试

[基于模式模板编写具体任务...]
```

### 模式 3：API 集成

**适用场景**：第三方服务集成

**引用方式**：

```markdown
### 任务组：[服务名称] 集成

> 引用模式：API 集成
> 服务：[ServiceName]

**文件：**

- 创建：`src/clients/[service]Client.ts` - API 客户端
- 创建：`src/adapters/[service]Adapter.ts` - 数据适配器
- 创建：`src/services/[service]Service.ts` - 业务封装
- 创建：`src/mocks/[service]Mock.ts` - 模拟实现
- 创建：`tests/[service].test.ts` - 集成测试

[基于模式模板编写具体任务...]
```

---

## 各语言示例

### TypeScript/JavaScript (Jest)

```typescript
describe("UserService", () => {
  it("should create a new user", () => {
    const user = UserService.create({ name: "John" });
    expect(user.name).toBe("John");
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

## 分块指南

### 分块粒度标准

| 指标   | 标准       | 原因               |
| ------ | ---------- | ------------------ |
| 行数   | 300-500 行 | 适配 AI 上下文窗口 |
| 任务数 | 5-10 个    | 保持逻辑完整性     |
| 依赖   | 块内自洽   | 减少跨块引用       |

### 分块边界识别

1. **按功能模块分块**：相关任务归为一块
2. **按实施阶段分块**：如"基础设施"、"核心功能"、"集成测试"
3. **按子系统分块**：每个子系统独立一块

### 分块命名建议

- `Chunk 1: 基础设施` - 项目初始化、依赖安装
- `Chunk 2: 数据模型` - 核心数据结构
- `Chunk 3: 业务逻辑` - 主要功能实现
- `Chunk 4: API 接口` - 对外接口
- `Chunk 5: 集成测试` - 端到端测试

---

## 变更影响分析模板

当发生变更时，使用以下模板记录影响分析：

```markdown
## 变更影响分析

**变更内容**：[具体变更描述]

**变更类型**：新增功能 / 修改需求 / 删除功能 / 技术调整 / 优先级调整

**直接影响的任务**：

- 任务 X：[如何影响]
- 任务 Y：[如何影响]

**间接影响的任务**：

- 任务 Z：[如何影响]

**影响的子系统**：

- 子系统 A：[如何影响]

**需要更新的文档**：

- [ ] 计划文档 A
- [ ] 纲领文件

**新增决策**（如有）：
| 决策 | 理由 | 影响范围 | 决策时间 |
| ---------- | -------- | -------- | ---------- |
| [决策内容] | [为什么] | [影响] | YYYY-MM-DD |
```

---

## 注意事项

- 每个块应 300-500 行，逻辑自洽
- 每个任务遵循 TDD：测试 → 失败 → 实现 → 通过
- 每个通过的测试后提交
- 所有示例应根据项目编程语言进行调整
- 多子系统项目必须创建纲领文件
- 每个子系统完成后更新纲领文件中的状态
- 纲领文件统一管理会话状态、决策记录、项目信息
- 关键决策必须记录在纲领文件的"决策记录"表格中
- 变更必须记录在纲领文件的"变更历史"表格中
- 常见场景可引用预定义模式提高效率
