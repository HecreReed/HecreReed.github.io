---
layout: default
title: API 使用
---

# Codex API 使用

与 Claude 按 token 计费不同，Codex 的最大优势之一就是包月模式。这意味着你基本不需要担心 token 消耗，可以放心使用。

---

## 包月渠道

Codex 有多种包月渠道可选，价格从几美元到几十美元不等，都能满足日常开发需求。

### GPT Plus 会员

最直接的方式是订阅 GPT Plus 会员：

- **价格**：$20/月
- **包含内容**：
  - ChatGPT Plus 访问权限
  - Codex API 访问权限
  - GPT-5.2、GPT-5.3-Codex 等所有模型
  - 较高的使用额度
- **适合人群**：个人开发者、需要同时使用 ChatGPT 和 Codex 的用户

这个价格对于重度使用来说非常划算。如果你每天都要写代码，$20/月 基本可以无限使用，不用担心费用问题。

### 中转服务

如果觉得官方价格贵，可以使用中转服务：

- **价格**：一个月几十元人民币（约 $5-10）
- **推荐服务**：rightcode、ikuncode 等
- **优势**：
  - 价格更便宜
  - 国内访问更稳定
  - 额度基本用不完
  - 支持支付宝、微信支付

中转服务的额度对于个人开发者来说完全够用。即使你每天写大量代码，一个月几十块也基本用不完。

### GPT Team（最便宜）

如果你想要最低成本，可以考虑 GPT Team：

- **价格**：约 $1/月（通过拼团或特殊渠道）
- **方式**：多人共享一个 Team 账号
- **注意事项**：
  - 需要找到可靠的拼团渠道
  - 可能有使用限制
  - 稳定性取决于团队管理

虽然价格极低，但对于日常开发来说完全够用。一个月一美元的成本，基本可以忽略不计。

---

## 不用担心 Token 消耗

这是 Codex 相比 Claude 的最大优势。

### Claude 的成本压力

使用 Claude 时，你需要时刻关注 token 消耗：
- 每次对话都在烧钱
- 处理大型项目时成本飞涨
- 使用 Opus 模型时更是昂贵
- 需要精打细算，避免浪费

这种按量计费的模式让人用起来有心理负担，总是担心费用超支。

### Codex 的自由使用

而 Codex 的包月模式让你可以：
- **随意使用**：不用担心每次调用的成本
- **反复调试**：可以多次尝试，直到满意为止
- **处理大项目**：不用担心大型代码库的 token 消耗
- **使用 xhigh 模式**：虽然慢但准确，不用担心费用
- **学习和探索**：可以用来学习代码、理解项目，不用心疼钱

这种"包月无限用"的模式，让 Codex 成为日常开发的理想选择。

---

## API 配置与管理

对于需要使用多个 API 提供商或频繁切换配置的用户，推荐使用 **cc-switch** 工具。

### 什么是 cc-switch

cc-switch 是一个跨平台的 All-in-One 配置管理工具，专门为 Claude Code、Codex、Gemini 等 AI CLI 工具设计。它可以让你轻松管理多个 API Key 和中转服务配置，一键切换不同的提供商。

**主要功能：**
- 管理多个 API 配置（官方 API、中转服务等）
- 一键切换不同的提供商
- 支持 Claude、OpenAI Codex、Gemini 等多种 AI 工具
- 跨平台支持（Windows、macOS、Linux）
- 提供桌面版和 CLI 版本

### 安装 cc-switch

**桌面版（推荐）：**

