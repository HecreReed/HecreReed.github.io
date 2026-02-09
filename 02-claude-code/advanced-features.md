---
layout: default
title: 高级功能
---

# Claude Code 高级功能

掌握了基础使用后，Claude Code 还有很多强大的高级功能。本章将介绍如何使用 Claude Code 进行服务器运维、处理专业领域问题，以及一些提高效率的高级技巧。

---

## 服务器运维

Claude Code 的一个强大之处在于它能执行命令行指令。这意味着很多可视化工具能做的事情，Claude Code 都能通过命令行完成。特别是在服务器运维场景下，Claude Code 可以成为你的得力助手。

### 远程服务器操作

Claude Code 可以通过 SSH 连接远程服务器，执行各种运维任务。

#### 使用公私钥认证（推荐）

在操作远程服务器时，强烈建议使用公私钥对而不是密码。这不仅更安全，也更方便 Claude Code 自动化操作。

**配置公私钥：**

```bash
# 生成密钥对（如果还没有）
ssh-keygen -t ed25519 -C "your_email@example.com"

# 将公钥复制到远程服务器
ssh-copy-id user@remote-server.com

# 测试连接
ssh user@remote-server.com
```

配置好后，你就可以让 Claude Code 直接操作远程服务器了：

```
你：帮我在服务器 user@example.com 上检查 nginx 状态

Claude Code：好的，我来检查...
[执行 ssh user@example.com "systemctl status nginx"]
Nginx 正在运行，状态正常。
```

#### 为什么不推荐使用密码

虽然 Claude Code 可以处理密码认证，但这存在安全风险：
- 密码可能在对话历史中留下记录
- 需要在命令中明文传递密码
- 无法实现真正的自动化（每次都要输入密码）

使用公私钥认证后，Claude Code 可以无缝地执行远程操作，既安全又高效。

### 文件传输

Claude Code 可以使用 `scp` 命令在本地和远程服务器之间传输文件。

**上传文件到服务器：**

```
你：把本地的 app.js 上传到服务器 /var/www/html/ 目录

Claude Code：好的，开始上传...
[执行 scp app.js user@example.com:/var/www/html/]
上传完成！
```

**从服务器下载文件：**

```
你：从服务器下载 /var/log/nginx/error.log 到本地

Claude Code：好的，开始下载...
[执行 scp user@example.com:/var/log/nginx/error.log ./]
下载完成！
```

**批量传输：**

```
你：把 dist 目录下的所有文件上传到服务器

Claude Code：好的，批量上传...
[执行 scp -r dist/* user@example.com:/var/www/html/]
所有文件已上传！
```

### 远程命令执行

Claude Code 可以在远程服务器上执行各种命令，完成复杂的运维任务。

**单条命令：**

```
你：在服务器上重启 nginx

Claude Code：[执行 ssh user@example.com "sudo systemctl restart nginx"]
Nginx 已重启！
```

**多条命令串联：**

使用 `&&` 连接符可以让多条命令依次执行，只有前一条成功才执行下一条：

```
你：在服务器上拉取最新代码并重启服务

Claude Code：好的，执行以下操作...
[执行 ssh user@example.com "cd /var/www/app && git pull && npm install && pm2 restart app"]
代码已更新，服务已重启！
```

**后台执行：**

使用 `&` 可以让命令在后台运行，不阻塞当前操作：

```
你：在服务器上启动一个长时间运行的任务

Claude Code：[执行 ssh user@example.com "nohup python3 long_task.py > output.log 2>&1 &"]
任务已在后台启动！
```

### 实际运维场景

**部署应用：**

```
你：帮我把这个 Node.js 应用部署到生产服务器

Claude Code：好的，开始部署流程...
1. 打包应用
   [执行 npm run build]
2. 上传到服务器
   [执行 scp -r dist/* user@prod-server.com:/var/www/app/]
3. 安装依赖
   [执行 ssh user@prod-server.com "cd /var/www/app && npm install --production"]
4. 重启服务
   [执行 ssh user@prod-server.com "pm2 restart app"]
部署完成！应用已在生产环境运行。
```

**日志分析：**

```
你：帮我分析服务器上最近的错误日志

Claude Code：好的，我来查看...
[执行 ssh user@example.com "tail -n 100 /var/log/app/error.log"]
发现以下问题：
- 数据库连接超时：15 次
- API 请求失败：8 次
- 内存不足警告：3 次

需要我帮你修复这些问题吗？
```

