# CLAUDE.md - github-suite

## Project Structure

```
github-suite/
├── github-finder/SKILL.md    # Project discovery skill (v2.1)
├── github-analyzer/SKILL.md  # Source code analysis skill (v2.0)
├── github-optimizer/SKILL.md # Multi-round project optimizer (v1.0)
├── README.md                 # English documentation
├── README_CN.md              # Chinese documentation
├── CLAUDE.md                 # This file
├── LICENSE                   # MIT license
└── .gitignore
```

## Development Rules

- Each skill is a single `SKILL.md` file inside its named directory
- Skills must have valid YAML frontmatter with: name, description, allowed-tools
- Keep skill files under 250 lines to minimize context consumption when loaded
- All skill instructions must be actionable (HOW to do, not just WHAT to do)
- Quality scoring must require evidence (file:line references), never vague assessments
- Version numbers are tracked in frontmatter comments and README tables — keep in sync
- README.md and README_CN.md must stay in sync for features, versions, and installation

## Testing a Skill

To test locally: copy the skill directory to `~/.claude/commands/` and restart Claude Code. Then invoke with `/github-finder <query>`, `/github-analyzer <url>`, or `/github-optimizer <url-or-path>`.
