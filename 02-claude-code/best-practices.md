---
layout: default
title: 最佳实践
---

# Claude Code 最佳实践

本章将通过真实的使用案例，展示如何充分发挥 Claude Code 的能力，解决实际开发中的复杂问题。

---

## 实战案例一：本地开发 + 云端训练

### 场景描述

你在做大模型微调项目，这类任务非常吃显存，本地的 GPU 根本跑不动。于是你在 AutoDL 或其他云服务平台租了一台配备 4090 的服务器。现在的问题是：如何高效地在本地开发代码，然后自动上传到云服务器运行测试？

传统的做法是：本地写代码 → 手动 scp 上传 → SSH 登录服务器 → 手动运行脚本 → 查看日志 → 发现问题 → 回到本地修改 → 重复整个流程。这个过程繁琐且容易出错。

**Claude Code 可以让整个流程自动化。**

### 配置云服务器

首先，在云服务器上配置临时的 SSH 访问（使用密码或公钥）：

```bash
# 在云服务器上
# 如果使用密码（临时方案）
sudo passwd your_username

# 推荐：配置公钥（更安全）
# 在本地生成密钥对
ssh-keygen -t ed25519 -C "autodl-temp"

# 将公钥复制到服务器
ssh-copy-id -p 端口号 root@服务器IP
```

### 启动 Claude Code

在本地项目目录启动 Claude Code，使用自动执行模式：

```bash
cd /path/to/your/llm-finetuning-project
claude --bypass
```

### 与 Claude Code 对话

```
你：我在做大模型微调，本地没有足够的显存。我租了一台 AutoDL 的 4090 服务器。
服务器信息：
- IP: 123.456.789.10
- 端口: 12345
- 用户名: root
- 我已经配置好了 SSH 公钥

我需要你帮我：
1. 检查本地代码是否完整
2. 将代码上传到服务器的 /root/llm-finetuning 目录
3. 在服务器上自动检测 GPU 设备
4. 安装必要的依赖
5. 运行训练脚本
6. 实时监控训练日志

Claude Code：好的，我来帮你完成整个流程。

[检查本地代码]
发现以下文件：
- train.py: 训练脚本
- model.py: 模型定义
- config.yaml: 配置文件
- requirements.txt: 依赖列表

[上传代码到服务器]
执行 scp -P 12345 -r ./* root@123.456.789.10:/root/llm-finetuning/
上传完成！

[连接服务器检测 GPU]
执行 ssh -p 12345 root@123.456.789.10 "nvidia-smi"
检测到：
- GPU 0: NVIDIA GeForce RTX 4090 (24GB)
- CUDA Version: 12.1
- Driver Version: 535.129.03

[检查并安装依赖]
执行 ssh -p 12345 root@123.456.789.10 "cd /root/llm-finetuning && pip install -r requirements.txt"
依赖安装完成！

[修改训练脚本以自动检测 GPU]
我注意到 train.py 中硬编码了 device='cuda:0'，我来改成自动检测：

```python
# 修改前
device = 'cuda:0'

# 修改后
import torch
device = 'cuda' if torch.cuda.is_available() else 'cpu'
if torch.cuda.is_available():
    print(f"Using GPU: {torch.cuda.get_device_name(0)}")
    print(f"GPU Memory: {torch.cuda.get_device_properties(0).total_memory / 1024**3:.2f} GB")
else:
    print("No GPU available, using CPU")
```

[重新上传修改后的文件]
执行 scp -P 12345 train.py root@123.456.789.10:/root/llm-finetuning/

[启动训练]
执行 ssh -p 12345 root@123.456.789.10 "cd /root/llm-finetuning && nohup python train.py > train.log 2>&1 &"
训练已在后台启动！

[监控训练日志]
执行 ssh -p 12345 root@123.456.789.10 "tail -f /root/llm-finetuning/train.log"

输出：
Using GPU: NVIDIA GeForce RTX 4090
GPU Memory: 24.00 GB
Loading model...
Model loaded successfully
Starting training...
Epoch 1/10: Loss=2.345, Accuracy=0.678
Epoch 2/10: Loss=1.987, Accuracy=0.723
...

训练正在进行中！需要我继续监控吗？
```

### 后续迭代

当你需要修改代码时，只需告诉 Claude Code：

