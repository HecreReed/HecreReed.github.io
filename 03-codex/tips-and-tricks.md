---
layout: default
title: 实战技巧
---

# Codex 实战技巧

本章将介绍 Codex 的实用技巧，帮助你更高效地使用这个强大的工具。

---

## 与 Claude 配合使用

Codex 和 Claude Code 各有所长，最佳实践是将它们结合使用。

### Claude 开发，Codex 检查

这是一个非常实用的工作流程：

**第一步：使用 Claude 快速开发**

Claude Code 擅长快速开发和迭代，特别是在前端、Python 等领域。你可以用 Claude 快速搭建项目框架、实现功能原型。

```bash
# 在项目目录启动 Claude Code
claude --bypass

# 让 Claude 快速开发功能
你：帮我实现一个用户登录功能，包括前端表单和后端 API
```

Claude 会快速生成代码，但可能存在一些小 bug 或不够精准的地方。

**第二步：使用 Codex 检查和优化**

开发完成后，切换到 Codex 进行代码审查：

```bash
# 在同一个项目目录启动 Codex
codex

# 让 Codex 检查 Claude 生成的代码
你：请检查这个登录功能的代码，看看有没有安全问题、性能问题或 bug
```

Codex 会仔细分析代码，找出潜在问题：
- 安全漏洞（SQL 注入、XSS 等）
- 性能问题（不必要的循环、内存泄漏等）
- 逻辑错误（边界条件、异常处理等）
- 代码规范（命名、结构等）

**第三步：Codex 进一步开发**

如果需要在现有项目基础上继续开发，Codex 是更好的选择：

```
你：在这个登录功能的基础上，添加双因素认证（2FA）
```

Codex 会准确理解现有代码结构，在不破坏原有功能的前提下添加新功能。它对大型项目的理解能力更强，修改更精准。

### 为什么这样配合效果好

- **Claude 的优势**：快速、灵活、适合从零开始
- **Codex 的优势**：精准、严谨、适合在现有基础上改进
- **结合使用**：既保证开发速度，又保证代码质量

---

## 上下文管理

Codex 和 Claude Code 一样，会对长对话进行自动 summary（摘要）。

### 自动摘要机制

当对话历史过长时，Codex 会自动总结之前的内容：
- 保留关键的代码修改
- 记住重要的决策和讨论
- 压缩不重要的细节

这个机制让你可以进行长时间的连续开发，而不用担心上下文溢出。

### 利用上下文的技巧

**1. 建立项目理解**

在开始工作前，让 Codex 先理解项目：

```
你：这是一个 React + TypeScript 的电商项目，使用 Redux 管理状态，
后端是 Node.js + Express + PostgreSQL。
请先浏览一下项目结构，理解整体架构。

Codex：[浏览项目文件]
我已经理解了项目结构：
- 前端：src/components、src/pages、src/store
- 后端：server/routes、server/controllers、server/models
- 数据库：使用 Sequelize ORM
...
```

建立了这个上下文后，后续的对话 Codex 都会记住项目的整体结构。

**2. 引用之前的讨论**

Codex 会记住之前的对话，你可以直接引用：

```
你：还记得我们之前讨论的用户认证方案吗？现在按照那个方案实现。

Codex：记得，我们决定使用 JWT + Refresh Token 的方案。
现在开始实现...
```

**3. 分阶段开发**

对于复杂任务，可以分阶段进行，Codex 会记住每个阶段的成果：

```
第一天：
你：先实现用户注册功能
Codex：[实现注册功能]

第二天：
你：在昨天的注册功能基础上，添加邮箱验证
Codex：好的，我记得昨天实现的注册功能，现在添加邮箱验证...
```

**4. 主动提醒关键信息**

如果担心 Codex 忘记重要信息，可以主动提醒：

```
你：提醒一下，这个项目使用的是 PostgreSQL 13，
不支持某些新特性，写 SQL 时要注意兼容性。

Codex：明白，我会注意 PostgreSQL 13 的兼容性。
```

