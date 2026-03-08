![Built with Claude Code](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# github-suite

> Claude Code SKILL suite for GitHub project discovery & source code analysis.
>
> GitHub 项目发现与源码深度分析工具套件，适用于 Claude Code SKILL 框架。

## Overview / 概览

| SKILL | Version | Description | 说明 |
|-------|---------|-------------|------|
| `github-finder` | v2.0 | Multi-source bilingual search with adaptive thresholds | 多源多角度搜索，自适应评估，双语支持 |
| `github-analyzer` | v1.0 | 6-dimension deep source code analysis | 6 维度源码深度分析，质量评估卡 |

## Workflow / 工作流

```
┌─────────────────┐     chain call      ┌──────────────────┐
│  github-finder   │ ──────────────────► │  github-analyzer  │
│  (Discovery)     │   optional deep     │  (Analysis)       │
│                  │   research trigger   │                   │
│  • Term research │                     │  • 3 modes        │
│  • Bilingual     │                     │  • 6 dimensions   │
│  • Multi-angle   │                     │  • Quality card   │
│  • Adaptive ★    │                     │  • Report library │
└─────────────────┘                      └──────────────────┘
        ▲                                         │
        │            User Request                  │
        └──────────────────────────────────────────┘
```

## Features / 核心能力

### github-finder v2.0

| Feature | Description | 说明 |
|---------|-------------|------|
| Term Research | Pre-research brand names, codenames, abbreviations before searching | 术语预研：搜索前识别产品名/代号/缩写 |
| Bilingual Search | 50/50 CN/EN for Chinese input, 30/70 for English input | 双语搜索：中英文按比例并行查询 |
| Multi-Angle Query | ≥3 angles: direct tool, ecosystem plugin, infra, community, alternative | 多角度查询：≥3 个搜索角度覆盖 |
| Adaptive Stars | Dynamic thresholds by ecosystem age (mature >1000, growing >200, emerging >50) | 自适应星级：按生态年龄动态调整阈值 |
| Search Expansion | README references, GitHub Topics, competitor comparison, citation graph | 搜索扩展：README 引用、Topics、竞品对比 |
| Community Sources | Hacker News, Reddit, V2EX, Zhihu | 社区源：多平台技术社区补充搜索 |
| Time Awareness | Current year in queries, 🆕 for new projects, ⚠️ for stale ones | 时间感知：年份附加、新旧项目标注 |

### github-analyzer v1.0

| Feature | Description | 说明 |
|---------|-------------|------|
| 3 Analysis Modes | Deep Research, Quick Overview, Comparative | 3 种模式：深度调研、快速概览、对比分析 |
| 6-Dimension Framework | Structure, Architecture, Modules, Patterns, Quality, Innovation | 6 维度：结构、架构、模块、模式、质量、创新 |
| Quality Scorecard | Visual rating card with per-dimension scores | 质量评估卡：多维度评分可视化 |
| Report Library | Save and retrieve analysis reports for future reference | 成果库：调研报告存储与引用 |

## Usage / 使用方法

### Project Discovery / 项目发现

```bash
# Basic search / 基础搜索
/github-finder I need a Go CLI framework

# Bilingual tech selection / 双语技术选型
/github-finder 找一个替代 Notion 的开源笔记软件

# Emerging ecosystem with adaptive thresholds / 新兴生态自适应搜索
/github-finder 基于 Gemini API 的开源项目

# Complex requirement with taxonomy / 复杂需求分类法
/github-finder 我想把各种 AI API 统一管理起来
```

### Source Code Analysis / 源码分析

```bash
# Deep research / 深度调研
/github-analyzer https://github.com/user/repo 深度调研

# Quick overview / 快速概览
/github-analyzer https://github.com/user/repo 快速概览

# Comparative analysis / 对比分析
/github-analyzer 对比 projectA vs projectB

# Focused dimensions / 指定关注维度
/github-analyzer https://github.com/user/repo 深度调研 关注架构设计和设计模式
```

### Chained Workflow / 链式调用

```bash
# Discover then analyze / 发现后深度分析
/github-finder 找一个 AI 代码编辑器，找到后深度分析
```

## Requirements / 环境要求

- [Claude Code](https://claude.ai/code) with SKILL framework support
- Internet access for GitHub search and web fetching

## Installation / 安装

```bash
# Clone to your SKILL repository
git clone https://github.com/HeroAshacker/github-suite.git \
  ~/.claude/skill-repository/github-suite

# Activate SKILLs (create symlinks)
ln -s ~/.claude/skill-repository/github-suite/github-finder \
  ~/.claude/skills/github-finder
ln -s ~/.claude/skill-repository/github-suite/github-analyzer \
  ~/.claude/skills/github-analyzer

# Restart Claude Code session to load new SKILLs
```

## Version / 版本

| SKILL | Version | Status |
|-------|---------|--------|
| github-finder | v2.0 | Stable |
| github-analyzer | v1.0 | Stable |

## License

[MIT](LICENSE) - see LICENSE file for details.

## Credits / 致谢

Built entirely with [Claude Code](https://claude.ai/code) by Anthropic.

Co-authored by Claude Opus 4.6.