```
你：训练 loss 下降太慢了，帮我调整一下学习率，从 1e-4 改成 5e-5，
然后重新上传并重启训练。

Claude Code：好的，我来修改配置并重启训练。

[修改 config.yaml]
learning_rate: 1e-4  →  learning_rate: 5e-5

[停止当前训练]
执行 ssh -p 12345 root@123.456.789.10 "pkill -f train.py"

[上传新配置]
执行 scp -P 12345 config.yaml root@123.456.789.10:/root/llm-finetuning/

[重启训练]
执行 ssh -p 12345 root@123.456.789.10 "cd /root/llm-finetuning && nohup python train.py > train.log 2>&1 &"

训练已重启，使用新的学习率 5e-5。
```

### 关键要点

1. **自动化流程**：Claude Code 能够串联起整个开发-部署-测试流程
2. **智能检测**：自动检测 GPU 设备，无需手动配置
3. **实时监控**：可以实时查看训练日志，发现问题立即调整
4. **快速迭代**：修改代码后自动上传重启，无需手动操作
5. **安全建议**：使用公钥认证而不是密码，训练完成后记得删除临时密钥

---

## 实战案例二：修复 Ubuntu 图形界面

### 场景描述

这是一个真实发生的案例。你在 Ubuntu 系统上工作，突然图形界面崩溃了，或者你想安装图形界面但遇到各种问题。你尝试了各种方法——重启显示管理器、重装驱动、检查配置文件——折腾了半天还是没修好。

这种系统级问题往往涉及多个组件：显示管理器（GDM/LightDM）、X Server、显卡驱动、桌面环境等。排查起来非常复杂，需要检查日志、配置文件、服务状态，还要理解它们之间的依赖关系。

**Claude Code 可以在几分钟内诊断并修复这类问题。**

### 启动 Claude Code

关键是要给 Claude Code 足够的权限访问系统文件：

```bash
# 在任意目录启动，允许访问整个系统
cd ~
sudo claude --bypass

# 或者如果不想用 sudo，至少给予读取系统日志的权限
claude --bypass
```

### 与 Claude Code 对话

```
你：我的 Ubuntu 图形界面启动不了了，黑屏只有光标。
我尝试重启 gdm 服务也没用。能帮我诊断并修复吗？
你可以访问任何系统文件和日志。

Claude Code：好的，我来帮你诊断问题。

[检查显示管理器状态]
执行 systemctl status gdm
输出：
● gdm.service - GNOME Display Manager
   Loaded: loaded (/lib/systemd/system/gdm.service; enabled)
   Active: failed (Result: exit-code)
   ...
   Process: 1234 ExitCode=1

显示管理器启动失败了。让我检查日志。

[查看系统日志]
执行 journalctl -u gdm -n 50
发现错误：
"Failed to start X server"
"No screens found"

看起来是 X Server 配置问题。

[检查 X Server 配置]
读取 /etc/X11/xorg.conf
读取 /var/log/Xorg.0.log

发现问题：
Xorg.0.log 显示：
"(EE) NVIDIA(GPU-0): Failed to initialize the NVIDIA GPU"
"(EE) No devices detected"

是显卡驱动的问题。

[检查显卡驱动]
执行 nvidia-smi
输出：
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver.

驱动确实有问题。让我检查驱动版本。

执行 dpkg -l | grep nvidia
发现安装了多个版本的驱动，可能冲突了。

[诊断结果]
问题根源：
1. 安装了多个版本的 NVIDIA 驱动导致冲突
2. X Server 无法正确加载显卡驱动
3. GDM 因为 X Server 启动失败而无法启动

[修复方案]
我将执行以下操作：
1. 完全卸载所有 NVIDIA 驱动
2. 清理残留配置
3. 重新安装正确版本的驱动
4. 重新生成 X Server 配置
5. 重启 GDM

开始修复...

[卸载旧驱动]
执行 sudo apt-get purge nvidia-*
执行 sudo apt-get autoremove
执行 sudo apt-get autoclean

[清理配置]
删除 /etc/X11/xorg.conf
删除 /etc/modprobe.d/nvidia*.conf

[检测显卡型号]
执行 lspci | grep VGA
检测到：NVIDIA GeForce GTX 1660 Ti

[安装推荐驱动]
执行 ubuntu-drivers devices
推荐驱动：nvidia-driver-535

执行 sudo apt-get install nvidia-driver-535
安装完成！

[重新生成配置]
执行 sudo nvidia-xconfig
X Server 配置已生成。

[重启显示管理器]
执行 sudo systemctl restart gdm

[验证修复]
执行 systemctl status gdm
输出：
● gdm.service - GNOME Display Manager
   Loaded: loaded
   Active: active (running)

执行 nvidia-smi
输出：
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 535.129.03   Driver Version: 535.129.03   CUDA Version: 12.2   |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0  On |                  N/A |
| 30%   45C    P8    10W / 120W |    512MiB /  6144MiB |      2%      Default |
+-------------------------------+----------------------+----------------------+

完美！图形界面已修复。你现在应该能看到登录界面了。
如果还是黑屏，请尝试按 Ctrl+Alt+F1 切换到 tty1，然后再按 Ctrl+Alt+F7 切换回图形界面。
```

