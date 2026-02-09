---
layout: default
title: 安装与配置
---

# Claude Code 安装与配置

本章将详细介绍如何在不同操作系统上安装 Claude Code，以及如何进行各种配置。

---

## 系统要求

在开始安装之前，确保你的系统满足以下要求：

- **操作系统**：macOS 10.15+、Linux（主流发行版）、Windows 10/11
- **Node.js**：16.0 或更高版本（推荐使用 LTS 版本）
- **Git**：2.0 或更高版本
- **终端**：支持 ANSI 颜色的现代终端
- **网络**：稳定的互联网连接

---

## macOS 安装

macOS 是 Claude Code 支持最好的平台，安装过程非常简单。

### 方法一：使用 Homebrew（推荐）

```bash
# 安装 Homebrew（如果还没有）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装 Claude Code
brew install anthropics/tap/claude-code

# 验证安装
claude --version
```

### 方法二：使用 npm

```bash
# 全局安装
npm install -g @anthropics/claude-code

# 验证安装
claude --version
```

### 方法三：使用安装脚本

```bash
# 下载并运行安装脚本
curl -fsSL https://raw.githubusercontent.com/anthropics/claude-code/main/install.sh | sh

# 脚本会自动检测系统并安装
# 安装完成后重启终端

# 验证安装
claude --version
```

---

## Linux 安装

Linux 系统推荐使用包管理器或安装脚本。

### Ubuntu/Debian

```bash
# 添加 Anthropic 仓库
curl -fsSL https://packages.anthropic.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/anthropic-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/anthropic-archive-keyring.gpg] https://packages.anthropic.com/apt stable main" | sudo tee /etc/apt/sources.list.d/anthropic.list

# 更新并安装
sudo apt update
sudo apt install claude-code

# 验证安装
claude --version
```

### Fedora/RHEL/CentOS

```bash
# 添加 Anthropic 仓库
sudo tee /etc/yum.repos.d/anthropic.repo <<EOF
[anthropic]
name=Anthropic Repository
baseurl=https://packages.anthropic.com/rpm
enabled=1
gpgcheck=1
gpgkey=https://packages.anthropic.com/gpg
EOF

# 安装
sudo dnf install claude-code
# 或者使用 yum
sudo yum install claude-code

# 验证安装
claude --version
```

### Arch Linux

```bash
# 使用 AUR
yay -S claude-code
# 或者
paru -S claude-code

# 验证安装
claude --version
```

### 通用方法：使用安装脚本

```bash
# 下载并运行安装脚本
curl -fsSL https://raw.githubusercontent.com/anthropics/claude-code/main/install.sh | sh

# 添加到 PATH（如果需要）
echo 'export PATH="$HOME/.claude-code/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# 验证安装
claude --version
```

---

## Windows 安装

Windows 支持在 2026 年初正式推出，现在有多种安装方式。

### 方法一：使用 Windows 安装程序（推荐）

