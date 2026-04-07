---
description: Design anything with the full 5-phase process (Absorb, Ideate, Build, Verify, Present). Works for any medium.
argument-hint: [what to design]
allowed-tools: Read, Write, Edit, Bash, Glob, Grep, Agent
---

# /design

You are executing the full design-discipline process. Follow every phase. No shortcuts.

**Read these files now** (they define the entire process):
- Skill: `.claude/skills/design-discipline/SKILL.md`
- Guardrails: `.claude/skills/design-discipline/reference/guardrails.md`
- Verification: `.claude/skills/design-discipline/reference/verification.md`
- Design knowledge: `.claude/skills/design-discipline/reference/design-knowledge.md`

Follow the 5-phase process defined in SKILL.md exactly.

**Brief:** $ARGUMENTS

---

## Additional: Design System Discovery Sub-Agent

During Phase 1 (ABSORB), spawn this sub-agent to discover the project's existing design system:

```json
{
  "subagent_type": "Explore",
  "description": "Discover design system for this project",
  "prompt": "Search the project directory for design-related files. Find: approved HTML/CSS files, design-related markdown, branded assets (logos, banners), any files containing color hex values, font declarations, or spacing patterns. Read the most relevant files and extract: color palette, fonts, spacing patterns, component conventions, border-radius usage, elevation model. Report what you found as a structured design system summary."
}
```