**系统监控：**

```
你：检查服务器的资源使用情况

Claude Code：[执行 ssh user@example.com "top -bn1 | head -20 && df -h && free -h"]
当前状态：
- CPU 使用率：45%
- 内存使用：8.2GB / 16GB (51%)
- 磁盘使用：120GB / 500GB (24%)
系统运行正常。
```

---

## 处理专业领域问题

Claude Code 虽然知识广泛，但在某些专业领域，它可能不了解最新的 API、特定的工具用法或者某些细节。这时候，你可以通过几种方式帮助它获取准确信息。

### 提供官方文档链接

当涉及到专业领域时，直接给 Claude Code 提供官方文档链接，让它学习后再工作。

**示例：LLVM/MLIR 开发**

比如你在做 LLVM 或 MLIR 相关开发，需要使用 `arith` dialect 的某些操作，但不确定 Claude Code 是否了解所有可用的 op：

```
你：我需要在 MLIR 中使用 arith dialect 的操作，但我不确定有哪些可用。
这是 arith dialect 的官方文档：https://mlir.llvm.org/docs/Dialects/ArithOps/
请你先学习一下这个文档，然后帮我实现一个整数加法的 pass。

Claude Code：好的，让我先查看文档...
[读取文档内容]
我了解了 arith dialect 的所有操作。对于整数加法，应该使用 arith.addi。
现在开始实现...
[编写代码]
完成！我使用了 arith.addi 操作来实现整数加法。
```

这种方式确保 Claude Code 使用的是最新、最准确的 API 信息。

### 让 Claude Code 主动搜索

对于不熟悉的领域，你可以明确要求 Claude Code 先进行网络搜索，再开始工作。

```
你：我需要实现一个 Rust 的异步 HTTP 服务器，使用 Tokio 框架。
但我不确定最新的最佳实践是什么，请你先 websearch 了解一下 2026 年的 Tokio 最佳实践，
然后再帮我实现。

Claude Code：好的，让我先搜索最新信息...
[执行 websearch]
我找到了 2026 年 Tokio 的最佳实践：
- 使用 Tokio 1.x 的最新版本
- 推荐使用 axum 作为 web 框架
- 异步运行时配置建议...

现在开始实现...
[编写代码]
完成！代码遵循了最新的最佳实践。
```

### 结合文档和搜索

对于复杂的专业问题，可以结合两种方式：

```
你：我在做 CUDA 编程，需要优化一个矩阵乘法的 kernel。
1. 先看看这个 CUDA 优化指南：https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/
2. 再搜索一下 2026 年最新的 CUDA 优化技巧
3. 然后帮我优化这段代码

Claude Code：好的，我会：
1. 学习官方优化指南
2. 搜索最新优化技巧
3. 应用到你的代码中

开始执行...
[学习文档]
[websearch]
[分析代码]
[优化代码]

完成！我应用了以下优化：
- 使用 shared memory 减少全局内存访问
- 优化线程块大小为 16x16
- 使用 memory coalescing
- 添加了 loop unrolling
性能预计提升 3-5 倍。
```

### 专业领域示例

**机器学习框架：**

```
你：我需要用 PyTorch 2.x 实现一个 Transformer 模型。
先看看官方文档：https://pytorch.org/docs/stable/nn.html#transformer-layers
然后帮我实现。
```

**区块链开发：**

```
你：我要写一个 Solidity 智能合约。
先搜索一下 2026 年 Solidity 的安全最佳实践，
特别是关于重入攻击的防护。
```

**游戏引擎：**

```
你：我在用 Godot 4.x 开发游戏，需要实现一个物理系统。
这是 Godot 物理引擎文档：https://docs.godotengine.org/en/stable/tutorials/physics/
请先学习后再帮我实现。
```

---

## Plan 模式

Plan 模式是 Claude Code 的一个强大功能，特别适合处理复杂的、多步骤的任务。

### 什么是 Plan 模式

在 Plan 模式下，Claude Code 不会立即开始修改代码，而是先制定一个详细的执行计划。这个计划会列出：
- 需要修改哪些文件
- 每个文件要做什么改动
- 可能遇到的问题
- 如何验证结果

