```text
  ____ _       _   _
 / ___| | ___ | |_| |__   ___ _ __
| |   | |/ _ \| __| '_ \ / _ \ '__|
| |___| | (_) | |_| | | |  __/ |
 \____|_|\___/ \__|_| |_|\___|_|
```

[English](README.md) | [中文](README.zh-CN.md)

**一键切换 Claude Code 服务商的命令行工具**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Shell](https://img.shields.io/badge/Shell-Bash-green.svg)](https://www.gnu.org/software/bash/)
[![Platform](https://img.shields.io/badge/Platform-macOS%20|%20Linux-lightgrey.svg)](#平台支持)

🔒 安全 • 🚀 快速 • 📦 轻量（约 500 行代码）

---

## 安装

```bash
# 1. 安装 Claude Code CLI
npm install -g @anthropic-ai/claude-code

# 2. 安装 Clother
curl -fsSL https://raw.githubusercontent.com/darkokoa/clother/main/clother.sh | bash

# 3. 添加到 PATH（根据提示执行）
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc && source ~/.zshrc
```

---

## 快速开始

### 已有 Claude Pro/Team 订阅？

```bash
clother-native              # 直接使用你的订阅，无需任何配置
```

### 想要使用其他模型？

```bash
clother config              # 配置 Z.AI、MiniMax、Kimi 等
clother-zai                 # 使用 Z.AI（GLM）
clother-zai-cn              # 使用智谱（GLM）
clother-minimax             # 使用 MiniMax
clother-minimax-cn          # 使用 MiniMax（中国）
```

---

## 服务商

### 原生 Anthropic（你的订阅）

```bash
clother-native              # Claude Sonnet/Opus/Haiku
                           # 使用你的 Claude Pro/Team 订阅
                           # 无需 API 密钥
```

### 第三方模型

| 命令 | 服务商 | 模型 | 获取 API 密钥 |
|---------|----------|--------|-------------|
| `clother-zai` | Z.AI | GLM-4.5-air、GLM-4.6 | [z.ai](https://z.ai) |
| `clother-zai-cn` | 智谱 | GLM-4.5-air、GLM-4.6 | [bigmodel.cn](https://bigmodel.cn) |
| `clother-minimax` | MiniMax | MiniMax-M2 | [minimax.io](https://minimax.io) |
| `clother-minimax-cn` | MiniMax（中国） | MiniMax-M2 | [minimaxi.com](https://minimaxi.com) |
| `clother-kimi` | 月之暗面 | Kimi-K2 系列 | [moonshot.ai](https://moonshot.ai) |
| `clother-katcoder` | KAT-Coder | KAT-Coder | [streamlake.ai](https://streamlake.ai) |

### 自定义服务商

添加自己的 Anthropic 兼容端点：

```bash
clother config              # 选择 "custom"
clother-myprovider          # 即可使用
```

---

## 命令

```bash
clother config              # 配置服务商
clother list                # 查看已配置的服务商
clother info <name>         # 查看服务商详情
clother uninstall           # 卸载
```

---

## 示例

```bash

# 传递任何 Claude Code 参数
clother-zai --dangerously-skip-permissions

# 查看配置信息
clother list
clother info zai
```

---

## 工作原理

Clother 创建小型启动脚本来设置环境变量：

```bash
# 当你运行：clother-zai
# 实际执行：
export ANTHROPIC_BASE_URL="https://api.z.ai/api/anthropic"
export ANTHROPIC_AUTH_TOKEN="$ZAI_API_KEY"
exec claude "$@"
```

无代理、无开销，仅通过环境变量实现。API 密钥安全存储在 `~/.clother/secrets.env`（chmod 600）。

---

## 常见问题

**可以同时使用多个服务商吗？**
可以。打开多个终端，每个都可以使用不同的服务商。

**API 密钥存储在哪里？**
存储在 `~/.clother/secrets.env`，权限为 `chmod 600`（只有你可以读取）。

**哪些服务商可以用？**
任何提供 Anthropic 兼容 API 的服务商。对于不兼容的服务商（如 OpenRouter、LiteLLM），请使用 [claude-code-router](https://github.com/musistudio/claude-code-router)。

**会修改我的 Claude 安装吗？**
不会。Clother 仅在启动 `claude` 前设置环境变量。

---

## 故障排除

| 问题 | 解决方案 |
|---------|----------|
| `claude: command not found` | 运行 `npm install -g @anthropic-ai/claude-code` |
| `clother: command not found` | 将 `~/bin` 添加到 PATH（参见安装步骤） |
| `API key not set` | 运行 `clother config` |

---

## 平台支持

✅ macOS (zsh/bash) • ✅ Linux (zsh/bash) • ✅ Windows (WSL)

---

## 许可证

MIT © [jolehuit](https://github.com/jolehuit)
