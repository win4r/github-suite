![Built with Claude Code](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# github-suite

> Claude Code skill suite for GitHub project discovery & source code analysis.

[中文文档](README_CN.md)

## Overview

| Skill | Version | Description |
|-------|---------|-------------|
| `github-finder` | v2.1 | Multi-source bilingual search with adaptive thresholds and search expansion |
| `github-analyzer` | v2.0 | 6-dimension deep source code analysis with evidence-based scoring |

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

### github-finder v2.1

| Feature | Description |
|---------|-------------|
| Term Research | Pre-research brand names, codenames, abbreviations before searching |
| Bilingual Search | 50/50 CN/EN for Chinese input, 30/70 for English input |
| Multi-Angle Query | >=3 angles: direct tool, ecosystem plugin, infra, community, alternative |
| Adaptive Stars | Dynamic thresholds by ecosystem age (mature >1000, growing >200, emerging >50) |
| Search Expansion | README references, GitHub Topics, competitor comparison, citation graph |
| Community Sources | Hacker News, Reddit, V2EX, Zhihu |
| Time Awareness | Current year in queries, annotations for new and stale projects |
| Taxonomy-First | Auto-decompose vague requirements into searchable subcategories |
| Error Recovery | Fallback strategies when searches or fetches fail |
| Parallel Search | Uses Agent tool to parallelize independent search queries |

### github-analyzer v2.0

| Feature | Description |
|---------|-------------|
| 3 Analysis Modes | Deep Research, Quick Overview, Comparative |
| 6-Section Report | Structure, Architecture, Modules, Patterns, Quality, Innovation |
| Evidence-Based Scoring | 6 scorecard dimensions (Style, Error Handling, Tests, Docs, Security, Architecture) with 3-tier rubrics |
| Pattern Detection | Concrete Grep-based detection for creational, structural, behavioral patterns |
| Quality Scorecard | Per-dimension scores with mandatory evidence citations |
| Parallel Analysis | Uses Agent tool to analyze multiple modules concurrently |
| Comparative Matrix | Side-by-side comparison with clear recommendation |
| Report Library | Save analysis reports locally for future reference and retrieval |
| Auto-Cleanup | Removes cloned repos from /tmp after analysis |

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
# Deep research (default mode)
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

- [Claude Code](https://claude.ai/code) (CLI, Desktop, or Web)
- Internet access for GitHub search and web fetching

## Installation

```bash
# Option 1: User-level (available in all projects)
git clone https://github.com/win4r/github-suite.git /tmp/github-suite
cp -r /tmp/github-suite/github-finder ~/.claude/commands/github-finder
cp -r /tmp/github-suite/github-analyzer ~/.claude/commands/github-analyzer
rm -rf /tmp/github-suite

# Option 2: Project-level (only available in that project)
mkdir -p .claude/commands
git clone https://github.com/win4r/github-suite.git /tmp/github-suite
cp -r /tmp/github-suite/github-finder .claude/commands/github-finder
cp -r /tmp/github-suite/github-analyzer .claude/commands/github-analyzer
rm -rf /tmp/github-suite

# Restart Claude Code session to load new skills
```

> **Note**: Each skill is a directory containing a `SKILL.md` file. Place under `~/.claude/commands/` (user-level) or `.claude/commands/` (project-level).

## Version

| Skill | Version | Status |
|-------|---------|--------|
| github-finder | v2.1 | Stable |
| github-analyzer | v2.0 | Stable |

## License

[MIT](LICENSE) - see LICENSE file for details.

## Credits

Built entirely with [Claude Code](https://claude.ai/code) by Anthropic.

Co-authored by Claude Opus 4.6.
