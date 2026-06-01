---
name: commit-helper
description: Conventional Commits 规范的 commit message 助手。当用户提到"提交"、"commit"、"提交信息"、"commit message"、"git commit"，或输入 `/commit-helper` 时使用此技能。帮助用户生成符合 Conventional Commits 规范的 commit message，支持完整 git 工作流：检查变更、分析类型、生成信息，并提供交互式选项是否执行 commit。确保在用户需要提交代码更改时主动提供帮助，即使他们没有明确提及 Conventional Commits。
---

# Conventional Commits 助手

帮助生成符合 Conventional Commits 规范的 commit message，并支持完整的 git 提交工作流。

## 使用场景

当你有以下需求时，这个技能会自动帮你：
- 需要提交代码但不确定如何写规范的 commit message
- 想要遵循 Conventional Commits 规范但不知道具体格式
- 需要分析代码变更并自动确定 commit 类型
- 希望简化 git 提交流程，从检查变更到生成信息一气呵成

---

## 工作流程

### 1. 检查 git 状态

首先检查当前 git 仓库的状态：
- 运行 `git status` 查看未跟踪和已修改的文件
- 运行 `git diff --staged` 或 `git diff` 查看具体变更内容
- 识别变更范围：是新增功能、修复 bug、重构代码还是文档更新

### 2. 分析变更类型

根据代码变更内容，确定合适的 Conventional Commits 类型：

| 类型 | 使用场景 | 判断依据 |
|------|----------|----------|
| **feat** | 新增功能 | 新增文件、添加新功能、实现新特性 |
| **fix** | 修复 bug | 修改错误逻辑、修复崩溃问题、解决缺陷 |
| **chore** | 日常维护 | 更新依赖、配置文件修改、构建脚本调整 |
| **docs** | 文档更新 | 修改 README、注释、文档文件 |
| **style** | 代码风格 | 格式化代码、调整缩进、不影响功能的样式修改 |
| **refactor** | 代码重构 | 重构代码结构、优化性能但不改变功能 |
| **test** | 测试相关 | 添加或修改测试用例 |
| **perf** | 性能优化 | 提升性能的代码修改 |
| **ci** | CI/CD 相关 | 修改 CI/CD 配置文件 |

### 3. 确定作用域（可选）

分析变更影响的模块或组件，确定合适的作用域：
- **前端**：`feat(ui)`, `fix(auth)`, `refactor(components)`
- **后端**：`feat(api)`, `fix(database)`, `chore(config)`
- **通用**：`docs(readme)`, `test(unit)`, `ci(github)`

### 4. 生成 commit message

根据分析结果，生成符合规范的 commit message：

**基础格式**：`type(scope): description`

要求：
- **type**：必须小写，使用上述标准类型
- **scope**：可选，括号内小写，简短描述影响范围
- **description**：简洁描述，使用祈使句现在时（如"add"而非"added"或"adds"）
- **长度**：描述部分不超过72个字符

### 5. 提供交互式选项

生成 commit message 后，提供以下选项：
1. **仅显示信息**：只输出 commit message，让用户自己执行 git commit
2. **执行提交**：询问确认后，自动执行 `git add` 和 `git commit -m "message"`
3. **重新生成**：如果不满意，可以重新分析并生成新的 message
4. **详细模式**：显示分析过程和选择理由

### 6. 智能格式判断

根据上下文自动选择输出格式：
- **首次使用或复杂变更**：提供详细版，包含分析过程和类型说明
- **简单变更或熟悉用户**：提供简洁版，直接输出 commit message
- **用户明确请求**：尊重用户的格式偏好（如"简洁点"或"详细说明"）

---

## 输出格式

### 简洁版（默认）

```
feat(auth): add user login functionality
```

### 详细版（适合学习或复杂变更）

```
## 生成的 commit message:
feat(auth): add user login functionality

## 分析过程:
1. **变更类型**: feat (新增功能)
   - 新增了用户登录相关的代码文件
   - 实现了登录表单和认证逻辑
2. **作用域**: auth (认证模块)
   - 变更主要集中在认证相关文件
3. **描述**: "add user login functionality"
   - 简洁描述新增的功能
   - 使用祈使句现在时

## 建议的 git 命令:
git add .
git commit -m "feat(auth): add user login functionality"
```

---

## 示例

### 示例 1：新增功能

**用户输入**：
> 我刚添加了用户注册功能，包括前端表单和后端API

**技能输出**（详细版）：
```
## 生成的 commit message:
feat(auth): implement user registration

## 分析过程:
1. **变更类型**: feat (新增功能)
   - 新增用户注册功能，属于新特性
2. **作用域**: auth (认证模块)
   - 注册功能属于用户认证范畴
3. **描述**: "implement user registration"
   - 准确描述实现的功能

## 交互选项:
1. 使用此信息提交 (git add & git commit)
2. 只显示信息，我自己提交
3. 重新生成
4. 切换为简洁版
```

### 示例 2：修复 bug

**用户输入**：
> 修复了登录页面在移动端的布局问题

**技能输出**（简洁版）：
```
fix(ui): correct mobile layout for login page
```

### 示例 3：文档更新

**用户输入**：
> 更新了 README 文件，添加了安装说明

**技能输出**：
```
docs(readme): add installation instructions
```

---

## Conventional Commits 规范要点

### 基本结构
```
<type>(<scope>): <description>
```

### 类型说明
- **feat**: 新增功能（用户可感知的新特性）
- **fix**: 修复 bug（解决问题、错误）
- **docs**: 仅文档更改
- **style**: 不影响代码含义的更改（空格、格式化等）
- **refactor**: 既不修复错误也不添加功能的代码更改
- **perf**: 提高性能的代码更改
- **test**: 添加或修正测试
- **chore**: 构建过程或辅助工具的变动

### 最佳实践
1. **描述使用祈使句**：如"add"、"fix"、"update"，而不是"added"、"fixes"
2. **首字母小写**：描述部分不要大写开头
3. **不加句号**：描述末尾不要加句号
4. **简洁明了**：用最少的词表达清楚变更内容

---

## 处理原则

1. **准确性优先**：确保 commit 类型准确反映变更本质
2. **实用性导向**：生成的 commit message 要实际可用，不追求过度复杂
3. **教育性辅助**：对不熟悉规范的用户，提供解释和指导
4. **灵活性适应**：根据用户熟练程度调整输出详略程度
5. **安全第一**：涉及 git 操作时，先确认再执行，避免误操作

## 注意事项

- 执行 git commit 前务必确认用户意图
- 对于重大变更，建议用户添加更详细的 commit body
- 如果变更涉及多个类型，选择最主要的一个
- 保持中文友好：对中文用户使用中文解释，但 commit message 本身用英文