### 实际效果

在这个真实案例中：
- **人工排查**：花了半天时间，尝试了各种方法，还是没找到问题根源
- **Claude Code**：几分钟内就诊断出是驱动冲突，并完成了修复

Claude Code 的优势在于：
1. **系统性诊断**：按照逻辑顺序检查各个组件
2. **日志分析**：能够快速解读复杂的系统日志
3. **自动化修复**：不需要你手动执行每一步命令
4. **验证结果**：修复后自动验证是否成功

### 适用的其他场景

这种方法不仅适用于图形界面问题，还可以解决：

**网络问题：**
```
你：我的 Ubuntu 连不上网了，WiFi 图标都不见了。

Claude Code：[检查网络管理器]
[检查网卡驱动]
[检查网络配置]
[修复并重启网络服务]
```

**启动问题：**
```
你：系统启动很慢，卡在某个服务上。

Claude Code：[分析启动日志]
[找出耗时的服务]
[优化或禁用问题服务]
```

**软件包依赖问题：**
```
你：apt 安装软件时总是报依赖错误。

Claude Code：[检查软件包状态]
[修复损坏的依赖]
[清理冲突的包]
```

**权限问题：**
```
你：某个程序无法访问文件，提示权限不足。

Claude Code：[检查文件权限]
[检查 SELinux/AppArmor 策略]
[修复权限配置]
```

---

## 最佳实践总结

### 1. 给予适当的权限

对于系统级问题，不要吝啬权限。使用 `--bypass` 参数让 Claude Code 能够访问所有必要的文件和日志。

```bash
# 系统诊断
sudo claude --bypass

# 项目开发（限制在项目目录）
cd /path/to/project
claude --bypass
```

### 2. 清晰描述问题

提供足够的上下文信息：
- 问题的具体表现
- 已经尝试过的解决方法
- 相关的错误信息
- 系统环境（如果相关）

### 3. 利用远程能力

Claude Code 不仅能操作本地，还能通过 SSH 操作远程服务器。充分利用这个能力实现：
- 本地开发 + 云端测试
- 多服务器部署
- 自动化运维

### 4. 自动化重复任务

如果某个流程需要重复执行，让 Claude Code 帮你写成脚本：

```
你：把刚才的上传和运行流程写成一个脚本，以后我直接运行就行。

Claude Code：[生成 deploy.sh 脚本]
[添加错误处理]
[添加日志输出]
完成！以后只需运行 ./deploy.sh 即可。
```

### 5. 保存成功的方案

当 Claude Code 成功解决了一个复杂问题，让它生成文档：

```
你：把刚才修复图形界面的步骤整理成文档，以后遇到类似问题可以参考。

Claude Code：[生成 troubleshooting.md]
[包含诊断步骤]
[包含常见问题]
[包含预防措施]
```

### 6. 分步验证

对于复杂任务，让 Claude Code 分步执行并验证：

```
你：先上传代码，确认无误后再运行。

Claude Code：[上传代码]
[验证文件完整性]
[确认后再运行]
```

### 7. 使用 Plan 模式处理复杂任务

对于涉及多个步骤的复杂任务，使用 Plan 模式：

```bash
claude --plan --bypass
```

这样 Claude Code 会先制定详细计划，你审核后再执行，降低风险。

### 8. 安全注意事项

- **临时凭证**：云服务器使用完后删除临时密钥
- **敏感信息**：不要在对话中直接输入密码
- **备份重要数据**：系统级操作前先备份
- **审查修改**：重要文件修改后检查 diff

### 9. 成本控制

- 简单任务使用 Haiku 模型
- 复杂任务才用 Opus
- 使用 Plan 模式避免反复试错
- 考虑使用中转服务降低成本

### 10. 持续学习

记录 Claude Code 的解决方案，积累经验：
- 成功的配置方案
- 常见问题的解决步骤
- 有用的命令和脚本
- 避免的坑和注意事项

---

## 下一步

掌握了最佳实践后，你可以：

1. 查看[实战项目](../07-projects/)，了解更多应用场景
2. 探索[常见问题](../08-resources/faq)，解决使用中的疑惑
3. 学习其他工具：[Codex](../03-codex/)、[Gemini](../04-gemini/)、[Grok](../05-grok/)

---

[返回目录](index) | [上一章：高级功能](advanced-features) | [下一章：实战项目](../07-projects/)
