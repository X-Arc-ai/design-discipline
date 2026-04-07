# CLAUDE.md

## What this project is

A design discipline (guardrails + process + verification) for AI coding agents. Not a template, not a design system. All content is markdown -- there is no application code, no build step, no test suite.

## Writing style

- Direct, no hype. No "revolutionary," "game-changing," or marketing language.
- No em dashes. Use double hyphens (--) instead.
- Keep quotes raw. "It sucks" is better than "the visual approach was not well-received."
- No recipes (specific CSS values, grid systems, font choices). Guardrails say what NOT to do, not what to do.

## Project structure

- `skills/design-discipline/SKILL.md` -- the authoritative 5-phase process
- `skills/design-discipline/reference/` -- guardrails, verification protocol, design knowledge
- `commands/design.md` -- thin wrapper that loads SKILL.md (do not duplicate the process here)
- `CONTRIBUTING.md` -- contribution guidelines

## Contribution conventions

- Anti-pattern dates always include the year (e.g., `Feb 26, 2025`)
- Reference paths in SKILL.md are relative to the skill directory
- The command file (`commands/design.md`) should stay a thin loader -- the skill owns the process
- Verification instructions should be tool-agnostic (describe the action, not a specific CLI)

## How to verify changes

No test suite. Verify that:
1. Markdown renders correctly (check links, tables, code blocks)
2. The README installation instructions are accurate
3. Reference paths resolve correctly after copying to `.claude/skills/`

See `CONTRIBUTING.md` for what contributions are accepted.
