---
layout: default
title: Codex 简介
---

# Codex 简介

Codex 是 OpenAI 推出的专业代码生成工具，以其精准的代码生成能力和对复杂编程语言的深度理解而闻名。与 Claude Code 相比，Codex 更注重代码的准确性和质量，特别是在处理大型项目和底层语言时表现出色。

---

## 多平台支持

Codex 对各个操作系统都非常友好，可以通过多种方式使用。

### VS Code 插件

最常用的方式是直接在 VS Code 中安装 Codex 插件。这种方式跨平台支持良好，无论是 Windows、macOS 还是 Linux，都能获得一致的体验。插件集成在编辑器中，可以实时提供代码建议、自动补全、代码解释等功能。

```bash
# 在 VS Code 中安装
# 1. 打开扩展市场（Ctrl+Shift+X 或 Cmd+Shift+X）
# 2. 搜索 "OpenAI Codex"
# 3. 点击安装
```

### Codex App（macOS）

目前 Codex App 只在 macOS 上提供，这是一个独立的桌面应用程序。虽然功能上与 VS Code 插件类似，但 Codex App 在某些场景下似乎更省钱——不过如果你使用的是包月套餐，这个优势就不太明显了。

Codex App 提供了更原生的 macOS 体验，界面更简洁，启动更快。如果你是 Mac 用户且经常需要快速查询代码问题，Codex App 是个不错的选择。

---

## 模型选择

Codex 提供了多种模型供选择，主要分为两类：带 `-codex` 后缀的和不带后缀的。

### 带 -codex 后缀的模型

这类模型专门针对代码生成进行了优化，比如 `gpt-5.3-codex`。它们在代码补全、函数生成、代码重构等任务上表现出色，响应速度也更快。理论上，这些模型应该是写代码的最佳选择。

### 不带 -codex 后缀的模型

这类模型是通用模型，比如 `gpt-5.2`。它们的综合能力更强，不仅能写代码，还能进行复杂的推理、分析、规划。虽然不是专门为代码优化的，但在实际使用中，很多开发者发现这些模型反而更强大。

### 实际体验

根据实际使用体验，虽然 OpenAI 在 2026 年初推出了 `gpt-5.3-codex`，但很多用户反馈 `gpt-5.2 xhigh` 的表现更好。这可能是因为通用模型在理解复杂需求、处理边界情况、进行架构设计时更有优势。

当然，这也取决于具体任务。如果是简单的代码补全或函数生成，`-codex` 后缀的模型可能更快更准。但如果是复杂的重构、调试或架构设计，通用模型可能更胜一筹。

---

## 思考模式

Codex 最强大的特性之一是它的多种思考模式。不同的模式在速度和质量之间做了不同的权衡。

### 四种思考模式

1. **Low（低）**：最快的模式，适合简单的代码补全和快速问答
2. **Medium（中）**：平衡速度和质量，适合日常开发
3. **High（高）**：更深入的思考，适合复杂问题
4. **Extra High（xhigh）**：最强大的模式，也是最慢的

### Extra High（xhigh）模式

这是 Codex 的"核武器"级别模式。当你使用 xhigh 模式时，模型会进行非常深入的思考和分析，运行一次可能需要等待较长时间，但结果往往非常准确。

**xhigh 模式的特点：**
- **极高的准确性**：几乎不会出现低级错误
- **深度理解**：能够理解复杂的代码逻辑和架构
- **全面考虑**：会考虑各种边界情况和潜在问题
- **速度较慢**：可能需要等待 30 秒到几分钟

**何时使用 xhigh：**
- 修复关键 bug
- 重构核心代码
- 设计复杂算法
- 处理底层系统代码
- 学习和理解复杂项目

**何时不用 xhigh：**
- 开发小功能或小应用（这种场景 Claude 更合适）
- 快速原型开发
- 简单的代码补全
- 时间紧迫的任务

根据实际体验，`gpt-5.2 xhigh` 在处理复杂问题时的表现非常出色，虽然慢，但结果往往一次就对，反而节省了反复修改的时间。

---

## 适用场景

Codex 和 Claude Code 各有所长，选择哪个取决于你的具体需求。

### Codex 的优势场景

**大型项目维护**

Codex 特别擅长在大型项目的基础上进行调整。它能够理解复杂的代码库结构，准确定位需要修改的地方，并确保修改不会破坏现有功能。如果你的项目已经有几万行甚至几十万行代码，Codex 是更好的选择。

**Bug 修复**

