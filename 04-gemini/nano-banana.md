---
layout: default
title: Nano Banana
---

# Nano Banana

Nano Banana 是 Google 在 2025 年 11 月推出的 AI 图像生成工具,作为 Gemini 生态系统的一部分。它能够根据文本描述生成高质量的图像,并提供强大的图像编辑功能。

---

## Nano Banana 简介

Nano Banana 是 Google 对标 DALL-E、Midjourney、Stable Diffusion 等图像生成工具的产品。它的最大特点是与 Gemini API 深度集成,可以在编程项目中轻松调用,实现自动化的图像生成和处理。

### 主要版本

**Nano Banana Pro**

这是目前最新的版本,提供了更高的图像质量和更多的编辑功能。Pro 版本支持:
- 更高分辨率的图像生成
- 更精准的提示词理解
- 图像编辑和修改功能
- 批量生成和处理

**Nano Banana 2**

这是社区版本,提供了基础的图像生成功能。虽然功能相对简单,但对于日常使用已经足够。

---

## 图像生成功能

Nano Banana 的核心功能是根据文本描述生成图像。

### 基础图像生成

最简单的使用方式就是给它一段文字描述,它会生成对应的图像:

```python
import google.generativeai as genai

# 配置 API
genai.configure(api_key='YOUR_API_KEY')

# 生成图像
response = genai.generate_image(
    prompt="一个现代化的网站首页设计,简洁风格,蓝白配色",
    model="nano-banana-pro"
)

# 保存图像
response.save("homepage_design.png")
```

### 风格控制

Nano Banana 支持多种艺术风格:

```python
# 写实风格
genai.generate_image(
    prompt="一个程序员在写代码",
    style="photorealistic"
)

# 插画风格
genai.generate_image(
    prompt="一个程序员在写代码",
    style="illustration"
)

# 极简风格
genai.generate_image(
    prompt="一个程序员在写代码",
    style="minimalist"
)
```

### 尺寸和比例

可以指定生成图像的尺寸和比例:

```python
# 方形图像
genai.generate_image(
    prompt="网站 Logo 设计",
    aspect_ratio="1:1",
    size="1024x1024"
)

# 宽屏图像
genai.generate_image(
    prompt="网站横幅设计",
    aspect_ratio="16:9",
    size="1920x1080"
)

# 竖屏图像
genai.generate_image(
    prompt="手机 App 启动页",
    aspect_ratio="9:16",
    size="1080x1920"
)
```

---

## 图像编辑功能

Nano Banana Pro 不仅能生成图像,还能编辑现有图像。

### 局部修改

可以指定修改图像的某个部分:

```python
# 上传原图
original_image = genai.upload_image("original.png")

# 修改局部
response = genai.edit_image(
    image=original_image,
    prompt="把背景改成蓝色渐变",
    mask_area="background"
)
```

### 风格转换

可以将图像转换成不同的艺术风格:

```python
# 照片转插画
response = genai.edit_image(
    image=original_image,
    prompt="转换成扁平化插画风格"
)

# 添加特效
response = genai.edit_image(
    image=original_image,
    prompt="添加赛博朋克风格的霓虹灯效果"
)
```

### 图像扩展

可以扩展图像的边界,自动生成周围的内容:

```python
# 向右扩展图像
response = genai.extend_image(
    image=original_image,
    direction="right",
    width=512
)
```

---

## 提示词技巧

写好提示词是生成高质量图像的关键。

### 提示词结构

一个好的提示词通常包含以下几个部分:

1. **主体**: 图像的核心内容
2. **风格**: 艺术风格或视觉风格
3. **细节**: 颜色、光线、构图等
4. **质量词**: 提高图像质量的关键词

**示例:**

```
主体: 一个现代化的办公室
风格: 极简主义设计
细节: 大落地窗,自然光线,白色和木色搭配
质量词: 高清,专业摄影,8K 分辨率
```

完整提示词:
```
一个现代化的办公室,极简主义设计,大落地窗,自然光线,
白色和木色搭配,高清,专业摄影,8K 分辨率
```

