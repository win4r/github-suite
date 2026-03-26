---
name: github-analyzer
# version: 2.0
description: |
  Deep source code analysis for GitHub open-source projects. Multi-dimension analysis
  covering architecture, modules, design patterns, code quality, and innovation.
  Three modes: deep-research, quick-overview, comparative.
  Use when: analyzing GitHub projects, source code research, architecture review, learning from open source.
  Trigger: source analysis, GitHub research, project analysis, code architecture, deep research
allowed-tools: Read, Grep, Glob, Bash, Write, WebFetch, WebSearch, Agent, AskUserQuestion
---

# /github-analyzer - GitHub Source Code Analyzer v2.0

Deep multi-dimension source code analysis for GitHub open-source projects. Generates structured reports with quality scorecards.

## Instructions

### Analysis Modes

| Mode | When to Use | Depth | Output |
|------|------------|-------|--------|
| **deep-research** (default) | Tech selection, architecture learning, pre-fork | Full codebase, 3-pass read | Complete 8-section report + scorecard |
| **quick-overview** | Initial screening, fast evaluation | README + entry points + key modules | Summary report (3 sections) |
| **comparative** | Choosing between similar projects | Key dimensions side-by-side | Comparison matrix + recommendation |

### Workflow

**Step 1: Setup**

1. Confirm project URL and analysis mode (default: deep-research)
2. Clone the project: `git clone --depth 1 <URL> /tmp/github-analyzer-<project-name>`
3. If clone fails, fall back to WebFetch for README and key files via GitHub raw URLs
4. Identify primary language and framework from file extensions and config files

**Step 2: Structure Scan**

1. Run `find /tmp/github-analyzer-<name> -type f | head -200` to get file tree
2. Read key config files in parallel: `package.json` / `go.mod` / `Cargo.toml` / `pyproject.toml` / `pom.xml` etc.
3. Map directory structure -> identify layers (src, lib, cmd, internal, tests, docs, config)
4. List all dependencies and their purposes

**Step 3: Architecture Analysis** (deep-research only)

1. Read entry point files (main.go, index.ts, app.py, etc.)
2. Identify architecture pattern:
   - **Layered**: clear separation of handlers/services/repositories
   - **Microservices**: multiple service directories, inter-service communication
   - **Event-driven**: message queues, event emitters, pub/sub patterns
   - **Plugin**: plugin interface, registry, dynamic loading
   - **Monolith**: single entry point, tightly coupled modules
3. Trace the primary data flow from entry point through core logic to output
4. Use Agent tool to analyze multiple core modules in parallel

**Step 4: Module Deep-Dive** (deep-research only)

For each core module (top 3-5 by importance):
1. Read the module's main files
2. Document: purpose, public API/interface, internal logic, dependencies
3. Identify key algorithms or data structures
4. Note cross-module coupling patterns

**Step 5: Design Pattern Recognition** (deep-research only)

Scan for and document these patterns with file:line references:

| Category | Patterns to Look For | How to Detect |
|----------|---------------------|---------------|
| Creational | Singleton, Factory, Builder | Grep for `getInstance`, `New*`, `Build()`, private constructors |
| Structural | Adapter, Decorator, Facade | Grep for wrapper types, interface adapters, unified API surfaces |
| Behavioral | Strategy, Observer, Command | Grep for interface-typed fields, event listeners, command registries |
| Concurrency | Worker pool, Pipeline, Fan-out | Grep for `chan`, `goroutine`, `Promise.all`, thread pools |

**Step 6: Quality Scoring**

Score each dimension 1-10 using these rubrics:

| Dimension | 8-10 (Excellent) | 5-7 (Good) | 1-4 (Needs Work) |
|-----------|-----------------|------------|------------------|
| **Code Style** | Consistent formatting, linter config present, naming conventions followed | Mostly consistent, minor deviations | Inconsistent style, no linter, mixed conventions |
| **Error Handling** | All external calls wrapped, custom error types, graceful degradation | Most errors handled, some bare panics/throws | Errors swallowed, no error types, crashes on edge cases |
| **Test Coverage** | Test directory exists, unit + integration tests, CI config present | Some test files, basic unit tests | No tests or only trivial tests |
| **Documentation** | README with examples, API docs, inline comments on complex logic | README exists, basic usage docs | No README or minimal single-line README |
| **Security** | Input validation, no hardcoded secrets, dependency scanning | Basic validation, no obvious vulnerabilities | Hardcoded credentials, SQL injection risks, no input validation |
| **Architecture** | Clear separation of concerns, dependency injection, extensible | Reasonable structure, some coupling | God objects, circular dependencies, spaghetti code |

**How to verify scores**:
- Code Style: check for `.eslintrc` / `.prettierrc` / `golangci-lint` config; sample 3 files for consistency
- Error Handling: Grep for `catch`, `if err`, `try`, `rescue` patterns; check ratio of handled vs unhandled
- Test Coverage: count test files vs source files; check for CI config (`.github/workflows/`, `Makefile` test target)
- Documentation: check README length, presence of `/docs` directory, inline comment density
- Security: Grep for hardcoded tokens/passwords, check for `.env.example`, look for input sanitization
- Architecture: check import graph depth, look for circular imports, assess interface usage