在修复 bug 时，Codex 的准确性优势尤为明显。它能够仔细分析错误原因，找出根本问题，并提供精准的修复方案。特别是使用 xhigh 模式时，修复的成功率非常高。

**代码学习**

如果你想深入理解某个复杂的代码库或算法，Codex 是很好的老师。它能够详细解释代码逻辑，指出关键设计决策，帮助你快速掌握项目的核心思想。

**底层语言开发**

对于 C++、Rust 这类有难度的底层语言，Codex 的表现明显优于 Claude。它对这些语言的语法、内存管理、并发模型等有更深入的理解，生成的代码更符合最佳实践。

**小众语言支持**

Codex 对小众语言的支持也更好。比如 Lean4（定理证明语言）、Haskell（函数式编程）、OCaml 等，Codex 都能提供相对准确的代码生成和建议。这些语言的训练数据较少，但 Codex 仍然能够理解它们的核心概念。

### Claude Code 更适合的场景

相比之下，Claude Code 更适合：
- 快速开发小功能或小应用
- 前端开发（React、Vue 等）
- Python 脚本和数据分析
- 需要频繁迭代的原型开发
- 多文件协同修改

---

## 定价模式

Codex 的定价模式相对友好，特别是对于频繁使用的开发者。

### 包月套餐

Codex 支持包月订阅，这是它相比 Claude 的一个重要优势。Claude 按 token 计费，如果频繁使用，成本会持续累积。而 Codex 的包月套餐让你可以放心使用，不用担心费用失控。

**GPT Plus 会员：**
- 价格：$20/月
- 包含 Codex 访问权限
- 额度较高，量大管饱
- 适合个人开发者

**中转服务：**
- 价格：一个月几十元人民币
- 基本用不完
- 推荐使用 rightcode 等服务
- 性价比更高

### 与 Claude 的成本对比

如果你是重度用户，Codex 的包月模式会比 Claude 的按量计费更经济。Claude 虽然功能强大，但在处理大型项目或频繁使用时，token 消耗会非常快，成本可能是 Codex 的数倍。

当然，如果你只是偶尔使用，或者主要做前端和 Python 开发，Claude 可能更合适。但如果你每天都要写大量代码，特别是 C++、Rust 这类底层语言，Codex 的包月套餐会更划算。

---

## Codex vs Claude Code

简单总结一下两者的区别：

| 特性 | Codex | Claude Code |
|------|-------|-------------|
| **准确性** | 更高，特别是 xhigh 模式 | 较快但可能有小 bug |
| **速度** | xhigh 模式较慢，其他模式快 | 整体较快 |
| **底层语言** | C++、Rust 表现更好 | 相对较弱 |
| **前端/Python** | 表现良好 | 表现优秀 |
| **小众语言** | 支持更好（如 Lean4） | 支持一般 |
| **大型项目** | 更擅长维护和调试 | 更擅长快速开发 |
| **定价** | 包月，成本可控 | 按量计费，重度使用成本高 |
| **使用场景** | 大型项目、底层开发、学习 | 小应用、前端、快速原型 |

---

## 开始使用

要开始使用 Codex，你需要：

1. 选择使用方式（VS Code 插件或 Codex App）
2. 配置 API Key 或订阅 GPT Plus
3. 根据任务选择合适的模型和思考模式
4. 在项目中开始使用

具体的安装和配置步骤，我们会在[安装与配置](installation)章节详细介绍。

---

[返回目录](index) | [下一章：安装与配置](installation)

---

## 参考资料

- [GPT-5.3-Codex 官方发布](https://openai.com/index/introducing-gpt-5-3-codex/)
- [GPT-5.2 和 Codex 完整指南 2026](https://www.digitalapplied.com/blog/gpt-5-2-codex-openai-model-guide-2026)
- [GPT-5.2 (xhigh) vs GPT-5 Codex (high) 对比](https://artificialanalysis.ai/models/comparisons/gpt-5-2-vs-gpt-5-codex)
- [Codex 最佳实践](https://community.openai.com/t/best-practices-for-using-codex/1373143)
- [Claude Code vs OpenAI Codex 对比](https://northflank.com/blog/claude-code-vs-openai-codex)
- [OpenAI Codex App 完整指南](https://almcorp.com/blog/openai-codex-app-macos-guide-features-pricing-security/)
- [VS Code 多代理开发](https://code.visualstudio.com/blogs/2026/02/05/multi-agent-development)
- [GPT-5.2 深度评测](https://www.turingcollege.com/blog/gpt-5-2-review)