### 常用质量词

这些词可以提高生成图像的质量:

- **高清相关**: 高清、4K、8K、超高清、专业摄影
- **光线相关**: 自然光、柔和光线、戏剧性光线、黄金时段
- **构图相关**: 对称构图、三分法、特写、全景
- **风格相关**: 写实、插画、扁平化、3D 渲染、手绘

### 避免的词汇

有些词汇可能导致生成效果不佳:

- 过于抽象的概念
- 相互矛盾的描述
- 过于复杂的场景
- 版权相关的品牌名称

### 提示词优化技巧

**1. 从简单开始**

先用简单的提示词生成,看看效果:
```
一个网站首页设计
```

**2. 逐步添加细节**

如果效果不满意,逐步添加细节:
```
一个网站首页设计,现代风格,蓝白配色
```

**3. 使用参考风格**

可以参考知名设计师或艺术家的风格:
```
一个网站首页设计,Apple 官网风格,极简主义
```

**4. 指定技术细节**

对于特定需求,可以指定技术细节:
```
一个网站首页设计,1920x1080,响应式布局,
包含导航栏、Hero 区域、功能介绍、底部信息
```

---

## 实际应用案例

Nano Banana 在编程项目中有很多实用的应用场景。

### UI 原型设计

在开发前端项目时,可以用 Nano Banana 快速生成 UI 原型:

```python
# 生成登录页面原型
login_page = genai.generate_image(
    prompt="""
    登录页面设计,现代风格,居中布局,
    包含 Logo、用户名输入框、密码输入框、登录按钮,
    蓝白配色,简洁大方
    """,
    size="1920x1080"
)

# 生成仪表盘原型
dashboard = genai.generate_image(
    prompt="""
    数据仪表盘设计,包含侧边栏导航、顶部搜索栏、
    多个数据卡片、图表展示,深色主题
    """,
    size="1920x1080"
)
```

### 自动生成占位图

在开发过程中,可以自动生成占位图:

```python
def generate_placeholder(category, size):
    """生成指定类别和尺寸的占位图"""
    prompts = {
        "user": "用户头像,简约风格,圆形",
        "product": "产品展示图,现代风格,白色背景",
        "banner": "网站横幅,抽象几何图案,渐变色"
    }

    return genai.generate_image(
        prompt=prompts[category],
        size=size
    )

# 批量生成
user_avatar = generate_placeholder("user", "256x256")
product_img = generate_placeholder("product", "800x800")
banner_img = generate_placeholder("banner", "1920x400")
```

### 图标和 Logo 生成

可以快速生成项目所需的图标和 Logo:

```python
# 生成 App 图标
app_icon = genai.generate_image(
    prompt="App 图标,代表代码和 AI,极简风格,蓝色渐变",
    size="512x512",
    style="flat"
)

# 生成 Logo
logo = genai.generate_image(
    prompt="公司 Logo,字母 'AI',现代科技感,蓝色",
    size="1024x1024",
    style="minimalist"
)
```

### 营销素材生成

可以为项目生成营销素材:

```python
# 生成社交媒体封面
social_cover = genai.generate_image(
    prompt="""
    社交媒体封面图,展示 AI 编程助手,
    现代科技风格,蓝紫渐变,包含产品截图
    """,
    size="1200x630"
)

# 生成宣传海报
poster = genai.generate_image(
    prompt="""
    产品宣传海报,AI 编程工具,
    未来科技感,霓虹灯效果,深色背景
    """,
    size="1080x1920"
)
```

### 文档配图

可以为技术文档生成配图:

```python
# 生成架构图示意
architecture = genai.generate_image(
    prompt="""
    系统架构图示意,包含前端、后端、数据库,
    简洁的流程图风格,蓝白配色
    """,
    size="1600x900"
)

# 生成流程图
flowchart = genai.generate_image(
    prompt="""
    用户注册流程图,包含输入、验证、保存、发送邮件等步骤,
    扁平化风格,清晰易懂
    """,
    size="1200x800"
)
```

---

