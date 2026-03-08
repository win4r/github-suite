![Built with Claude Code](https://img.shields.io/badge/Built%20with-Claude%20Code-blueviolet)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

# github-suite

> GitHub 项目发现与源码深度分析工具套件，适用于 Claude Code SKILL 框架。

[English](README.md)

## 概览

| SKILL | 版本 | 说明 |
|-------|------|------|
| `github-finder` | v2.0 | 多源多角度搜索，自适应评估，双语支持 |
| `github-analyzer` | v1.0 | 6 维度源码深度分析，质量评估卡 |

## 工作流

```
┌─────────────────┐      链式调用       ┌──────────────────┐
│  github-finder   │ ──────────────────► │  github-analyzer  │
│  （项目发现）     │   可选深度调研触发   │  （源码分析）      │
│                  │                     │                   │
│  • 术语预研      │                     │  • 3 种模式       │
│  • 双语搜索      │                     │  • 6 维度分析     │
│  • 多角度查询    │                     │  • 质量评估卡     │
│  • 自适应星级 ★  │                     │  • 成果报告库     │
└─────────────────┘                      └──────────────────┘
        ▲                                         │
        │              用户请求                     │
        └──────────────────────────────────────────┘
```

## 核心能力

### github-finder v2.0

| 能力 | 说明 |
|------|------|
| 术语预研 | 搜索前识别产品名、代号、缩写 |
| 双语搜索 | 中文输入按 50/50 中英比例，英文输入按 30/70 比例并行查询 |
| 多角度查询 | ≥3 个搜索角度：直接工具、生态插件、基础设施、社区、替代方案 |
| 自适应星级 | 按生态年龄动态调整阈值（成熟 >1000、成长 >200、新兴 >50） |
| 搜索扩展 | README 引用、GitHub Topics、竞品对比、引用图谱 |
| 社区源 | Hacker News、Reddit、V2EX、知乎 |
| 时间感知 | 查询附加年份，🆕 标注新项目，⚠️ 标注停滞项目 |

### github-analyzer v1.0

| 能力 | 说明 |
|------|------|
| 3 种分析模式 | 深度调研、快速概览、对比分析 |
| 6 维度框架 | 结构、架构、模块、模式、质量、创新 |
| 质量评估卡 | 多维度评分可视化 |
| 成果库 | 调研报告存储与引用 |

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
# 深度调研
/github-analyzer https://github.com/user/repo 深度调研

# 快速概览
/github-analyzer https://github.com/user/repo 快速概览

# 对比分析
/github-analyzer 对比 projectA vs projectB

# 指定关注维度
/github-analyzer https://github.com/user/repo 深度调研 关注架构设计和设计模式
```

### 链式调用

```bash
# 发现后深度分析
/github-finder 找一个 AI 代码编辑器，找到后深度分析
```

## 环境要求

- [Claude Code](https://claude.ai/code)，需支持 SKILL 框架
- 可访问互联网（用于 GitHub 搜索和网页抓取）

## 安装

```bash
# 克隆到 SKILL 仓库目录
git clone https://github.com/HeroAshacker/github-suite.git \
  ~/.claude/skill-repository/github-suite

# 激活 SKILL（创建符号链接）
ln -s ~/.claude/skill-repository/github-suite/github-finder \
  ~/.claude/skills/github-finder
ln -s ~/.claude/skill-repository/github-suite/github-analyzer \
  ~/.claude/skills/github-analyzer

# 重启 Claude Code 会话以加载新 SKILL
```

## 版本

| SKILL | 版本 | 状态 |
|-------|------|------|
| github-finder | v2.0 | 稳定 |
| github-analyzer | v1.0 | 稳定 |

## 许可证

[MIT](LICENSE) - 详见 LICENSE 文件。

## 致谢

完全使用 Anthropic 的 [Claude Code](https://claude.ai/code) 构建。

由 Claude Opus 4.6 协作完成。
