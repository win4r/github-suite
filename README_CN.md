![Built with Claude Code](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# github-suite

> GitHub 项目发现、源码深度分析与多轮迭代优化工具套件，适用于 Claude Code Skill 框架。

[English](README.md)

## 概览

| Skill | 版本 | 说明 |
|-------|------|------|
| `github-finder` | v2.1 | 多源多角度搜索，自适应评估，双语支持，搜索扩展 |
| `github-analyzer` | v2.0 | 6 维度源码深度分析，证据驱动评分，质量评估卡 |
| `github-optimizer` | v1.0 | 多轮迭代项目优化，严重等级驱动，质量关卡 |

## 工作流

```
┌─────────────────┐      链式调用       ┌──────────────────┐
│  github-finder   │ ──────────────────► │  github-analyzer  │
│  （项目发现）     │   可选深度调研触发   │  （源码分析）      │
│                  │                     │                   │
│  • 术语预研      │                     │  • 3 种模式       │
│  • 双语搜索      │                     │  • 6 维度分析     │
│  • 多角度查询    │                     │  • 质量评估卡     │
│  • 自适应星级 ★  │                     │  • 报告库         │
└─────────────────┘                      └──────────────────┘
        ▲                                         │
        │              用户请求                     │
        └──────────────────────────────────────────┘

┌──────────────────────────────────────────────────┐
│  github-optimizer（独立使用 或 分析后优化）         │
│                                                   │
│  • 深度侦察         • 严重等级分类                 │
│  • 多轮迭代修复     • 质量关卡                     │
│  • 代码审查         • 前后对比指标                 │
└──────────────────────────────────────────────────┘
```

## 核心能力

### github-finder v2.1

| 能力 | 说明 |
|------|------|
| 术语预研 | 搜索前识别产品名、代号、缩写 |
| 双语搜索 | 中文输入按 50/50 中英比例，英文输入按 30/70 比例并行查询 |
| 多角度查询 | >=3 个搜索角度：直接工具、生态插件、基础设施、社区、替代方案 |
| 自适应星级 | 按生态年龄动态调整阈值（成熟 >1000、成长 >200、新兴 >50） |
| 搜索扩展 | README 引用、GitHub Topics、竞品对比、引用图谱 |
| 社区源 | Hacker News、Reddit、V2EX、知乎 |
| 时间感知 | 查询附加年份，标注新项目和停滞项目 |
| 分类法先行 | 模糊需求自动拆解为可搜索子分类 |
| 错误恢复 | 搜索或抓取失败时的降级策略 |
| 并行搜索 | 使用 Agent 工具并行执行独立搜索 |

### github-analyzer v2.0

| 能力 | 说明 |
|------|------|
| 3 种分析模式 | 深度调研、快速概览、对比分析 |
| 6 章节报告 | 结构、架构、模块、模式、质量、创新 |
| 证据驱动评分 | 6 维评分卡（风格、错误处理、测试、文档、安全、架构），三级标准，引用具体文件和行号 |
| 模式检测 | 基于 Grep 的创建型、结构型、行为型模式检测 |
| 质量评估卡 | 多维度评分，强制提供证据 |
| 并行分析 | 使用 Agent 工具并发分析多个模块 |
| 对比矩阵 | 并排比较，给出明确推荐 |
| 报告库 | 分析报告本地存储与引用 |
| 自动清理 | 分析完成后自动删除 /tmp 中的克隆仓库 |

### github-optimizer v1.0

| 能力 | 说明 |
|------|------|
| 5 阶段工作流 | 侦察 -> 规划 -> 执行 -> 审查 -> 交付 |
| 严重等级驱动 | Critical -> High -> Medium -> Low，不混合等级 |
| 深度侦察 | 完整文件清单，结构理解，系统化问题扫描 |
| 8 类问题扫描 | 正确性、完整性、一致性、性能、安全、可用性、架构、可维护性 |
| 质量关卡 | 每轮完成后自检和回归检查 |
| 优化模式库 | 内置常见反模式识别（膨胀、过时引用、模糊指令等） |
| 前后对比指标 | 量化和定性改进对比 |
| 并行执行 | 使用 Agent 工具并行处理同一轮内的独立修复 |

## 使用方法

### 项目发现

```bash
# 基础搜索
/github-finder I need a Go CLI framework

# 双语技术选型
/github-finder 找一个替代 Notion 的开源笔记软件

# 新兴生态自适应搜索
/github-finder 基于 Gemini API 的开源项目

# 复杂需求分类法
/github-finder 我想把各种 AI API 统一管理起来
```

### 源码分析

```bash
# 深度调研（默认模式）
/github-analyzer https://github.com/user/repo deep-research

# 快速概览
/github-analyzer https://github.com/user/repo quick-overview

# 对比分析
/github-analyzer compare projectA vs projectB

# 指定关注维度
/github-analyzer https://github.com/user/repo deep-research focus on architecture and design patterns
```

### 项目优化

```bash
# 优化远程项目
/github-optimizer https://github.com/user/repo

# 优化当前本地项目
/github-optimizer .

# 优化指定本地路径
/github-optimizer /path/to/project
```

### 链式调用

```bash
# 发现后深度分析
/github-finder 找一个 AI 代码编辑器，找到后深度分析
```

## 环境要求

- [Claude Code](https://claude.ai/code)（CLI、桌面版或网页版）
- 可访问互联网（用于 GitHub 搜索和网页抓取）

## 安装

```bash
# 方式 1: 用户级安装（所有项目可用，推荐）
git clone https://github.com/win4r/github-suite.git /tmp/github-suite
cp -r /tmp/github-suite/github-finder ~/.claude/commands/github-finder
cp -r /tmp/github-suite/github-analyzer ~/.claude/commands/github-analyzer
cp -r /tmp/github-suite/github-optimizer ~/.claude/commands/github-optimizer
rm -rf /tmp/github-suite

# 方式 2: 项目级安装（仅在该项目中可用）
mkdir -p .claude/commands
git clone https://github.com/win4r/github-suite.git /tmp/github-suite
cp -r /tmp/github-suite/github-finder .claude/commands/github-finder
cp -r /tmp/github-suite/github-analyzer .claude/commands/github-analyzer
cp -r /tmp/github-suite/github-optimizer .claude/commands/github-optimizer
rm -rf /tmp/github-suite

# 重启 Claude Code 会话以加载新 Skill
```

> **注意**: 每个 Skill 是包含 `SKILL.md` 文件的目录。放在 `~/.claude/commands/` (用户级) 或 `.claude/commands/` (项目级) 下。

## 版本

| Skill | 版本 | 状态 |
|-------|------|------|
| github-finder | v2.1 | 稳定 |
| github-analyzer | v2.0 | 稳定 |
| github-optimizer | v1.0 | 稳定 |

## 许可证

[MIT](LICENSE) - 详见 LICENSE 文件。

## 致谢

完全使用 Anthropic 的 [Claude Code](https://claude.ai/code) 构建。

由 Claude Opus 4.6 协作完成。