## 与其他图像生成工具对比

让我们看看 Nano Banana 与其他主流图像生成工具的区别。

### Nano Banana vs DALL-E

**Nano Banana 的优势:**
- 与 Gemini API 深度集成,编程调用更方便
- 免费额度相对慷慨
- 支持图像编辑和扩展
- 响应速度较快

**DALL-E 的优势:**
- 图像质量可能更高
- 提示词理解更准确
- 生成的图像更有创意
- 社区资源更丰富

### Nano Banana vs Midjourney

**Nano Banana 的优势:**
- 提供 API 接口,可编程调用
- 价格更透明,按量计费
- 集成在 Gemini 生态中
- 适合自动化场景

**Midjourney 的优势:**
- 艺术性更强
- 图像质量更高
- 风格更多样
- 社区更活跃

### Nano Banana vs Stable Diffusion

**Nano Banana 的优势:**
- 无需本地部署,开箱即用
- 不需要 GPU,成本更低
- API 调用简单
- 官方支持和维护

**Stable Diffusion 的优势:**
- 完全开源,可自定义
- 可本地运行,数据更安全
- 社区模型丰富
- 无使用限制

### 使用建议

- **快速原型和自动化**: 选 Nano Banana
- **艺术创作和高质量图像**: 选 Midjourney 或 DALL-E
- **本地部署和自定义**: 选 Stable Diffusion
- **编程项目集成**: 选 Nano Banana 或 DALL-E API

---

## 免费使用方式

Nano Banana 提供了多种免费使用方式。

### 官方 API 免费额度

通过 Gemini API 调用 Nano Banana,有一定的免费额度:

- 每天可以生成一定数量的图像
- 免费额度对个人项目基本够用
- 超出后按量计费,价格合理

### 第三方免费服务

有一些第三方网站提供免费的 Nano Banana 访问:

- **banana-ai.org**: 免费使用,无需注册
- **easemate.ai**: 提供 Nano Banana 免费生成
- **nanabananaai.com**: Nano Banana 2 免费版本

这些服务适合快速测试和个人使用,但可能有使用限制。

### Google AI Studio

在 Google AI Studio 中可以直接使用 Nano Banana:

1. 访问 [Google AI Studio](https://ai.google.dev/)
2. 登录 Google 账号
3. 选择 Nano Banana 模型
4. 输入提示词生成图像

这种方式适合学习和实验,有可视化界面,使用方便。

---

## 开始使用

要开始使用 Nano Banana,你需要:

1. 注册 Google AI Studio 账号
2. 获取 Gemini API Key
3. 安装 Python SDK: `pip install google-generativeai`
4. 开始生成图像

**快速开始示例:**

```python
import google.generativeai as genai

# 配置 API Key
genai.configure(api_key='YOUR_API_KEY')

# 生成第一张图像
response = genai.generate_image(
    prompt="一只可爱的猫咪,卡通风格",
    model="nano-banana-pro"
)

# 保存图像
response.save("my_first_image.png")
print("图像已生成!")
```

---

## 下一步

了解了 Nano Banana 后,你可以:

1. 尝试在项目中集成图像生成功能
2. 探索更多提示词技巧
3. 学习其他 AI 工具:[Grok](../05-grok/)

---

[返回目录](index) | [上一章: Gemini 简介](introduction) | [下一部分: Grok 篇](../05-grok/index)

---

## 参考资料

- [Nano Banana Pro 官方发布](https://blog.google/innovation-and-ai/products/nano-banana-pro/)
- [Gemini API 图像生成文档](https://ai.google.dev/gemini-api/docs/image-generation)
- [Nano Banana Pro 完全指南 2026](https://www.youtube.com/watch?v=ZCw325FiS78)
- [Gemini 图像生成概览](https://gemini.google/overview/image-generation/)
- [Banana AI 免费编辑器](https://banana-ai.org/)
- [Nano Banana 免费生成器](https://www.easemate.ai/nano-banana-ai-image-generator)
- [Nano Banana 2 官网](https://nano-banana2.co/)
