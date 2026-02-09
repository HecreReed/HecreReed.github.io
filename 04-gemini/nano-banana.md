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

## 多风格图像生成

Nano Banana 最强大的功能之一就是能够生成各种风格的图像,从写实照片到卡通插画,从扁平化设计到 3D 渲染,应有尽有。

### 支持的风格类型

Nano Banana 可以生成多种风格的图像:

- **写实照片风格**: 接近真实照片的效果
- **插画风格**: 手绘、卡通、漫画等
- **扁平化设计**: 现代 UI 设计常用的扁平风格
- **3D 渲染**: 立体感强的 3D 效果
- **艺术风格**: 油画、水彩、素描等艺术风格
- **PPT 图表风格**: 商务演示常用的图表和图示
- **技术图示**: 架构图、流程图、示意图等

### 模仿特定风格生成

Nano Banana 的一个强大功能是可以模仿某张图的风格去生成新图像。比如你看到一张 PPT 里的图很好看,想生成类似风格的图,可以这样做:

**步骤 1: 让 GPT 生成提示词**

把参考图发给 ChatGPT 或其他 GPT 模型,告诉它:

```
我要用 Nano Banana 去画这种风格的图,请帮我生成一个提示词,
用 markdown 代码块给我。
```

GPT 会分析图片的风格特征,然后生成一个详细的提示词:

````markdown
```
扁平化插画风格,简约现代,使用蓝色和橙色渐变,
几何图形组合,圆角矩形,柔和阴影,
商务演示风格,专业设计,高清
```
````

**步骤 2: 复制提示词给 Gemini**

复制 GPT 生成的提示词,然后在 Gemini 中开启画图功能,把提示词粘贴进去,并加上你要生成的具体内容:

```
[GPT 生成的风格提示词] + [你要画的内容]

例如:
扁平化插画风格,简约现代,使用蓝色和橙色渐变,
几何图形组合,圆角矩形,柔和阴影,
商务演示风格,专业设计,高清,
内容: 一个团队协作的场景,三个人在讨论项目
```

这样生成的图像就会保持参考图的风格,但内容是你想要的。

**实际应用场景:**

- **统一 PPT 风格**: 模仿 PPT 中某一页的图片风格,生成其他页面的配图
- **品牌视觉统一**: 模仿品牌设计风格,生成一系列配图
- **UI 设计**: 模仿某个 App 的插画风格,生成新的图标和插图
- **技术文档**: 模仿某个技术文档的图示风格,生成新的示意图

---

## 提示词技巧

写好提示词是生成高质量图像的关键。

### 提示词结构

一个好的提示词通常包含以下几个部分:

1. **风格**: 艺术风格或视觉风格(最重要)
2. **主体**: 图像的核心内容
3. **细节**: 颜色、光线、构图等
4. **质量词**: 提高图像质量的关键词

**示例:**

```
风格: 扁平化插画风格,现代简约
主体: 一个程序员在写代码
细节: 蓝色和白色配色,柔和光线,侧面视角
质量词: 高清,专业设计,矢量图风格
```

完整提示词:
```
扁平化插画风格,现代简约,一个程序员在写代码,
蓝色和白色配色,柔和光线,侧面视角,
高清,专业设计,矢量图风格
```

### 常用风格关键词

**商务/PPT 风格:**
- 扁平化插画风格
- 商务演示风格
- 几何图形组合
- 渐变色背景
- 圆角设计
- 专业简约

**技术图示风格:**
- 技术示意图风格
- 流程图风格
- 架构图风格
- 线条简洁
- 蓝白配色
- 图标化设计

**UI 设计风格:**
- 现代 UI 设计
- 移动端界面风格
- 玻璃拟态
- 新拟物化
- 渐变色卡片
- 阴影层次

**艺术风格:**
- 水彩画风格
- 油画风格
- 素描风格
- 像素艺术
- 赛博朋克风格
- 蒸汽波风格

### 提示词优化技巧

**1. 借助 GPT 生成提示词**

如果你不知道怎么描述想要的风格,可以:

- 把参考图发给 GPT,让它分析风格特征
- 描述你想要的效果,让 GPT 帮你生成提示词
- 让 GPT 优化你写的提示词,使其更准确

**2. 从简单开始,逐步细化**

先用简单的提示词生成,看看效果:
```
一个网站首页设计
```

如果效果不满意,逐步添加细节:
```
一个网站首页设计,现代风格,蓝白配色,扁平化设计
```

**3. 使用具体的风格参考**

可以参考知名的设计风格或品牌:
```
Apple 官网风格的产品展示页,极简主义,大量留白
```