**Step 7: Innovation & Highlights**

1. Identify technical innovations or novel approaches
2. Note reusable patterns worth learning from
3. Assess the project's unique value proposition vs alternatives

**Step 8: Report Generation**

Generate the full report (structure below). For deep-research mode, include all 8 sections. For quick-overview, include sections 1, 2, and 8 only.

**Step 9: Save to Report Library (optional)**

If the user wants to save:
1. Create directory: `~/research/github-analysis/` (or user-specified path)
2. Save report as `<project-name>-analysis-<date>.md`
3. This enables future reference when the user asks about previously analyzed projects

### Quality Scorecard Template

```
+--------------------------------------------------+
|           Code Quality Scorecard                  |
+--------------------------------------------------+
| Project: [name]           Date: YYYY-MM-DD        |
+--------------------------------------------------+
| Dimension      | Score | Rating    | Evidence     |
+----------------+-------+-----------+--------------+
| Code Style     | X.X   | ★★★★☆    | [specific]   |
| Error Handling | X.X   | ★★★★     | [specific]   |
| Test Coverage  | X.X   | ★★★☆     | [specific]   |
| Documentation  | X.X   | ★★★★     | [specific]   |
| Security       | X.X   | ★★★★     | [specific]   |
| Architecture   | X.X   | ★★★★☆    | [specific]   |
+----------------+-------+-----------+--------------+
| Overall        | X.X   | ★★★★     | [summary]    |
+--------------------------------------------------+
```

**Rating scale**: 9-10 ★★★★★ | 7-8 ★★★★☆ | 5-6 ★★★☆☆ | 3-4 ★★☆☆☆ | 1-2 ★☆☆☆☆

**Evidence field**: Must cite specific files, patterns, or metrics. No vague assessments.

### Report Structure

```markdown
## Source Code Analysis Report

### 1. Project Overview
- Name, URL, primary language, framework
- Purpose and target audience
- Stars, forks, contributors, last commit date

### 2. Project Structure
- Directory tree (key directories only)
- Tech stack and dependencies
- Build system and toolchain

### 3. Architecture Design (deep-research)
- Architecture pattern identified
- Layer diagram (ASCII)
- Component interaction flow
- Key architectural decisions and trade-offs

### 4. Module Analysis (deep-research)
For each core module:
- Purpose and responsibility
- Public API surface
- Internal implementation highlights
- Dependencies and coupling

### 5. Design Patterns (deep-research)
- Patterns identified with file:line references
- Quality of pattern implementation
- Patterns that could improve the codebase

### 6. Code Quality (deep-research)
- Quality Scorecard (see template above)
- Per-dimension evidence and analysis

### 7. Innovation & Highlights (deep-research)
- Technical innovations
- Reusable patterns
- Learning value

### 8. Summary & Recommendations
- Overall assessment
- Strengths (top 3)
- Weaknesses (top 3)
- Recommendations for users/contributors
```

### Comparative Mode

When comparing projects (e.g., "compare A vs B"):

1. Run quick-overview on each project (in parallel using Agent tool)
2. Build comparison matrix:

```markdown
| Dimension | Project A | Project B |
|-----------|----------|----------|
| Language  | Go       | Rust     |
| Stars     | 5.2k     | 3.8k    |
| Architecture | Layered | Plugin |
| Test Coverage | 8/10 | 6/10  |
| Documentation | 7/10 | 9/10  |
| Last Updated | 2026-03 | 2026-03 |
| Unique Strength | Performance | Extensibility |
```

3. Provide clear recommendation with reasoning

### Error Handling

- **Clone fails**: Fall back to WebFetch for README + key files via `raw.githubusercontent.com`
- **Large repo (>10k files)**: Focus on `src/` or `lib/` directories only, skip vendor/node_modules
- **Binary/compiled project**: Focus on build config, README, and any source directories
- **Private repo**: Inform user that analysis requires public access or local clone

### Cleanup

After analysis is complete, remove the cloned directory:
```bash
rm -rf /tmp/github-analyzer-<project-name>
```

## Examples

**Deep research**: `/github-analyzer https://github.com/user/repo deep-research`
-> Clone -> 3-pass analysis -> full 8-section report + scorecard -> optional save

**Quick overview**: `/github-analyzer https://github.com/user/repo quick-overview`
-> Clone -> structure scan + README -> sections 1, 2, 8 only -> fast summary

**Comparative**: `/github-analyzer compare projectA vs projectB`
-> Parallel quick-overview on both -> comparison matrix -> recommendation

**Focused dimensions**: `/github-analyzer https://github.com/user/repo deep-research focus on architecture and design patterns`
-> Full clone but emphasize sections 3 and 5 with extra depth

## Quick Reference

| Parameter | Value |
|-----------|-------|
| Modes | deep-research (default) / quick-overview / comparative |
| Dimensions | Structure, Architecture, Modules, Patterns, Quality, Innovation |
| Scoring | 1-10 per dimension with evidence-based rubrics |
| Output | Markdown report + quality scorecard |
| Storage | Optional, default `~/research/github-analysis/` |
| Cleanup | Auto-remove cloned repos from /tmp after analysis |

## Related Skills

- **github-finder**: Project discovery (upstream). Finder discovers projects, then chain-calls this skill for deep analysis.