1. 访问 [Claude Code 官网](https://code.claude.com/download)
2. 下载 Windows 安装程序（`.exe` 文件）
3. 双击运行安装程序
4. 按照向导完成安装
5. 安装完成后，打开 PowerShell 或 Windows Terminal

```powershell
# 验证安装
claude --version
```

### 方法二：使用 Scoop

```powershell
# 安装 Scoop（如果还没有）
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
irm get.scoop.sh | iex

# 添加 Anthropic bucket
scoop bucket add anthropic https://github.com/anthropics/scoop-bucket

# 安装 Claude Code
scoop install claude-code

# 验证安装
claude --version
```

### 方法三：使用 npm

```powershell
# 全局安装
npm install -g @anthropics/claude-code

# 验证安装
claude --version
```

### Windows 特别说明

- 推荐使用 **Windows Terminal** 而不是传统的 CMD
- 确保 PowerShell 执行策略允许运行脚本
- 某些功能可能需要管理员权限

---

## 初始配置

安装完成后，需要进行初始配置。

### 配置 API Key

```bash
# 启动配置向导
claude config

# 或者直接设置 API Key
claude config set api-key YOUR_API_KEY_HERE

# 如果使用中转服务（如 ikuncode）
claude config set api-key YOUR_IKUNCODE_API_KEY
claude config set api-base https://api.ikuncode.cc/v1
```

### 配置文件位置

Claude Code 的配置文件位于：

- **macOS/Linux**: `~/.config/claude/config.json`
- **Windows**: `%APPDATA%\claude\config.json`

### 手动编辑配置文件

```json
{
  "api_key": "your-api-key-here",
  "api_base": "https://api.anthropic.com",
  "model": "claude-sonnet-4-5-20250929",
  "max_tokens": 4096,
  "temperature": 0.7
}
```

### 配置多个模型

```bash
# 设置默认模型
claude config set model claude-sonnet-4-5-20250929

# 设置 Opus 模型（用于复杂任务）
claude config set model-opus claude-opus-4-6-20260206

# 设置 Haiku 模型（用于简单任务）
claude config set model-haiku claude-haiku-3-5-20250219
```

---

## IDE 集成

Claude Code 可以与主流 IDE 集成，提供更好的开发体验。

### VS Code 集成

**安装扩展：**

1. 打开 VS Code
2. 进入扩展市场（Ctrl+Shift+X 或 Cmd+Shift+X）
3. 搜索 "Claude Code"
4. 点击安装

**或者使用命令行：**

```bash
code --install-extension anthropic.claude-code
```

**配置：**

在 VS Code 设置中（`settings.json`）添加：

```json
{
  "claude-code.apiKey": "your-api-key",
  "claude-code.model": "claude-sonnet-4-5-20250929",
  "claude-code.autoSave": true,
  "claude-code.enableInlineCompletion": true
}
```

**使用：**

- 按 `Ctrl+Shift+P`（或 `Cmd+Shift+P`）打开命令面板
- 输入 "Claude Code" 查看可用命令
- 或者在编辑器中右键选择 "Ask Claude Code"

### Cursor 集成

Cursor 是基于 VS Code 的 AI 编辑器，可以直接使用 Claude Code。

**配置：**

1. 打开 Cursor 设置
2. 进入 "AI" 部分
3. 选择 "Claude Code" 作为 AI 提供商
4. 输入 API Key

**或者在终端中：**

```bash
# Cursor 可以直接调用 Claude Code CLI
# 在 Cursor 的终端中使用 claude 命令即可
```

### JetBrains IDEs（IntelliJ、PyCharm 等）

**安装插件：**

1. 打开 IDE
2. 进入 Settings/Preferences → Plugins
3. 搜索 "Claude Code"
4. 安装并重启 IDE

**配置：**

1. 进入 Settings → Tools → Claude Code
2. 输入 API Key
3. 选择模型
4. 配置快捷键

---

## MCP 服务器配置

MCP（Model Context Protocol）是 Claude Code 的扩展机制，可以添加各种功能。

### 什么是 MCP

MCP 服务器是独立的进程，为 Claude Code 提供额外的能力，比如：
- 访问数据库
- 调用外部 API
- 读取特定格式的文件
- 集成第三方服务

### 配置 MCP 服务器

在配置文件中添加 MCP 服务器：

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "your-github-token"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:pass@localhost/db"
      }
    }
  }
}
```

### 常用 MCP 服务器

**文件系统访问：**
```bash
npm install -g @modelcontextprotocol/server-filesystem
```

**GitHub 集成：**
```bash
npm install -g @modelcontextprotocol/server-github
```

**数据库访问：**
```bash
npm install -g @modelcontextprotocol/server-postgres
npm install -g @modelcontextprotocol/server-mysql
```

**浏览器自动化：**
```bash
npm install -g @modelcontextprotocol/server-puppeteer
```

---

## Hooks 配置

Hooks 允许你在 Claude Code 执行特定操作时运行自定义脚本。

### 配置 Hooks

在配置文件中添加：

```json
{
  "hooks": {
    "pre-commit": "npm run lint && npm test",
    "post-commit": "echo 'Commit completed!'",
    "pre-push": "npm run build",
    "on-error": "notify-send 'Claude Code Error' '$ERROR_MESSAGE'"
  }
}
```

### 可用的 Hook 类型

- `pre-commit`: 提交代码前执行
- `post-commit`: 提交代码后执行
- `pre-push`: 推送代码前执行
- `post-push`: 推送代码后执行
- `on-error`: 发生错误时执行
- `on-success`: 任务成功时执行

### Hook 脚本示例

**自动格式化代码：**
```json
{
  "hooks": {
    "pre-commit": "prettier --write . && git add -A"
  }
}
```

**运行测试：**
```json
{
  "hooks": {
    "pre-commit": "npm test || exit 1"
  }
}
```

**通知：**
```json
{
  "hooks": {
    "on-success": "osascript -e 'display notification \"Task completed!\" with title \"Claude Code\"'",
    "on-error": "osascript -e 'display notification \"Error occurred!\" with title \"Claude Code\"'"
  }
}
```

---

## 高级配置

### 配置代理

如果需要通过代理访问 API：

```bash
# 设置 HTTP 代理
claude config set http-proxy http://proxy.example.com:8080