```
Dribbble 流行的插画风格,渐变色,3D 元素
```

**4. 指定技术细节**

对于特定需求,可以指定技术细节:
```
PPT 配图,16:9 比例,扁平化插画,
蓝橙渐变,表现团队协作场景,
三个人物剪影,简约现代
```

---

## 截图伪造与去水印

Nano Banana 的一个强大但容易被忽视的功能是可以生成各种截图,只要提示词给得对,任何类型的截图都能画出来。

### 生成各类截图

通过精确的提示词,Nano Banana 可以生成:

- **软件界面截图**: IDE、编辑器、应用程序界面
- **网站截图**: 网页设计、后台管理界面
- **聊天记录截图**: 微信、QQ、Slack 等聊天界面
- **数据报表截图**: 数据分析、图表、仪表盘
- **系统界面截图**: Windows、macOS、Linux 桌面
- **移动端截图**: iOS、Android 应用界面

**示例提示词:**

```
macOS 终端截图,黑色背景,绿色文字,
显示 Python 代码运行结果,
包含命令提示符和输出信息,
真实的终端字体,专业截图
```

```
VS Code 编辑器截图,深色主题,
左侧文件树,中间代码编辑区显示 React 组件代码,
右侧终端显示 npm run dev 运行信息,
真实的 IDE 界面,高清截图
```

```
微信聊天界面截图,显示项目讨论内容,
包含文字消息和代码片段,
真实的微信界面风格,时间戳显示今天
```

### 去除水印

Nano Banana 生成的图片右下角会有水印,但可以通过专门的网站去除。

**去水印网站:**

有一些专门为 Gemini/Nano Banana 生成的图片去水印的网站,搜索 "Gemini 图片去水印" 或 "Nano Banana 去水印" 就能找到。这些网站可以:

- 自动识别并去除 Nano Banana 的水印
- 保持图片质量不变
- 快速处理,无需注册
- 免费使用

**使用流程:**

1. 在 Gemini 中用 Nano Banana 生成图片
2. 下载生成的图片(带水印)
3. 上传到去水印网站
4. 下载处理后的图片(无水印)

**注意事项:**

- 去水印后的图片可以用于个人项目、学习、演示等场景
- 如果用于商业用途,请遵守相关版权规定
- 建议保存原图和去水印后的图片,以备不同场景使用

### 实际应用场景

**1. 项目演示**

在做项目演示时,可以快速生成各种界面截图:

```
你需要展示一个数据分析平台,但还没开发完成。
可以用 Nano Banana 生成:
- 登录页面截图
- 数据仪表盘截图
- 报表页面截图
- 用户管理界面截图

提示词示例:
数据分析平台仪表盘截图,现代设计,深色主题,
左侧导航栏,顶部搜索和用户头像,
中间显示多个数据卡片和图表,
包含折线图、柱状图、饼图,
真实的 Web 应用界面,高清截图
```

**2. 技术文档配图**

为技术文档生成配图:

```
需要展示如何使用某个工具,但懒得真的去截图。
可以用 Nano Banana 生成:
- 安装过程截图
- 配置界面截图
- 运行结果截图
- 错误提示截图

提示词示例:
终端安装 Node.js 的截图,macOS 终端,
显示 brew install node 命令和安装过程输出,
包含进度条和成功提示,
真实的终端界面,专业截图
```

**3. 教程制作**

制作教程时快速生成示例截图:

```
写一个 React 教程,需要展示代码和运行效果。
可以用 Nano Banana 生成:
- VS Code 编辑器中的代码截图
- 浏览器中的运行效果截图
- 开发者工具的调试截图
- 错误提示和解决方案截图
```

**4. 产品原型**

在产品设计阶段快速生成原型截图:

```
需要向客户展示产品原型,但还没开始开发。
可以用 Nano Banana 生成:
- 各个页面的界面截图
- 不同状态下的界面变化
- 移动端和桌面端的对比
- 用户操作流程的截图序列
```

### 提示词技巧

生成高质量截图的关键是提示词要足够具体:

**1. 指定界面类型和平台**

```
macOS 系统截图 / Windows 系统截图 / iOS 应用截图
VS Code 编辑器 / Chrome 浏览器 / 微信界面
```

**2. 描述界面布局**

```
左侧文件树,中间代码编辑区,右侧终端
顶部导航栏,中间内容区,底部状态栏
```

**3. 指定内容细节**

```
显示 Python 代码,包含函数定义和注释
显示聊天记录,包含文字和表情
显示数据图表,包含折线图和数值标注
```

**4. 强调真实感**

```
真实的界面风格,专业截图,高清
实际的字体和配色,真实的阴影和圆角
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