访问 [cc-switch GitHub](https://github.com/farion1231/cc-switch) 下载对应平台的安装包。

**CLI 版本：**

```bash
# 使用 npm 安装
npm install -g cc-switch-cli

# 或者使用 yarn
yarn global add cc-switch-cli
```

### 配置 API 提供商

使用 cc-switch 配置 Codex API 非常简单，只需 4 步：

**1. 启动 cc-switch**

```bash
# 桌面版：直接打开应用
# CLI 版：运行命令
cc-switch
```

**2. 添加提供商**

在 cc-switch 中添加你的 API 配置：

```bash
# 添加 OpenAI 官方 API
cc-switch add openai-official \
  --api-key "your-openai-api-key" \
  --base-url "https://api.openai.com/v1"

# 添加中转服务（如 rightcode）
cc-switch add rightcode \
  --api-key "your-rightcode-api-key" \
  --base-url "https://api.rightcode.cn/v1"

# 添加另一个中转服务（如 ikuncode）
cc-switch add ikuncode \
  --api-key "your-ikuncode-api-key" \
  --base-url "https://api.ikuncode.cc/v1"
```

**3. 切换提供商**

需要切换时，只需一条命令：

```bash
# 切换到 rightcode
cc-switch use rightcode

# 切换到官方 API
cc-switch use openai-official

# 查看当前使用的提供商
cc-switch current
```

**4. 查看所有配置**

```bash
# 列出所有配置的提供商
cc-switch list

# 输出示例：
# ✓ rightcode (active)
#   openai-official
#   ikuncode
```

### 使用场景

**场景一：官方 API 和中转服务切换**

```bash
# 平时使用便宜的中转服务
cc-switch use rightcode

# 中转服务不稳定时，切换到官方 API
cc-switch use openai-official
```

**场景二：多个中转服务备份**

```bash
# 配置多个中转服务作为备份
cc-switch add rightcode-1 --api-key "key1" --base-url "url1"
cc-switch add rightcode-2 --api-key "key2" --base-url "url2"

# 一个服务出问题时，立即切换到另一个
cc-switch use rightcode-2
```

**场景三：不同项目使用不同配置**

```bash
# 个人项目使用中转服务
cd ~/personal-project
cc-switch use rightcode

# 公司项目使用官方 API
cd ~/work-project
cc-switch use openai-official
```

### 桌面版界面

cc-switch 的桌面版提供了图形化界面，更加直观：

- **配置管理**：可视化添加、编辑、删除配置
- **一键切换**：点击即可切换提供商
- **状态显示**：实时显示当前使用的配置
- **测试连接**：可以测试 API 是否可用

### 高级功能

**配置模板：**

cc-switch 支持配置模板，可以快速添加常用的中转服务：

```bash
# 使用模板添加 rightcode
cc-switch add-from-template rightcode

# 使用模板添加 ikuncode
cc-switch add-from-template ikuncode
```

**环境变量导出：**

cc-switch 可以将当前配置导出为环境变量：

```bash
# 导出当前配置
cc-switch export

# 输出：
# export OPENAI_API_KEY="your-key"
# export OPENAI_BASE_URL="your-base-url"
```

**配置备份：**

```bash
# 备份所有配置
cc-switch backup config-backup.json

# 恢复配置
cc-switch restore config-backup.json
```

### 为什么推荐 cc-switch

1. **简化管理**：不用手动修改配置文件或环境变量
2. **快速切换**：一条命令即可切换提供商
3. **多工具支持**：同时管理 Claude、Codex、Gemini 的配置
4. **避免错误**：图形化界面减少配置错误
5. **配置同步**：可以在多台设备间同步配置

---

## 使用建议

### 1. 选择合适的渠道

- **重度使用**：GPT Plus 会员，$20/月 最稳定
- **日常开发**：中转服务，几十元/月 性价比高
- **预算有限**：GPT Team，$1/月 够用

### 2. 不用节省 Token

既然是包月，就不要像用 Claude 那样精打细算：
- 遇到问题多问几次
- 不满意就重新生成
- 使用 xhigh 模式不用心疼
- 可以用来学习和探索

### 3. 合理使用思考模式

- **日常开发**：使用 medium 或 high 模式
- **关键任务**：使用 xhigh 模式，虽然慢但准
- **简单补全**：使用 low 模式，快速响应

### 4. 与 Claude 配合使用

虽然 Codex 包月很划算，但不同工具有不同优势：
- **Codex**：大型项目、底层语言、精准修复
- **Claude**：快速开发、前端、Python、数据分析

根据任务选择合适的工具，可以达到最佳效果。

---

## 成本对比

让我们算一笔账，看看 Codex 的包月模式有多划算。

### Claude 的成本（按量计费）

假设你是一个活跃的开发者：
- 每天使用 Claude Sonnet 处理代码任务
- 平均每天消耗 100K tokens（输入+输出）
- 一个月 30 天

**成本计算：**
- Sonnet 输入：$3/1M tokens
- Sonnet 输出：$15/1M tokens
- 假设输入输出各占一半：50K + 50K
- 每天成本：(50K × $3 + 50K × $15) / 1M = $0.9
- 每月成本：$0.9 × 30 = **$27**

如果使用 Opus，成本会更高：
- Opus 输入：$15/1M tokens
- Opus 输出：$75/1M tokens
- 每月成本：约 **$135**

### Codex 的成本（包月）

- GPT Plus：**$20/月**，无限使用
- 中转服务：**$5-10/月**，基本用不完
- GPT Team：**$1/月**，够用

**结论：**
- 如果你是重度用户，Codex 的包月模式能节省 50%-90% 的成本
- 而且不用担心费用超支，可以放心使用
- 特别是使用 xhigh 模式时，不用心疼 token

---

## 常见问题

### Q: 包月真的够用吗？

A: 对于个人开发者来说，完全够用。即使你每天写大量代码，GPT Plus 或中转服务的额度都很难用完。

### Q: 中转服务靠谱吗？

A: 选择知名的中转服务（如 rightcode）通常很稳定。建议先试用一个月，确认稳定后再长期使用。

### Q: GPT Team 怎么找？

A: 可以在相关社区、论坛寻找拼团信息。注意选择可靠的组织者，避免被骗。

### Q: 包月和按量计费哪个更好？

A: 如果你是重度用户（每天都用），包月更划算。如果只是偶尔使用，按量计费可能更合适。

### Q: 可以同时订阅多个服务吗？

A: 可以。比如同时订阅 GPT Plus（用 Codex）和 Claude 中转服务，根据任务选择合适的工具。

---

## 下一步

了解了 API 使用和定价后，你可以：

1. 学习[基础使用](basic-usage)，开始实际使用 Codex
2. 探索[高级功能](advanced-features)，发挥 Codex 的最大潜力
3. 查看[最佳实践](best-practices)，提高使用效率

---

[返回目录](index) | [上一章：安装与配置](installation) | [下一章：基础使用](basic-usage)

---

## 参考资料

- [cc-switch 官方 GitHub](https://github.com/farion1231/cc-switch)
- [cc-switch CLI 版本](https://github.com/thomas-jack/cc-switch-cli)
- [cc-switch 5 分钟入门指南](https://help.apiyi.com/en/cc-switch-beginner-guide-en.html)
- [cc-switch 配置教程（以 APIYI 为例）](https://blog.wentuo.ai/en/cc-switch-add-provider-tutorial-en.html)
- [CCS 文档](https://docs.claudekit.cc/docs/tools/ccs)
- [CCS 多账号切换工具](https://ccs.kaitran.ca/)
- [如何使用 OpenAI Codex 配置自己的 API Key](https://zeabur.com/blogs/use-codex-with-ai-hub)