---

## Skills 功能（Codex App）

Codex App 提供了强大的 Skills 功能，可以自动化常见的开发任务。

### 什么是 Skills

Skills 是预定义的工作流程，通过 `SKILLS.md` 文件配置。它可以让你用简单的命令触发复杂的操作，避免重复输入相同的提示词。

### 创建 Skills

在项目根目录创建 `SKILLS.md` 文件：

```markdown
# Project Skills

## /review
Review the code for:
- Security vulnerabilities
- Performance issues
- Code style consistency
- Potential bugs

## /test
Run all tests and analyze failures:
1. Run unit tests
2. Run integration tests
3. If any test fails, analyze the error and suggest fixes

## /deploy
Deploy the application:
1. Run tests
2. Build the project
3. Upload to server
4. Restart services
5. Verify deployment

## /refactor [file]
Refactor the specified file:
- Improve code structure
- Extract reusable functions
- Add proper error handling
- Update documentation
```

### 使用 Skills

配置好后，就可以用简单的命令触发：

```
你：/review

Codex：开始代码审查...
[检查安全漏洞]
[检查性能问题]
[检查代码风格]
发现 3 个需要改进的地方：
1. ...
2. ...
3. ...
```

```
你：/test

Codex：运行测试...
[执行单元测试]
[执行集成测试]
所有测试通过！
```

```
你：/deploy

Codex：开始部署流程...
[运行测试]
[构建项目]
[上传到服务器]
[重启服务]
[验证部署]
部署成功！应用已在生产环境运行。
```

### Skills 的优势

1. **避免重复**：不用每次都输入长长的提示词
2. **标准化流程**：确保每次执行相同的步骤
3. **团队协作**：团队成员可以共享 Skills 配置
4. **快速触发**：一个命令完成复杂任务

### 高级 Skills 技巧

**带参数的 Skills：**

```markdown
## /add-feature [feature-name]
Add a new feature:
1. Create feature branch: feature/[feature-name]
2. Generate boilerplate code
3. Add tests
4. Update documentation
```

使用：
```
你：/add-feature user-profile

Codex：创建功能分支 feature/user-profile...
[生成代码]
[添加测试]
[更新文档]
完成！
```

**条件执行：**

```markdown
## /smart-deploy
Smart deployment:
- If tests fail, stop and report errors
- If on main branch, deploy to production
- If on develop branch, deploy to staging
- Otherwise, deploy to test environment
```

**组合 Skills：**

```markdown
## /full-check
Complete project check:
1. Run /review
2. Run /test
3. Check dependencies for updates
4. Generate coverage report
```

---

## 其他实用技巧

### 1. 使用 xhigh 模式处理关键任务

对于重要的代码修改，不要吝啬使用 xhigh 模式：

```
你：[使用 xhigh 模式] 修复这个内存泄漏问题，这是生产环境的关键 bug
```

虽然慢，但一次就能修对，比反复调试节省时间。

### 2. 明确指定编程范式

如果项目有特定的编程风格，明确告诉 Codex：

```
你：这个项目使用函数式编程风格，避免使用 class，
多使用 pure function 和 immutable data。
```

### 3. 提供测试用例

让 Codex 理解预期行为的最好方式是提供测试用例：

```
你：实现一个函数 parseDate(str)，要求：
- parseDate("2026-02-09") 返回 Date 对象
- parseDate("invalid") 返回 null
- parseDate(null) 返回 null
```

### 4. 分步验证

对于复杂修改，让 Codex 分步执行并验证：

```
你：重构这个函数，但是分步进行：
1. 先提取重复的逻辑
2. 运行测试确保功能不变
3. 再优化性能
4. 最后添加错误处理
每一步完成后等我确认再继续。
```

### 5. 利用 Codex 学习代码

Codex 是很好的代码导师：

