---
name: github-optimizer
# version: 1.0
description: |
  Multi-round iterative optimizer for open-source projects. Performs deep analysis,
  classifies issues by severity, plans and executes multi-round improvements,
  runs code review between rounds, and verifies cross-file consistency.
  Transforms any project from current state to production-quality through
  structured iteration with quality gates.
  Use when: optimizing open-source projects, improving code quality, refactoring,
  iterating to best practices, polishing projects before release.
  Trigger: optimize project, iterate to optimal, improve quality, polish project,
  refactor project, multi-round improvement
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, WebFetch, WebSearch, Agent, AskUserQuestion, Skill, TaskCreate, TaskUpdate
---

# /github-optimizer - Open-Source Project Multi-Round Optimizer v1.0

Structured methodology for iterating any open-source project to optimal quality through deep analysis, severity-based prioritization, and multi-round improvement with quality gates.

## Instructions

### Core Principle

**Severity-Driven Iteration**: Fix the most impactful issues first. Each round targets one severity tier. Never mix severity levels in a single round — this prevents regression and keeps changes reviewable.

### Phase 1: Deep Reconnaissance (DO NOT skip)

Before touching any code, build a complete mental model of the project.

**Step 1.1: Clone & Inventory**

```bash
# If remote URL provided
git clone --depth 50 <URL> /tmp/github-optimizer-<project>
# --depth 50 gives enough history for context without full clone
```

- Run `find . -type f -not -path './.git/*' | head -300` for full file tree
- Count lines: `find . -type f -name '*.md' -o -name '*.ts' -o -name '*.py' ... | xargs wc -l`
- Check git history: `git log --oneline -20` for project trajectory
- Read ALL non-binary files (use Agent tool for parallel reads if >10 files)

**Step 1.2: Structural Understanding**

Read and internalize in this order:
1. README / documentation — understand what the project claims to do
2. Config files (package.json, go.mod, pyproject.toml, etc.) — tech stack and dependencies
3. Entry points (main.*, index.*, app.*) — how it starts
4. Core source files — what it actually does
5. Tests — what's validated
6. CI/CD config (.github/workflows, Makefile) — what's automated

**Step 1.3: Issue Identification**

Systematically scan for issues across these categories:

| Category | What to Look For |
|----------|-----------------|
| **Correctness** | Bugs, logic errors, broken references, wrong paths/URLs, missing imports |
| **Completeness** | Missing error handling, missing tests, incomplete docs, missing configs |
| **Consistency** | Naming mismatches across files, version number drift, style inconsistencies |
| **Performance** | Unnecessary complexity, N+1 patterns, missing caching, oversized bundles |
| **Security** | Hardcoded secrets, missing input validation, outdated dependencies, injection risks |
| **Usability** | Unclear README, missing examples, wrong installation instructions, poor CLI UX |
| **Architecture** | Tight coupling, circular dependencies, god objects, missing abstractions |
| **Maintainability** | No CLAUDE.md/CONTRIBUTING.md, unclear project structure, missing linter config |

**Step 1.4: Severity Classification**

Classify every issue into exactly one severity tier:

| Severity | Definition | Examples |
|----------|-----------|---------|
| **Critical** | Project doesn't work, data loss risk, security vulnerability | Missing tool permissions that block core functionality, broken entry point, hardcoded credentials |
| **High** | Major quality/usability problem, significant waste | 50%+ code duplication, wrong installation instructions, missing error handling on critical paths |
| **Medium** | Noticeable quality gap, inconsistency | Naming mismatches, missing tests for edge cases, vague documentation |
| **Low** | Polish item, minor inconsistency | Missing file in structure diagram, minor style issues, optional config |

Output a numbered issue table:

```markdown
| # | Severity | Issue | Files Affected |
|---|----------|-------|----------------|
| 1 | Critical | ... | file1, file2 |
| 2 | Critical | ... | file3 |
| 3 | High | ... | file1, file4 |
...
```

### Phase 2: Iteration Planning

**Step 2.1: Create Round Plan**

Group issues into rounds by severity. Each round = one severity tier:

| Round | Focus | Quality Gate |
|-------|-------|-------------|
| Round 1 | All Critical issues | Project functions correctly after this round |
| Round 2 | All High issues | No major quality gaps remain |
| Round 3 | All Medium issues | Cross-file consistency achieved |
| Round 4 | All Low issues | Polish complete |
| Round 5 | Final review | Independent code review passes with zero findings |

**Adaptive rounds**: If a severity tier has 0 issues, skip that round. If a round creates new issues (discovered during implementation), add them to the appropriate severity tier and address in the correct round.

**Step 2.2: Create Task Tracker**

Use TaskCreate to create one task per round. This gives the user visibility into progress.

### Phase 3: Iterative Execution

