![Built with Claude Code](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# github-suite

> Claude Code SKILL suite for GitHub project discovery & source code analysis.

[中文文档](README_CN.md)

## Overview

| SKILL | Version | Description |
|-------|---------|-------------|
| `github-finder` | v2.0 | Multi-source bilingual search with adaptive thresholds |
| `github-analyzer` | v1.0 | 6-dimension deep source code analysis |

## Workflow

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

## Features

### github-finder v2.0

| Feature | Description |
|---------|-------------|
| Term Research | Pre-research brand names, codenames, abbreviations before searching |
| Bilingual Search | 50/50 CN/EN for Chinese input, 30/70 for English input |
| Multi-Angle Query | ≥3 angles: direct tool, ecosystem plugin, infra, community, alternative |
| Adaptive Stars | Dynamic thresholds by ecosystem age (mature >1000, growing >200, emerging >50) |
| Search Expansion | README references, GitHub Topics, competitor comparison, citation graph |
| Community Sources | Hacker News, Reddit, V2EX, Zhihu |
| Time Awareness | Current year in queries, 🆕 for new projects, ⚠️ for stale ones |

### github-analyzer v1.0

| Feature | Description |
|---------|-------------|
| 3 Analysis Modes | Deep Research, Quick Overview, Comparative |
| 6-Dimension Framework | Structure, Architecture, Modules, Patterns, Quality, Innovation |
| Quality Scorecard | Visual rating card with per-dimension scores |
| Report Library | Save and retrieve analysis reports for future reference |

## Usage

### Project Discovery

```bash
# Basic search
/github-finder I need a Go CLI framework

# Tech selection with bilingual support
/github-finder Find an open-source alternative to Notion

# Emerging ecosystem with adaptive thresholds
/github-finder Open-source projects built on Gemini API

# Complex requirement with taxonomy
/github-finder I want to unify multiple AI API providers
```

### Source Code Analysis

```bash
# Deep research
/github-analyzer https://github.com/user/repo deep-research

# Quick overview
/github-analyzer https://github.com/user/repo quick-overview

# Comparative analysis
/github-analyzer compare projectA vs projectB

# Focused dimensions
/github-analyzer https://github.com/user/repo deep-research focus on architecture and design patterns
```

### Chained Workflow

```bash
# Discover then analyze
/github-finder Find an AI code editor, then deep-analyze the best match
```

## Requirements

- [Claude Code](https://claude.ai/code) with SKILL framework support
- Internet access for GitHub search and web fetching

## Installation

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

## Version

| SKILL | Version | Status |
|-------|---------|--------|
| github-finder | v2.0 | Stable |
| github-analyzer | v1.0 | Stable |

## License

[MIT](LICENSE) - see LICENSE file for details.

## Credits

Built entirely with [Claude Code](https://claude.ai/code) by Anthropic.

Co-authored by Claude Opus 4.6.