```
你：这个算法是怎么工作的？为什么要这样实现？
有没有更好的方案？

Codex：这个算法使用了动态规划...
[详细解释]
[提供替代方案]
[分析优缺点]
```

### 6. 代码迁移

Codex 擅长代码迁移和转换：

```
你：把这个 JavaScript 代码转换成 TypeScript，
添加完整的类型定义。
```

```
你：把这个 Python 2 代码升级到 Python 3，
注意处理所有不兼容的地方。
```

### 7. 性能优化

让 Codex 分析性能瓶颈：

```
你：这个函数运行很慢，帮我分析性能瓶颈并优化。
```

Codex 会：
- 识别时间复杂度问题
- 找出不必要的计算
- 建议更高效的算法
- 提供优化后的代码

### 8. 安全审计

定期让 Codex 审计代码安全：

```
你：审计这个 API 接口的安全性，检查：
- SQL 注入
- XSS 攻击
- CSRF 攻击
- 权限控制
- 敏感信息泄露
```

---

## 工作流程建议

### 日常开发流程

1. **早上**：用 Codex 审查昨天的代码，发现问题
2. **开发时**：用 Claude 快速实现新功能
3. **下午**：用 Codex 检查和优化代码
4. **提交前**：用 Codex 做最后的安全和性能检查

### 大型重构流程

1. **规划阶段**：用 Codex xhigh 模式制定重构计划
2. **执行阶段**：分模块重构，每个模块完成后用 Codex 验证
3. **测试阶段**：用 Codex 生成测试用例，确保功能不变
4. **优化阶段**：用 Codex 优化性能和代码质量

### Bug 修复流程

1. **定位问题**：用 Codex 分析日志和错误信息
2. **理解原因**：让 Codex 解释为什么会出现这个 bug
3. **修复代码**：用 Codex xhigh 模式修复
4. **添加测试**：用 Codex 生成测试用例，防止回归

---

## 下一步

掌握了这些技巧后，你可以：

1. 查看[应用场景](use-cases)，了解 Codex 的更多用途
2. 学习其他工具：[Gemini](../04-gemini/)、[Grok](../05-grok/)
3. 查看[实战项目](../07-projects/)，看看实际应用

---

[返回目录](index) | [上一章：API 使用](api-usage) | [下一章：应用场景](use-cases)

---

## 参考资料

- [Codex Skills 完全指南：自动化提示词](https://medium.com/@proflead/codex-skills-explained-the-complete-guide-to-automating-your-prompts-26dd5a89d580)
- [如何使用 Codex App 的 Skills 功能](https://peggie7191.medium.com/how-to-use-the-skills-feature-in-the-codex-app-d20e570db4c8)
- [Codex App 超级指南 2026](https://kingy.ai/ai/the-codex-app-super-guide-2026-from-hello-world-to-worktrees-skills-mcp-ci-and-enterprise-governance/)
- [Codex Skills 101：使用 SKILLS.md 构建可复用工作流](https://dev.to/proflead/codex-skills-101-build-reusable-ai-workflows-with-skillsmd-42fe)
- [Codex Skills 深度解析：渐进式披露、触发器和最佳实践](https://habr.com/en/articles/984916/)
- [初学者应该使用的 Skills 库](https://medium.com/@markchen69/the-codex-app-just-shipped-heres-the-skills-library-beginners-should-start-with-0c05011c2a19)
- [Codex CLI vs Claude Code：准确性还是速度？](https://smartscope.blog/en/generative-ai/chatgpt/codex-vs-claude-code-2026-benchmark/)
- [Codex 使用最佳实践](https://community.openai.com/t/best-practices-for-using-codex/1373143)
- [Codex CLI 权威指南：从安装到生产工作流](https://jpcaparas.medium.com/the-definitive-guide-to-codex-cli-from-first-install-to-production-workflows-a9f1e7c887ab)
- [Claude Code vs OpenAI Codex：2026 年哪个更好？](https://northflank.com/blog/claude-code-vs-openai-codex)