For **each round**, follow this cycle:

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐     ┌─────────────┐
│  Implement   │ ──► │  Self-Check  │ ──► │  Verify No   │ ──► │  Mark Round │
│  All Fixes   │     │  Each Fix    │     │  Regression  │     │  Complete   │
│  in Round    │     │  Works       │     │  Introduced  │     │             │
└─────────────┘     └──────────────┘     └──────────────┘     └─────────────┘
```

**3.1 Implementation Rules**

- Fix all issues in the current severity tier, working through them in order
- For each fix:
  - Read the affected file(s) BEFORE editing (never edit blind)
  - Make the minimum change needed — do not scope-creep
  - If a fix requires changes across multiple files, make them all atomically
- Use Agent tool to parallelize independent fixes within the same round
- Keep a mental diff of what changed — you'll need it for self-check

**3.2 Self-Check After Each Round**

After completing a round, verify:
- [ ] Every issue in this severity tier is addressed
- [ ] No files were left in an inconsistent state
- [ ] Changes don't break functionality addressed in prior rounds
- [ ] If tests exist, they still pass: `npm test` / `go test ./...` / `pytest` / etc.

**3.3 Regression Check**

For any file modified in this round, re-read it fully and verify:
- No accidental deletions of working code
- No introduced typos or syntax errors
- Cross-references to/from this file still valid

### Phase 4: Final Review (Round 5)

This round is **review-only** — no implementation unless the review finds issues.

**Step 4.1: Cross-File Consistency Audit**

Use Agent tool (subagent_type: "superpowers:code-reviewer" if available) to verify:

| Check | How |
|-------|-----|
| Version numbers | All files referencing version must match |
| Naming | Same concept must use same name everywhere |
| URLs/paths | All references must resolve correctly |
| Feature claims | README features must match actual implementation |
| Config completeness | All referenced tools/dependencies actually available |
| Documentation accuracy | Examples must be valid, installation must work |

**Step 4.2: Before/After Summary**

Generate a comparison table showing what improved:

```markdown
| Metric | Before | After | Delta |
|--------|--------|-------|-------|
| [relevant metric] | X | Y | improvement |
```

Include both quantitative (line counts, issue counts) and qualitative (capability descriptions) metrics.

### Phase 5: Ship

**Step 5.1: Commit**

Create a single well-structured commit with:
- Subject line: `refactor: [concise description of optimization]`
- Body: bullet points for each round's changes
- Co-author trailer

**Step 5.2: Push** (only if user confirms)

Never auto-push. Always ask:
> "All rounds complete. Ready to push to origin/main?"

### Error Handling

| Situation | Action |
|-----------|--------|
| Project too large (>500 files) | Focus on core src/ directory, skip vendor/generated |
| No tests exist | Note as High issue, suggest test framework but don't block other rounds |
| Can't clone (private repo) | Ask user for local path or access token |
| Issue discovered mid-round from wrong tier | Log it, address in correct round, don't mix severity |
| Fix in round N breaks something from round N-1 | Stop, revert the breaking change, find alternative approach |
| User disagrees with severity classification | Adjust immediately — user classification overrides |

### Optimization Patterns (Learned Heuristics)

Common patterns that recur across projects — check for these proactively:

| Pattern | Signal | Fix |
|---------|--------|-----|
| **Bloated config/docs** | File >250 lines with repeated sections | Consolidate, eliminate duplication |
| **Missing tool permissions** | Config says "allowed: X" but instructions use Y | Add missing tools to permissions |
| **Stale references** | Wrong URLs, old usernames, deprecated paths | Update to current values |
| **Template without substance** | Scoring rubric with "X.X" placeholders | Fill with concrete criteria and examples |
| **Vague instructions** | "Identify patterns" without HOW | Add detection methods (grep patterns, file signals) |
| **Inconsistent naming** | Same concept called 3 different names | Pick one, apply everywhere |
| **Missing error handling** | Happy path only, no fallback | Add degradation strategy for each failure mode |
| **No cleanup** | Temp files/clones left behind | Add cleanup step at end of workflow |

## Examples

**Skill project**: `/github-optimizer https://github.com/user/my-skills`
-> Found: missing allowed-tools (Critical), 50% duplication (High), wrong install path (High), version drift (Medium)
-> R1: fix tools -> R2: rewrite + fix path -> R3: align versions -> R4: polish -> R5: review

**Web app**: `/github-optimizer https://github.com/user/my-app`
-> Found: broken Docker (Critical), no error boundaries (High), no tests (Medium), stale README (Low)
-> R1: fix Docker -> R2: add error handling -> R3: add tests -> R4: update docs -> R5: review

**Library/SDK**: `/github-optimizer /path/to/local/sdk`
-> Found: circular deps (Critical), missing type exports (High), no JSDoc (Medium), no changelog (Low)
-> R1: break cycles -> R2: fix exports -> R3: add JSDoc -> R4: add changelog -> R5: review

## Quick Reference

| Parameter | Value |
|-----------|-------|
| Phases | 5 (Recon -> Plan -> Execute -> Review -> Ship) |
| Rounds | Up to 5 (one per severity tier + final review) |
| Severity tiers | Critical > High > Medium > Low |
| Core principle | Fix most impactful issues first, never mix severity |
| Quality gate | Each round must pass self-check before next round starts |
| Parallelization | Use Agent tool for independent file reads and fixes |
| Commit strategy | Single commit covering all rounds, detailed body |

## Related Skills

- **github-analyzer**: Deep source code analysis. Use as input to optimizer for comprehensive initial assessment.
- **github-finder**: Project discovery. Find projects to optimize.