你可以审核这个计划，确认无误后，Claude Code 才会开始真正的执行。

### 启动 Plan 模式

```bash
# 启动 Plan 模式
claude --plan

# 或者在对话中切换
你：进入 plan 模式
```

### Plan 模式的工作流程

```
你：我想重构整个用户认证模块，使用 JWT 替代 Session

Claude Code (Plan 模式)：好的，让我先制定一个计划...

[分析现有代码结构]
[制定重构方案]

重构计划：

1. 后端改动
   - models/user.js: 移除 session 相关字段，添加 JWT 配置
   - middleware/auth.js: 重写认证中间件，使用 JWT 验证
   - controllers/auth.js: 修改登录逻辑，返回 JWT token
   - utils/jwt.js: 新建文件，实现 JWT 生成和验证

2. 前端改动
   - services/auth.js: 修改 API 调用，使用 token 认证
   - store/user.js: 更新状态管理，存储 token
   - utils/request.js: 在请求头中添加 token

3. 测试
   - tests/auth.test.js: 更新测试用例

4. 配置
   - .env: 添加 JWT_SECRET 配置

预计影响：
- 需要修改 8 个文件
- 需要安装 jsonwebtoken 依赖
- 现有 session 数据需要迁移

风险评估：
- 需要用户重新登录
- 需要更新 API 文档

确认执行这个计划吗？

你：确认

Claude Code：开始执行计划...
[按计划逐步执行]
```

### Plan 模式的优势

- **降低风险**：在执行前就能发现潜在问题
- **提高效率**：避免走弯路，一次性做对
- **便于审核**：团队成员可以审核计划
- **学习价值**：通过计划了解 AI 的思路

---

## MCP 集成

MCP (Model Context Protocol) 允许 Claude Code 连接各种外部服务和工具。

### 常用 MCP 服务器

**数据库访问：**

```bash
# 配置 PostgreSQL MCP 服务器
claude config mcp add postgres \
  --command "npx @modelcontextprotocol/server-postgres" \
  --env DATABASE_URL="postgresql://user:pass@localhost/db"
```

使用：

```
你：查询数据库中所有活跃用户

Claude Code：[通过 MCP 连接数据库]
找到 1,234 个活跃用户。需要我导出数据吗？
```

**浏览器自动化：**

```bash
# 配置 Puppeteer MCP 服务器
claude config mcp add browser \
  --command "npx @modelcontextprotocol/server-puppeteer"
```

使用：

```
你：帮我测试一下登录流程是否正常

Claude Code：[启动浏览器]
[自动填写表单]
[点击登录按钮]
[验证跳转]
登录流程正常，所有步骤都成功了。
```

---

## 高级命令技巧

### 条件执行

```bash
# 只有前一条命令成功才执行下一条
command1 && command2 && command3

# 前一条失败才执行下一条
command1 || command2

# 无论成功失败都执行下一条
command1 ; command2
```

### 管道和重定向

```bash
# 管道：将前一个命令的输出作为后一个命令的输入
cat file.txt | grep "error" | wc -l

# 重定向输出到文件
command > output.txt

# 追加到文件
command >> output.txt

# 重定向错误输出
command 2> error.txt

# 同时重定向标准输出和错误输出
command > output.txt 2>&1
```

### 后台任务

```bash
# 在后台运行
command &

# 使用 nohup 防止终端关闭后任务停止
nohup command &

# 查看后台任务
jobs

# 将后台任务调到前台
fg %1
```

---

## 实用技巧总结

1. **服务器运维**：使用公私钥认证，避免密码泄露
2. **专业领域**：提供文档链接或让 Claude Code 先搜索
3. **复杂任务**：使用 Plan 模式，先规划再执行
4. **命令串联**：善用 `&&`、`||`、`;` 等连接符
5. **远程操作**：结合 SSH、SCP 实现自动化运维
6. **MCP 集成**：扩展 Claude Code 的能力边界

---

## 下一步

掌握了高级功能后，你可以：

1. 查看[最佳实践](best-practices)，学习如何更高效地使用 Claude Code
2. 阅读[实战案例](../07-projects/)，看看这些功能的实际应用
3. 探索[常见问题](../08-resources/faq)，解决使用中的疑惑

---

[返回目录](index) | [上一章：基础使用](basic-usage) | [下一章：最佳实践](best-practices)
