---
name: github-finder
# version: 2.1
description: |
  GitHub project discovery with bilingual multi-source search and adaptive scoring.
  Searches GitHub for open-source projects matching user requirements with multi-angle
  queries, adaptive star thresholds, community source validation, and search expansion.
  Can chain-call github-analyzer for deep analysis.
  Use when: finding open-source projects, tech selection, searching GitHub, comparing solutions.
  Trigger: find project, search GitHub, open-source selection, discover repos
allowed-tools: WebSearch, WebFetch, Agent, AskUserQuestion, Skill
---

# /github-finder - GitHub Project Discovery v2.1

Multi-source bilingual search for GitHub open-source projects with adaptive scoring. Chain-calls github-analyzer for deep analysis.

## Instructions

### Workflow

**Step 0: Term Research** (skip if no proper nouns detected)

If the user input contains potential product names, codenames, or abbreviations:
1. WebSearch "[term] what is" / "[term] 是什么" to resolve ambiguity
2. Build keyword list: exact name + generic terms + synonyms
3. Example: "Antigravity" → Google OAuth codename → keywords: ["antigravity auth", "gemini api proxy"]

**Step 1: Requirement Analysis & Search Planning**

1. **Parse requirements**: functionality, tech stack, use case
2. **Bilingual keywords**: detect input language, generate both CN/EN queries

| Input Language | CN Queries | EN Queries | Extra Sources |
|---------------|-----------|-----------|---------------|
| Chinese | 50% | 50% | CSDN, Zhihu, V2EX |
| English | 30% | 70% | — |
| Mixed | 40% | 60% | By content |

3. **Plan search angles** (must cover **>=3**):
   - Direct tool: `X tool/library site:github.com`
   - Ecosystem plugin: `X plugin/extension for [platform]`
   - Infrastructure: `X gateway/proxy/balancer`
   - Community curated: `awesome-X` / `best X [current year]`
   - Alternative: `alternative to [known project]`

4. **Taxonomy-first** (activate when: vague requirements OR first-round results < 3):
   - Decompose into 3-5 solution subcategories, search each independently
   - Example: "unify AI APIs" -> {API gateway, load balancer, key management, usage monitor, SDK wrapper}

5. **Set adaptive star threshold** based on ecosystem age:

| Ecosystem Age | Threshold | How to Judge |
|--------------|-----------|-------------|
| Mature (>3yr) | stars:>1000 | First related project created >3yr ago |
| Growing (1-3yr) | stars:>200 | First related project created 1-3yr ago |
| Emerging (<1yr) | stars:>50 | First related project created <1yr ago |
| Always | No floor | Keep 1-2 low-star but highly relevant projects |

**Step 2: Multi-Source Search** (target: 8-15 candidates)

Execute searches in parallel where possible using the Agent tool:

1. **GitHub search**: >=3 angles x bilingual = 6+ queries with `site:github.com`
2. **Community sources** (1-2 queries each, extract mentioned project names only):
   - Hacker News: `[keyword] site:news.ycombinator.com`
   - Reddit: `[keyword] site:reddit.com r/programming OR r/opensource`
   - V2EX (for CN): `[keyword] site:v2ex.com`
3. **Time awareness**: append current year to queries; mark projects accordingly

**Step 2.5: Search Expansion** (on top results)

1. **README references**: WebFetch TOP 3 project READMEs, extract "See also" / "Alternatives" / "Related" sections and GitHub links -> mark discovered projects with tag
2. **GitHub Topics**: extract topic tags from TOP projects, browse `site:github.com/topics/[tag]` for 2-3 relevant topics
3. **Competitor comparison** (TOP 1 only): search "[project] vs" and "alternative to [project]"
4. **Citation graph** (only if candidates < 5): check TOP 1 author's other repos, "Used by" dependents

**Error handling**: If WebFetch fails for a URL, try WebSearch for the project name + README instead. If a community source returns nothing, skip it and note in the report.

**Step 3: Filter & Score**

Score each candidate using:

| Metric | Weight | Criteria |
|--------|--------|----------|
| Feature match | 30% | Core features meet requirements |
| Stars | 15% | Adaptive threshold (not absolute) |
| Activity | 20% | Commits within last 3 months |
| Documentation | 15% | README complete with examples |
| Community | 10% | Active issues, multiple contributors |
| Discovery source | 10% | Multi-source bonus (see below) |

Discovery source bonus: community mention +3, README reference +3, Topics discovery +2, competitor comparison +2 (max 10)

**Annotations**: new (<6mo) projects with fresh tag, unmaintained (>1yr) with warning tag, README-referenced with clip tag, community-sourced with megaphone tag

Filter to TOP 5-8 candidates with WebFetch for each README.

**Step 4: Quick Evaluation & Ranking**

For each candidate: read README, assess requirement match, note discovery channel, rank.

**Step 5: Deep Analysis (optional)**

If user requests deep analysis or says "then analyze":
- Use Skill tool: `Skill(skill="github-analyzer", args="<project URL> deep-research")`
- Integrate analysis results into the report

### Output Format

```markdown
## GitHub Project Discovery Report

### Requirements
[Original user request]

### Term Research
- Identified: [term] -> [actual meaning]
- Keywords: [exact, generic, synonyms]

### Search Strategy
- Bilingual keywords: [CN] / [EN]
- Search angles: [angle1, angle2, angle3, ...]
- Star threshold: [adaptive threshold] (ecosystem age: [X years])

### Recommended Projects

#### 1. [Project Name](URL) - Stars count [annotations]
- **Purpose**: One-line description
- **Tech stack**: Go / Python / ...
- **Last updated**: YYYY-MM-DD
- **Match score**: X/5
- **Discovery**: GitHub search / Community / README reference / Topics / Competitor
- **Why**: [recommendation reason]
- **Caveats**: [potential limitations]

#### 2. ... [new project annotation] (emerging)
#### 3. ... [warning annotation] (maintenance risk)

### Expansion Discoveries
- Via README references: [projects]
- Via Topics browsing: [projects]
- Via competitor comparison: [projects]
- Via community discussions: [projects]

### Recommendation
Based on analysis, recommend **[project]** because: ...

### Coverage Checklist
- [x] Term research
- [x] Bilingual search
- [x] >=3 search angles
- [x] Community sources
- [x] README expansion
- [x] Topics browsing
- [ ] Competitor comparison (TOP 1)
- [ ] Citation graph (only when needed)

### Next Steps
- [ ] Deep analysis with /github-analyzer?
```

## Examples

**Basic search**: `/github-finder I need a Go CLI framework`
-> Term research: skip (common term) -> Mature ecosystem -> stars:>1000 -> 3 angles -> README expansion discovers urfave/cli, kong from cobra's README

**Bilingual tech selection**: `/github-finder Find an open-source Notion alternative`
-> "Notion" = product name confirmed -> bilingual search -> HN/Reddit community sources -> README cross-references Logseq, Joplin, AppFlowy

**Emerging ecosystem**: `/github-finder Open-source projects using Gemini API`
-> Growing ecosystem -> stars:>200 + keep low-star gems -> time-aware "2026" queries -> community sources (V2EX/Reddit)

**Complex (taxonomy-first)**: `/github-finder I want to unify multiple AI API providers`
-> Vague requirement -> 5 subcategories -> each searched independently -> grouped recommendations

**Chain call**: `/github-finder Find an AI code editor, then deep-analyze the best match`
-> Full discovery -> recommend top match -> Skill call to github-analyzer -> integrated report

## Quick Reference

| Parameter | Value |
|-----------|-------|
| Search angles | >=3 (tool / plugin / infra / curated / alternative) |
| Bilingual ratio | CN input 50:50, EN input 30:70, mixed 40:60 |
| Star threshold | Mature >1000, Growing >200, Emerging >50, always keep low-star gems |
| Candidate count | 8-15 initial -> TOP 5-8 final |
| Deep analysis | Optional, chain-calls `/github-analyzer` |

## Related Skills

- **github-analyzer**: Deep source code analysis (downstream). Chain-call after discovery for 6-dimension analysis.
- **github-optimizer**: Multi-round project optimization. Use after discovery to iteratively improve a project to production quality.
