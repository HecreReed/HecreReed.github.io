---
layout: default
title: 准备工作
---

# 准备工作

在开始使用 AI Agent 工具之前，需要完成一些基础配置。

## 目录

- [账号注册](#账号注册)
- [API Key 获取](#api-key-获取)
- [开发环境配置](#开发环境配置)
- [费用说明](#费用说明)
- [安全注意事项](#安全注意事项)

---

## 账号注册与推荐方案

### Claude (Anthropic)

**官方渠道：**
1. 访问 [claude.ai](https://claude.ai)
2. 使用邮箱或 Google 账号注册
3. 验证邮箱
4. 获取 API Key：访问 [console.anthropic.com](https://console.anthropic.com)

**实用建议：**

Claude 官方 API 在中国区使用存在一些问题：容易遇到账号封禁，且价格相对较高。更推荐使用中转服务。

**推荐方案：ikuncode 中转站**
- 使用 0.4x 倍率的反代服务
- 价格更实惠，稳定性好
- 访问：[ikuncode.com](https://ikuncode.com)
- 注册后获取 API Key，使用方式与官方完全相同

### OpenAI (Codex/GPT)

**方案一：GPT Plus 会员（推荐）**

如果你已经订阅了 ChatGPT Plus 会员（$20/月），可以直接使用 Codex：
- 额度较高，量大管饱
- 直接在 ChatGPT 界面使用
- 或通过 API 调用（需要单独申请 API 访问）

**方案二：rightcode 中转站**

如果没有 Plus 会员，推荐使用 rightcode 中转站：
- 订阅价格：一个月几十块人民币
- 额度基本用不完
- 访问：[rightcode.cn](https://rightcode.cn)
- 提供稳定的 API 访问

**官方渠道：**
1. 访问 [platform.openai.com](https://platform.openai.com)
2. 注册账号
3. 绑定支付方式（需要国际信用卡）
4. 在 API Keys 页面创建密钥

### Google (Gemini)

**推荐方案：淘宝购买 Gemini Pro 会员**

Gemini Pro 会员可以考虑在淘宝购买：
- 搜索"Gemini Pro 会员"或"Google One AI Premium"
- 价格相对实惠
- 包含 Gemini Advanced 访问权限

**官方渠道：**
1. 访问 [ai.google.dev](https://ai.google.dev)
2. 使用 Google 账号登录
3. 在 Google AI Studio 中获取 API Key
4. 免费额度较高，适合测试

### xAI (Grok)

**推荐方案：使用免费版**

Grok 的免费版本已经足够日常使用，无需付费。

**如果需要付费版本：**
- 将 VPN 节点切换到印度
- 订阅价格约 40 多元人民币/月（印度区价格）
- 使用 Visa 卡支付
- 比美国区便宜很多

**官方渠道：**
1. 需要 X (Twitter) 账号
2. 访问 [x.ai](https://x.ai) 或在 X 平台使用
3. 免费版可直接使用
4. Premium 订阅获得更多功能

---

## API Key 获取

### 什么是 API Key

API Key 是用于身份验证的密钥，类似于密码。每次调用 API 时都需要提供。

### 中转站 API Key 获取

**ikuncode（Claude）:**
```bash
# 1. 访问 https://ikuncode.com
# 2. 注册账号并充值
# 3. 在控制台获取 API Key
# 4. 使用时将 API 端点改为 ikuncode 提供的地址
```

**rightcode（OpenAI）:**
```bash
# 1. 访问 https://rightcode.cn
# 2. 注册并订阅套餐
# 3. 获取 API Key
# 4. 配置 API 端点为 rightcode 提供的地址
```

### 官方 API Key 获取

**Claude:**
```bash
# 访问控制台
https://console.anthropic.com/settings/keys

# 点击 "Create Key"
# 复制并保存密钥（只显示一次）
```

**OpenAI:**
```bash
# 访问 API Keys 页面
https://platform.openai.com/api-keys

# 点击 "Create new secret key"
# 命名并保存密钥
```

**Gemini:**
```bash
# 访问 Google AI Studio
https://aistudio.google.com/app/apikey

# 点击 "Get API key"
# 选择项目或创建新项目
```

### 密钥管理

**环境变量方式（推荐）:**

```bash
# macOS/Linux
export ANTHROPIC_API_KEY="your-key-here"
export OPENAI_API_KEY="your-key-here"
export GOOGLE_API_KEY="your-key-here"

# 添加到 ~/.bashrc 或 ~/.zshrc 永久保存
echo 'export ANTHROPIC_API_KEY="your-key-here"' >> ~/.zshrc
```

**配置文件方式:**

```bash
# Claude Code
claude config set api-key your-key-here

# 或创建配置文件 ~/.config/claude/config.json
{
  "api_key": "your-key-here"
}
```

---

## 开发环境配置

### 必备工具

**1. 终端/命令行**
- macOS: Terminal 或 iTerm2
- Windows: PowerShell 或 Windows Terminal
- Linux: 系统自带终端

**2. 代码编辑器**
- VS Code（推荐）
- Cursor
- Sublime Text
- Vim/Neovim

**3. Git**
```bash
# 检查是否已安装
git --version

# macOS 安装
brew install git

# Ubuntu/Debian 安装
sudo apt install git

# Windows 安装
# 下载 https://git-scm.com/download/win
```

**4. Node.js（可选，用于某些工具）**
```bash
# 检查版本
node --version
npm --version

# 使用 nvm 安装
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install --lts
```

**5. Python（可选，用于某些工具）**
```bash
# 检查版本
python3 --version
pip3 --version

# macOS 安装
brew install python3

# Ubuntu/Debian 安装
sudo apt install python3 python3-pip
```

### Claude Code 安装

```bash
# macOS/Linux
curl -fsSL https://raw.githubusercontent.com/anthropics/claude-code/main/install.sh | sh

# 或使用 npm
npm install -g @anthropics/claude-code

# 验证安装
claude --version

# 配置 API Key
claude config set api-key your-key-here
```

### GitHub Copilot 安装

```bash
# VS Code 中安装
# 1. 打开 VS Code
# 2. 进入扩展市场
# 3. 搜索 "GitHub Copilot"
# 4. 点击安装
# 5. 登录 GitHub 账号
```

### Gemini SDK 安装

```bash
# Python
pip install google-generativeai

# Node.js
npm install @google/generative-ai
```

---

## 费用说明

### 推荐方案费用对比

| 服务 | 方案 | 费用 | 说明 |
|------|------|------|------|
| Claude | ikuncode 中转 | 按量计费，0.4x 倍率 | 比官方便宜，稳定可靠 |
| Codex | GPT Plus 会员 | $20/月 | 额度高，量大管饱 |
| Codex | rightcode 中转 | 几十元/月 | 订阅制，基本用不完 |
| Gemini | 淘宝 Pro 会员 | 约 100-150 元/月 | 包含 Advanced 功能 |
| Grok | 免费版 | 免费 | 日常使用足够 |
| Grok | 印度区付费 | 约 40 元/月 | 比美国区便宜 |

### 官方定价参考

**Claude 官方：**

| 模型 | 输入价格 | 输出价格 | 上下文窗口 |
|------|---------|---------|-----------|
| Claude 3.5 Sonnet | $3/1M tokens | $15/1M tokens | 200K |
| Claude 3 Opus | $15/1M tokens | $75/1M tokens | 200K |
| Claude 3 Haiku | $0.25/1M tokens | $1.25/1M tokens | 200K |

**OpenAI 官方：**

| 模型 | 输入价格 | 输出价格 | 上下文窗口 |
|------|---------|---------|-----------|
| GPT-4 Turbo | $10/1M tokens | $30/1M tokens | 128K |
| GPT-4 | $30/1M tokens | $60/1M tokens | 8K |
| GPT-3.5 Turbo | $0.5/1M tokens | $1.5/1M tokens | 16K |

**Gemini 官方：**

| 模型 | 免费额度 | 付费价格 | 上下文窗口 |
|------|---------|---------|-----------|
| Gemini 1.5 Pro | 50 请求/天 | $7/1M tokens | 1M |
| Gemini 1.5 Flash | 1500 请求/天 | $0.35/1M tokens | 1M |

### 省钱建议

1. **优先使用免费额度**：Gemini 的免费额度很高，适合日常使用
2. **选择中转服务**：比官方便宜，且更稳定
3. **合理选择模型**：不是所有任务都需要最强的模型
4. **使用会员套餐**：如果使用频繁，订阅制更划算

---

## 安全注意事项

### API Key 安全

**❌ 不要做：**
- 不要将 API Key 提交到 Git 仓库
- 不要在代码中硬编码 API Key
- 不要分享 API Key 给他人
- 不要在公开场合展示 API Key

**✅ 应该做：**
- 使用环境变量存储 API Key
- 使用 `.gitignore` 忽略配置文件
- 定期轮换 API Key
- 设置使用限额和预警

### .gitignore 配置

```bash
# 创建 .gitignore 文件
cat > .gitignore << EOF
# API Keys 和配置
.env
.env.local
config.json
*.key

# 系统文件
.DS_Store
Thumbs.db

# 依赖
node_modules/
venv/
__pycache__/
EOF
```

### 环境变量文件

```bash
# 创建 .env 文件（不要提交到 Git）
ANTHROPIC_API_KEY=your-key-here
OPENAI_API_KEY=your-key-here
GOOGLE_API_KEY=your-key-here

# 在代码中使用
# Python
import os
api_key = os.getenv('ANTHROPIC_API_KEY')

# Node.js
require('dotenv').config();
const apiKey = process.env.ANTHROPIC_API_KEY;
```

### 使用限额设置

在各平台的控制台中设置：
- 每月最大消费额度
- 单次请求限制
- 速率限制
- 预警通知

---

## 验证配置

完成配置后，运行以下命令验证：

```bash
# 检查 Claude Code
claude --version
claude auth status

# 检查环境变量
echo $ANTHROPIC_API_KEY
echo $OPENAI_API_KEY
echo $GOOGLE_API_KEY

# 测试 API 连接
# Claude
claude chat "Hello"

# OpenAI (使用 curl)
curl https://api.openai.com/v1/models \
  -H "Authorization: Bearer $OPENAI_API_KEY"

# Gemini (使用 Python)
python3 << EOF
import google.generativeai as genai
import os
genai.configure(api_key=os.getenv('GOOGLE_API_KEY'))
model = genai.GenerativeModel('gemini-pro')
response = model.generate_content('Hello')
print(response.text)
EOF
```

---

## 下一步

配置完成后，可以：

1. 学习[基础概念](basic-concepts)
2. 开始使用 [Claude Code](../02-claude-code/)
3. 查看[完整大纲](../outline)

---

[返回目录](index) | [上一章：什么是 AI Agent](what-is-ai-agent) | [下一章：基础概念](basic-concepts)
