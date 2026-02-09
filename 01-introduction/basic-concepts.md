---
layout: default
title: 基础概念
---

# 基础概念

掌握这些基础概念，帮助你更好地使用 AI Agent 工具。

## 目录

- [Prompt Engineering](#prompt-engineering)
- [Token 与上下文窗口](#token-与上下文窗口)
- [温度参数](#温度参数)
- [流式输出](#流式输出)
- [常见术语表](#常见术语表)

---

## Prompt Engineering

### 什么是 Prompt

Prompt（提示词）是你发送给 AI 的指令或问题。好的 Prompt 能够获得更好的结果。

### 基本原则

**1. 清晰明确**
```
❌ 不好：写个函数
✅ 好：用 Python 写一个函数，接收一个整数列表，返回列表中的最大值
```

**2. 提供上下文**
```
❌ 不好：修复这个 bug
✅ 好：这是一个 React 组件，点击按钮时状态没有更新。请帮我找出问题并修复。
```

**3. 分步骤说明**
```
✅ 好：
1. 创建一个 Express 服务器
2. 添加一个 /api/users 路由
3. 从数据库读取用户列表
4. 返回 JSON 格式的数据
```

**4. 给出示例**
```
✅ 好：
将以下数据转换为 JSON 格式：
输入：name=John, age=30, city=NYC
期望输出：{"name": "John", "age": 30, "city": "NYC"}
```

### Prompt 模板

**代码生成：**
```
用 [语言] 写一个 [功能描述]
要求：
- [要求1]
- [要求2]
- [要求3]
```

**代码解释：**
```
解释以下代码的功能：
[代码]

请说明：
1. 主要功能
2. 关键步骤
3. 可能的问题
```

**Bug 修复：**
```
以下代码有问题：
[代码]

错误信息：
[错误]

请帮我：
1. 找出问题原因
2. 提供修复方案
3. 解释为什么会出现这个问题
```

---

## Token 与上下文窗口

### 什么是 Token

Token 是 AI 模型处理文本的基本单位。可以理解为"词块"。

**示例：**
```
文本："Hello, world!"
Tokens：["Hello", ",", " world", "!"]
约 4 个 tokens
```

**估算规则：**
- 英文：1 个单词 ≈ 1-2 个 tokens
- 中文：1 个汉字 ≈ 1.5-2 个 tokens
- 代码：1 行 ≈ 5-10 个 tokens

### 上下文窗口

上下文窗口是 AI 一次能"记住"的最大 token 数量。

| 模型 | 上下文窗口 | 约等于 |
|------|-----------|--------|
| Claude 3.5 Sonnet | 200K tokens | ~150K 英文单词 |
| GPT-4 Turbo | 128K tokens | ~96K 英文单词 |
| Gemini 1.5 Pro | 1M tokens | ~750K 英文单词 |

### 为什么重要

- **费用计算**：按 token 数量计费
- **内容限制**：超过窗口大小会被截断
- **性能影响**：更多 token = 更慢的响应

### Token 优化技巧

**1. 精简 Prompt**
```
❌ 不好（冗长）：
请你帮我写一个函数，这个函数的功能是...（200 字）

✅ 好（简洁）：
写一个函数：输入整数数组，返回最大值
```

**2. 移除无用内容**
```python
# ❌ 不要包含大量注释
# 这是一个函数
# 它做了很多事情
# ...（100 行注释）

# ✅ 只保留关键信息
def process_data(data):
    # 处理数据并返回结果
    return result
```

**3. 使用引用而非复制**
```
❌ 不好：把整个文件内容粘贴进来（5000 行）
✅ 好：只粘贴相关的函数（50 行）
```

---

## 温度参数

### 什么是温度

温度（Temperature）控制 AI 输出的随机性和创造性。

**取值范围：** 0.0 - 2.0

### 不同温度的效果

| 温度 | 特点 | 适用场景 |
|------|------|---------|
| 0.0 - 0.3 | 确定性强，输出稳定 | 代码生成、数据分析 |
| 0.4 - 0.7 | 平衡创造性和准确性 | 通用对话、文档编写 |
| 0.8 - 1.0 | 更有创造性 | 头脑风暴、创意写作 |
| 1.0+ | 非常随机 | 艺术创作、实验性任务 |

### 示例对比

**Prompt:** "给这个函数起个名字：计算两个数的和"

**温度 0.0：**
```
add_numbers
```

**温度 0.7：**
```
calculate_sum
```

**温度 1.5：**
```
magical_number_combiner
```

### 使用建议

```python
# 代码生成 - 使用低温度
response = model.generate(
    prompt="写一个排序函数",
    temperature=0.2
)

# 创意写作 - 使用高温度
response = model.generate(
    prompt="写一个科幻故事",
    temperature=0.9
)
```

---

## 流式输出

### 什么是流式输出

流式输出（Streaming）是指 AI 逐字逐句地返回结果，而不是等待全部生成完成。

### 对比

**非流式：**
```
用户：写一篇文章
AI：[等待 30 秒]
AI：[一次性返回完整文章]
```

**流式：**
```
用户：写一篇文章
AI：标题...
AI：第一段...
AI：第二段...
AI：[逐步显示]
```

### 优势

- ✅ 更快的首字响应
- ✅ 更好的用户体验
- ✅ 可以提前看到结果
- ✅ 可以随时中断

### 代码示例

**Python (Claude):**
```python
import anthropic

client = anthropic.Anthropic()

with client.messages.stream(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    messages=[{"role": "user", "content": "写一首诗"}]
) as stream:
    for text in stream.text_stream:
        print(text, end="", flush=True)
```

**JavaScript (OpenAI):**
```javascript
const stream = await openai.chat.completions.create({
  model: 'gpt-4',
  messages: [{ role: 'user', content: '写一首诗' }],
  stream: true,
});

for await (const chunk of stream) {
  process.stdout.write(chunk.choices[0]?.delta?.content || '');
}
```

---

## 常见术语表

### AI 相关

| 术语 | 英文 | 说明 |
|------|------|------|
| 提示词 | Prompt | 发送给 AI 的指令 |
| 令牌 | Token | 文本处理的基本单位 |
| 上下文 | Context | AI 能"记住"的内容 |
| 温度 | Temperature | 控制输出随机性的参数 |
| 采样 | Sampling | AI 选择下一个词的方式 |
| 微调 | Fine-tuning | 针对特定任务训练模型 |
| 嵌入 | Embedding | 将文本转换为向量 |

### 模型相关

| 术语 | 说明 |
|------|------|
| LLM | Large Language Model，大语言模型 |
| GPT | Generative Pre-trained Transformer |
| API | Application Programming Interface |
| SDK | Software Development Kit |
| CLI | Command Line Interface |

### 功能相关

| 术语 | 说明 |
|------|------|
| Few-shot | 提供少量示例让 AI 学习 |
| Zero-shot | 不提供示例直接执行任务 |
| Chain of Thought | 让 AI 逐步思考问题 |
| RAG | Retrieval-Augmented Generation，检索增强生成 |
| Function Calling | 让 AI 调用外部函数 |

### 性能相关

| 术语 | 说明 |
|------|------|
| Latency | 延迟，从请求到响应的时间 |
| Throughput | 吞吐量，单位时间处理的请求数 |
| Rate Limit | 速率限制，限制请求频率 |
| Quota | 配额，可用的资源总量 |

---

## 实践建议

### 1. 从简单开始

先用简单的 Prompt 测试，逐步增加复杂度。

### 2. 迭代优化

根据结果不断调整 Prompt，找到最佳表达方式。

### 3. 保存模板

将好用的 Prompt 保存为模板，方便复用。

### 4. 监控使用

定期检查 token 使用量和费用，避免超支。

### 5. 学习示例

查看官方文档和社区示例，学习最佳实践。

---

## 下一步

现在你已经掌握了基础概念，可以：

1. 开始使用 [Claude Code](../02-claude-code/)
2. 学习 [Prompt Engineering 进阶](../06-advanced/prompt-engineering)
3. 查看[实战案例](../07-projects/)

---

[返回目录](index) | [上一章：准备工作](getting-started) | [下一部分：Claude Code 篇](../02-claude-code/)
