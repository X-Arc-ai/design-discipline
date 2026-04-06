---
description: Design anything with the full 5-phase process (Absorb, Ideate, Build, Verify, Present). Works for any medium.
argument-hint: [what to design]
allowed-tools: Read, Write, Edit, Bash, Glob, Grep, Agent
---

# /design

You are executing the full design-discipline process. Follow every phase. No shortcuts.

Load the design skill and all references:
- Skill: `.claude/skills/design-discipline/SKILL.md`
- Guardrails: `.claude/skills/design-discipline/reference/guardrails.md`
- Verification: `.claude/skills/design-discipline/reference/verification.md`
- Design knowledge: `.claude/skills/design-discipline/reference/design-knowledge.md`

**Brief:** $ARGUMENTS

---

## PHASE 1: ABSORB

1. Parse the brief. Identify: what is this, who is it for, what medium, what feeling.

2. **Design system discovery.** Spawn a sub-agent to explore:
   - The project directory for any design files, approved HTML/CSS, branded assets
   - Any existing implementations that have been approved
   - Previous design feedback or preference notes

   ```json
   {
     "subagent_type": "Explore",
     "description": "Discover design system for this project",
     "prompt": "Search the project directory for design-related files. Find: approved HTML/CSS files, design-related markdown, branded assets (logos, banners), any files containing color hex values, font declarations, or spacing patterns. Read the most relevant files and extract: color palette, fonts, spacing patterns, component conventions, border-radius usage, elevation model. Report what you found as a structured design system summary."
   }
   ```

3. If approved work exists: report the discovered design system. If not: propose initial design tokens (spacing scale, type scale, color palette, border radii, shadow levels).

**Present to user:** "Here's what I found / Here's what I propose for the design system. Brief understood as: [summary]. Proceeding to ideation."

---

## PHASE 2: IDEATE

1. Reason through:
   - **Content hierarchy:** What is most important? Secondary? Supporting?
   - **Emotional arc:** What should the viewer feel first, second, third?
   - **Content type:** Narrative, comparative, demonstrative, or informational?
   - **Show > Tell check:** Can I show the actual thing instead of describing it?

2. Generate 2-3 structural approaches. For each:
   - Describe the approach
   - Trace back to first principles: does this serve the content?
   - Note which guardrails it respects

3. Pick direction with rationale. Document WHY.

**Present to user:** "Here are 2-3 approaches. I recommend [X] because [rationale]. Want me to proceed or adjust?"

---

## PHASE 3: BUILD

1. Code with the design system from Phase 1
2. Apply design tokens systematically (no arbitrary values)
3. Build all states (success, error, loading, empty)
4. Handle responsive breakpoints from the start (if web)
5. Check every element against the guardrails -- am I defaulting to any anti-pattern?

**Do NOT present yet.** Go directly to Phase 4.

---

## PHASE 4: VERIFY (Adversarial -- you are attacking your own work)

Full protocol: `reference/verification.md`. Follow it exactly.

**If the output can be rendered in a browser:**

### 4A: Adversarial Critique (BEFORE any fixes)

1. Open via Playwright CLI (`playwright-cli open <url>`)
2. Screenshot at desktop: `playwright-cli resize 1440 900` then `playwright-cli screenshot` -- full page AND scroll to each section for detail shots
3. Screenshot at tablet: `playwright-cli resize 768 1024` then `playwright-cli screenshot`
4. Screenshot at mobile: `playwright-cli resize 375 812` then `playwright-cli screenshot`
5. Run programmatic layout checks via `playwright-cli eval`:
   - Containment: are `max-w-*` containers actually centered? (`getBoundingClientRect().left` > 0?)
   - Overflow: anything breaking out of viewport?
   - Effect visibility: are glass/blur/shadow effects actually rendering?
6. **Write the critique.** For each screenshot, answer: "If a design lead reviewed this, what would they reject?" Be specific and spatial ("card title at x=0, touching viewport edge"), not vague ("alignment seems off").
7. **Intent comparison table.** For each major design element, compare what the brief intended vs what the screenshot shows. Every mismatch is a finding.
8. Grade each finding: CRITICAL / MAJOR / MINOR.

**Do NOT skip the critique. Do NOT go straight to fixing. Write it out first.**

### 4B: Fix Loop

1. Fix all CRITICAL issues, then MAJOR, then MINOR
2. Re-screenshot affected sections
3. Re-run programmatic checks
4. Write a short re-assessment per fix: "Before: [problem]. After: [result]."
5. If fixes introduced new issues, catch them here
6. Repeat until critique comes back clean at all breakpoints
7. Clean up verification screenshots from `.playwright-cli/`

**If non-renderable output:** Same adversarial framing -- write the critique against guardrails.md, do the intent comparison, fix, re-assess.

---

## PHASE 5: PRESENT

1. Show the final output
2. Explain key design decisions and rationale
3. Note which design system tokens were used
4. Flag any trade-offs or decisions that could go either way
5. If the user wants to see screenshots, take fresh ones and keep them (don't clean up requested screenshots)