# 设置 HTTPS 代理
claude config set https-proxy https://proxy.example.com:8080

# 或者使用环境变量
export HTTP_PROXY=http://proxy.example.com:8080
export HTTPS_PROXY=https://proxy.example.com:8080
```

### 配置超时时间

```bash
# 设置请求超时（秒）
claude config set timeout 120

# 设置流式响应超时
claude config set stream-timeout 300
```

### 配置日志级别

```bash
# 设置日志级别：debug, info, warn, error
claude config set log-level debug

# 查看日志文件位置
claude config get log-file
```

### 配置自定义指令

创建 `.claude.md` 文件在项目根目录：

```markdown
# Project Context

This is a React + TypeScript project using Vite.

## Code Style
- Use functional components
- Prefer hooks over class components
- Use TypeScript strict mode
- Follow Airbnb style guide

## Testing
- Use Vitest for unit tests
- Use Testing Library for component tests
- Aim for 80%+ coverage

## Important Files
- `src/components/` - React components
- `src/hooks/` - Custom hooks
- `src/utils/` - Utility functions
```

---

## 验证配置

完成配置后，运行以下命令验证：

```bash
# 检查版本
claude --version

# 检查配置
claude config list

# 测试 API 连接
claude auth status

# 运行简单测试
claude chat "Hello, Claude!"
```

如果一切正常，你应该能看到 Claude 的回复。

---

## 常见问题

### API Key 无效

```bash
# 检查 API Key 是否正确
claude config get api-key

# 重新设置
claude config set api-key YOUR_NEW_API_KEY

# 测试连接
claude auth status
```

### 命令找不到

```bash
# macOS/Linux: 检查 PATH
echo $PATH

# 添加到 PATH
export PATH="$HOME/.claude-code/bin:$PATH"

# Windows: 检查环境变量
echo $env:PATH
```

### 权限问题

```bash
# macOS/Linux: 修复权限
chmod +x ~/.claude-code/bin/claude

# Windows: 以管理员身份运行
```

### 网络连接问题

```bash
# 测试网络连接
curl https://api.anthropic.com/v1/messages

# 如果使用中转服务
curl https://api.ikuncode.cc/v1/messages
```

---

## 下一步

配置完成后，你可以：

1. 学习[基础使用](basic-usage)
2. 探索[高级功能](advanced-features)
3. 查看[最佳实践](best-practices)

---

[返回目录](index) | [上一章：简介](introduction) | [下一章：基础使用](basic-usage)

---

## 参考资料

- [Claude Code 官方文档 - 快速开始](https://code.claude.com/docs/en/quickstart)
- [Claude Code 官方文档 - 设置](https://code.claude.com/docs/en/settings)
- [Windows 11 安装指南](https://interworks.com/blog/2026/01/27/how-to-install-claude-code-on-windows-11/)
- [VS Code 集成指南](https://code.claude.com/docs/en/vs-code)
- [MCP 服务器配置](https://medium.com/@the.gigi/claude-code-deep-dive-mcp-unleashed-0c7692f9c2c2)
- [Claude Code CLI 速查表](https://shipyard.build/blog/claude-code-cheat-sheet/)
- [多提供商配置指南](https://gist.github.com/spideynolove/13785891385ed6916619ebb991b490b9)
