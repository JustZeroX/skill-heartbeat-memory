# Heartbeat-Memory

🧠 Heartbeat 自动记忆保存 - 在 Heartbeat 触发时自动检查新 sessions，生成 Daily 笔记，并定期提炼 MEMORY.md。

<!-- Badge Row 1: Core Info -->
[![ClawHub](https://img.shields.io/badge/ClawHub-heartbeat--memory-E75C46?logo=clawhub)](https://clawhub.ai/JustZeroX/heartbeat-memory)
[![GitHub](https://img.shields.io/badge/GitHub-skill--heartbeat--memory-181717?logo=github)](https://github.com/JustZeroX/skill-heartbeat-memory)
[![Version](https://img.shields.io/badge/version-0.0.3-orange)](https://github.com/JustZeroX/skill-heartbeat-memory)

<!-- Badge Row 2: Platforms -->
[![macOS](https://img.shields.io/badge/macOS-000000?logo=apple&logoColor=white)](https://openclaw.ai) 
[![Windows](https://img.shields.io/badge/Windows-0078D6?logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCA4OCA4OCI+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgMGgzOXYzOUgweiIvPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik00OSAwaDM5djM5SDQ5eiIvPjxwYXRoIGZpbGw9IiNmZmYiIGQ9Ik0wIDQ5aDM5djM5SDB6Ii8+PHBhdGggZmlsbD0iI2ZmZiIgZD0iTTQ5IDQ5aDM5djM5SDQ5eiIvPjwvc3ZnPg==)](https://openclaw.ai) 
[![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)](https://openclaw.ai)

<!-- Badge Row 3: License -->
[![License](https://img.shields.io/badge/License-MIT-BD2D2D)](LICENSE)

---

### 中文 | [English](#english-version)

---

## 🚀 快速开始

**3 步上手：**

```bash
# 1. 安装
clawhub install heartbeat-memory

# 2. 重启 Gateway
openclaw gateway restart

# 3. 等待 Heartbeat 自动触发
```

首次运行会自动创建配置文件，无需额外配置！

---

## 目录

- [✨ 核心功能](#-核心功能)
- [🔧 安装](#-安装)
- [📖 使用指南](#-使用指南)
- [⚙️ 配置说明](#️-配置说明)
- [📊 处理策略](#-处理策略)
- [❓ 常见问题](#-常见问题)
- [📄 许可证](#-许可证)

---

## ✨ 核心功能

- **🤖 自动检查新 sessions** - 每次 Heartbeat 触发时自动扫描
- **📝 Daily 笔记生成** - 自动生成格式化的每日聊天记录
- **🧠 MEMORY.md 提炼** - 定期提炼长期记忆
- **📊 智能分批处理** - 根据任务量自动选择处理策略
- **📈 状态追踪** - 记录处理进度，支持断点续处理
- **🔔 完成通知** - 处理后自动发送通知
- **🚀 无需配置 LLM** - 自动使用 OpenClaw 主配置的 LLM
- **💾 自动初始化** - 首次运行自动创建配置文件和目录

---

## 🔧 安装

### 方式 1：Via ClawHub（推荐 ⭐）

若未安装 clawhub，请先安装：
```bash
npm install -g clawhub
```

已安装 clawhub 后，执行：
```bash
clawhub install heartbeat-memory
openclaw gateway restart
```

**优点：**
- ✅ 一键安装，自动下载到全局目录
- ✅ 所有工作区共享
- ✅ 支持后续更新

### 方式 2：Manual / Git

```bash
git clone https://github.com/JustZeroX/skill-heartbeat-memory.git ~/.openclaw/skills/heartbeat-memory
openclaw gateway restart
```

**适用场景：**
- ✅ 想要自定义代码
- ✅ 参与贡献开发
- ✅ ClawHub 不可用时

### 验证安装

```bash
ls ~/.openclaw/skills/heartbeat-memory/SKILL.md
```

看到文件即表示安装成功。

---

## 📖 使用指南

### 执行方式

**方式 1：Heartbeat 自动触发（推荐）**
```
Heartbeat 每 30 分钟触发 → 自动执行 heartbeat-memory
```

**方式 2：手动调用（subagent 环境）**
```javascript
const heartbeat = require('~/.openclaw/skills/heartbeat-memory/index.js');
await heartbeat.run();
```

### 查看结果

```bash
# 查看当前工作区
echo $OPENCLAW_WORKSPACE

# 查看 Daily 笔记
cat $OPENCLAW_WORKSPACE/memory/daily/YYYY-MM-DD.md

# 查看长期记忆
cat $OPENCLAW_WORKSPACE/MEMORY.md

# 查看配置
cat $OPENCLAW_WORKSPACE/memory/heartbeat-memory-config.json
```

### 修改配置

```bash
vim $OPENCLAW_WORKSPACE/memory/heartbeat-memory-config.json
```

---

## ⚙️ 配置说明

### 🚀 无需配置 LLM！

Skill 会自动使用 OpenClaw 主配置的 LLM，无需单独配置 API Key。

### 可选配置项

编辑 `<工作区>/memory/heartbeat-memory-config.json`：

| 配置项 | 说明 | 默认值 |
|--------|------|--------|
| `enabled` | 是否启用 | `true` |
| `batchSize` | 每批处理数 | `5` |
| `largeTaskThreshold` | subagent 阈值 | `10` |
| `timeoutSeconds` | LLM 超时时间（秒） | `1000` |
| `notifyTarget` | 通知目标 | 自动获取 |
| `processSessionsAfter` | 只处理此日期后的 sessions | `null` |
| `maxSessionsPerRun` | 单次最多处理 sessions 数 | `50` |
| `refineSchedule.type` | 提炼频率 | `weekly` |
| `refineSchedule.dayOfWeek` | 每周几 | `sunday` |
| `refineSchedule.time` | 每日时间 | `20:00` |

**timeoutSeconds 建议：**
- 少量 sessions (<10 个)：300-600 秒
- 中量 sessions (10-30 个)：600-1000 秒
- 大量 sessions (>30 个)：1000-1800 秒
- 首次运行（全量处理）：1800-3600 秒

### 配置示例

**基础配置（默认）：**
```json
{
  "memorySave": {
    "enabled": true
  }
}
```

**首次运行限制（避免处理大量历史数据）：**
```json
{
  "memorySave": {
    "enabled": true,
    "processSessionsAfter": "2026-03-01T00:00:00Z",
    "maxSessionsPerRun": 20
  }
}
```

**指定通知渠道（飞书）：**
```json
{
  "notifyTarget": "feishu:ou_xxxxxxxxxxxxx",
  "memorySave": {
    "enabled": true
  }
}
```

---

## 📊 处理策略

### 首次启用

首次运行时：
- 自动扫描所有 sessions
- 分批处理（每批 5 个）
- 生成对应日期的 Daily 笔记
- 首次强制触发一次 MEMORY.md 提炼

### 日常增量

| 数量 | 策略 | 耗时 |
|------|------|------|
| < 5 个 | 直接处理 | <2 分钟 |
| 5-10 个 | 分批处理 | 2-5 分钟 |
| > 10 个 | 启动 subagent | 5-10 分钟 |

### 处理流程

```
Heartbeat 触发
    ↓
sessions_list 获取会话列表
    ↓
sessions_history 获取消息内容
    ↓
sessions_spawn 启动 subagent 进行 LLM 提炼
    ↓
写入 Daily 笔记
    ↓
检查是否提炼 MEMORY.md
    ↓
发送完成通知
```

---

## ❓ 常见问题

**Q: 需要配置 LLM API Key 吗？**  
A: **不需要！** Skill 会自动使用 OpenClaw 主配置的 LLM，通过 subagent 方式调用。

**Q: 多久检查一次？**  
A: 跟随 Heartbeat 频率：
- 工作日：09:00 / 14:00 / 20:00
- 周末：10:00 / 20:00

**Q: 如何查看处理进度？**  
A: 处理完成后会自动发送通知，包含：检查 sessions 数、新处理数、是否提炼 MEMORY。

**Q: 可以修改提炼频率吗？**  
A: 可以，编辑配置文件中的 `refineSchedule`。

**Q: 如何处理大量 sessions？**  
A: 自动分批处理，每次 Heartbeat 最多处理 5 个，剩余下次继续。

**Q: 可以禁用自动保存吗？**  
A: 可以，配置文件中设置 `"enabled": false`。

**Q: 首次运行会提炼 MEMORY.md 吗？**  
A: **会！** 首次运行会强制触发一次 MEMORY.md 提炼，之后按计划频率执行。

---

## 🌍 跨平台支持

### 平台兼容

- ✅ **macOS** - 完全支持
- ✅ **Linux** - 完全支持
- ✅ **Windows** - 完全支持（PowerShell/CMD）

### 多工作区支持

Skill 自动支持多工作区，无需额外配置：

| 工作区类型 | 配置位置 | 数据位置 |
|-----------|---------|---------|
| **默认工作区** | `~/.openclaw/workspace/` | `~/.openclaw/workspace/memory/` |
| **自定义工作区** | `$OPENCLAW_WORKSPACE/` | `$OPENCLAW_WORKSPACE/memory/` |
| **项目工作区** | `./.openclaw/` | `./.openclaw/memory/` |

---

## 📄 许可证

MIT License

---

[Top / 返回顶部](#heartbeat-memory)

---

## English Version

### 🚀 Quick Start

**3 Steps:**

```bash
# 1. Install
clawhub install heartbeat-memory

# 2. Restart Gateway
openclaw gateway restart

# 3. Wait for Heartbeat trigger
```

---

### Table of Contents

- [✨ Core Features](#-core-features)
- [🔧 Installation](#-installation)
- [📖 Usage Guide](#-usage-guide)
- [⚙️ Configuration](#️-configuration)
- [📊 Processing Strategy](#-processing-strategy)
- [❓ FAQ](#-faq)
- [📄 License](#-license)

---

### ✨ Core Features

- **🤖 Auto Check Sessions** - Scan new sessions on every Heartbeat trigger
- **📝 Daily Note Generation** - Auto-generate formatted daily chat logs
- **🧠 MEMORY.md Refinement** - Periodically refine long-term memory
- **📊 Smart Batching** - Auto-select processing strategy based on task volume
- **📈 Progress Tracking** - Record processing state, support resume
- **🔔 Completion Notification** - Auto-send notification after processing
- **🚀 No LLM Config** - Auto-use OpenClaw's main LLM
- **💾 Auto Initialization** - Create config files and directories on first run

---

### 🔧 Installation

#### Option 1: Via ClawHub (Recommended ⭐)

```bash
npm install -g clawhub  # If not installed
clawhub install heartbeat-memory
openclaw gateway restart
```

**Benefits:**
- ✅ One-click install to global directory
- ✅ Share across all workspaces
- ✅ Support updates

#### Option 2: Manual / Git

```bash
git clone https://github.com/JustZeroX/skill-heartbeat-memory.git ~/.openclaw/skills/heartbeat-memory
openclaw gateway restart
```

**Use Cases:**
- ✅ Want to customize code
- ✅ Contribute to development
- ✅ ClawHub unavailable

---

### 📖 Usage Guide

#### Execution Methods

**Method 1: Heartbeat Auto-Trigger (Recommended)**
```
Heartbeat every 30 min → Auto-execute heartbeat-memory
```

**Method 2: Manual Call (subagent)**
```javascript
const heartbeat = require('~/.openclaw/skills/heartbeat-memory/index.js');
await heartbeat.run();
```

#### View Results

```bash
echo $OPENCLAW_WORKSPACE
cat $OPENCLAW_WORKSPACE/memory/daily/YYYY-MM-DD.md
cat $OPENCLAW_WORKSPACE/MEMORY.md
```

---

### ⚙️ Configuration

### 🚀 No LLM Config Needed!

Skill auto-uses OpenClaw's main LLM configuration.

#### Optional Config

Edit `<workspace>/memory/heartbeat-memory-config.json`:

| Config | Description | Default |
|--------|-------------|---------|
| `enabled` | Enable/disable | `true` |
| `batchSize` | Batch size | `5` |
| `timeoutSeconds` | LLM timeout (seconds) | `1000` |
| `notifyTarget` | Notification target | Auto-detect |
| `processSessionsAfter` | Process sessions after date | `null` |
| `refineSchedule.type` | Refinement frequency | `weekly` |

**timeoutSeconds Recommendations:**
- Few sessions (<10): 300-600 seconds
- Medium sessions (10-30): 600-1000 seconds
- Many sessions (>30): 1000-1800 seconds
- First run (full): 1800-3600 seconds

#### Config Examples

**Basic (Default):**
```json
{
  "memorySave": {
    "enabled": true
  }
}
```

**First Run (Limit History):**
```json
{
  "memorySave": {
    "enabled": true,
    "processSessionsAfter": "2026-03-01T00:00:00Z",
    "maxSessionsPerRun": 20
  }
}
```

**Custom Notification (Feishu):**
```json
{
  "notifyTarget": "feishu:ou_xxxxxxxxxxxxx",
  "memorySave": {
    "enabled": true
  }
}
```

---

### 📊 Processing Strategy

#### First Run

- Scan all sessions
- Batch process (5 per batch)
- Generate Daily notes
- Force refine MEMORY.md once

#### Daily Incremental

| Count | Strategy | Time |
|-------|----------|------|
| < 5 | Direct process | <2 min |
| 5-10 | Batch process | 2-5 min |
| > 10 | Subagent | 5-10 min |

#### Workflow

```
Heartbeat Trigger
    ↓
sessions_list get session list
    ↓
sessions_history get message content
    ↓
sessions_spawn subagent for LLM refinement
    ↓
Write Daily notes
    ↓
Check if refine MEMORY.md
    ↓
Send completion notification
```

---

### ❓ FAQ

**Q: Need LLM API Key?**  
A: **No!** Skill auto-uses OpenClaw's main LLM via subagent.

**Q: How often to check?**  
A: Follows Heartbeat frequency (Weekdays: 09:00/14:00/20:00, Weekends: 10:00/20:00).

**Q: How to check progress?**  
A: Auto-send notification after completion with stats.

**Q: Can I change refinement frequency?**  
A: Yes, edit `refineSchedule` in config.

**Q: Can I disable auto-save?**  
A: Yes, set `"enabled": false` in config.

**Q: Will first run refine MEMORY.md?**  
A: **Yes!** First run forces one MEMORY.md refinement.

---

### 🌍 Cross-Platform Support

#### Platform Compatibility

- ✅ **macOS** - Full support
- ✅ **Linux** - Full support
- ✅ **Windows** - Full support (PowerShell/CMD)

#### Multi-Workspace

| Workspace Type | Config Location | Data Location |
|---------------|-----------------|---------------|
| **Default** | `~/.openclaw/workspace/` | `~/.openclaw/workspace/memory/` |
| **Custom** | `$OPENCLAW_WORKSPACE/` | `$OPENCLAW_WORKSPACE/memory/` |
| **Project** | `./.openclaw/` | `./.openclaw/memory/` |

---

### 📄 License

MIT License

---

[Top](#heartbeat-memory)
