# 常见计划模式库

预定义的任务模板，可快速复用于常见场景。

---

## 使用方式

当识别到以下常见模式时，可直接引用对应模板。

---

## 模式 1：CRUD 模块

**适用场景**：数据增删改查操作

**典型文件结构**：

| 文件 | 职责 |
|------|------|
| `src/models/<entity>.ts` | 数据模型定义 |
| `src/repositories/<entity>Repository.ts` | 数据访问层 |
| `src/services/<entity>Service.ts` | 业务逻辑层 |
| `src/controllers/<entity>Controller.ts` | API 控制器 |
| `tests/<entity>.test.ts` | 测试文件 |

**典型任务顺序**：
1. 定义数据模型
2. 实现 Repository（CRUD 操作）
3. 实现 Service（业务逻辑）
4. 实现 Controller（API 端点）
5. 集成测试

---

## 模式 2：认证模块

**适用场景**：用户认证授权

**典型文件结构**：

| 文件 | 职责 |
|------|------|
| `src/auth/jwtHandler.ts` | JWT 令牌处理 |
| `src/auth/middleware.ts` | 认证中间件 |
| `src/auth/refreshHandler.ts` | 令牌刷新 |
| `src/services/userService.ts` | 用户服务 |
| `tests/auth.test.ts` | 认证测试 |

**典型任务顺序**：
1. 实现 JWT 生成和验证
2. 实现认证中间件
3. 实现登录/登出逻辑
4. 实现令牌刷新机制
5. 权限验证

---

## 模式 3：API 集成

**适用场景**：第三方服务集成

**典型文件结构**：

| 文件 | 职责 |
|------|------|
| `src/clients/<service>Client.ts` | API 客户端 |
| `src/adapters/<service>Adapter.ts` | 数据适配器 |
| `src/services/<service>Service.ts` | 业务封装 |
| `src/mocks/<service>Mock.ts` | 模拟实现 |
| `tests/<service>.test.ts` | 集成测试 |

**典型任务顺序**：
1. 定义 API 客户端接口
2. 实现请求/响应处理
3. 实现数据适配层
4. 实现错误处理和重试
5. 创建模拟实现用于测试

---

## 模式 4：中间件/插件

**适用场景**：请求处理管道、插件系统

**典型文件结构**：

| 文件 | 职责 |
|------|------|
| `src/middleware/<name>.ts` | 中间件实现 |
| `src/types/middleware.ts` | 类型定义 |
| `tests/middleware/<name>.test.ts` | 测试文件 |

**典型任务顺序**：
1. 定义中间件接口
2. 实现核心逻辑
3. 实现配置选项
4. 错误处理
5. 集成测试

---

## 模式引用方式

在计划中引用模式：

```markdown
### 任务组：用户管理 CRUD

> 引用模式：CRUD 模块
> 实体：User

[基于模式模板编写具体任务...]
```
