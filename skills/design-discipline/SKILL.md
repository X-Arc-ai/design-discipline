---
name: design-discipline
description: Design discipline for AI coding agents. Produces agency-grade visual output across any medium (websites, pitch decks, dashboards, emails, terminal UIs, documentation). Encodes quality guardrails from validated experience, a structured design process, and mandatory visual verification.
user-invocable: false
---

# Design Discipline

This skill produces enterprise/agency-grade design output across ANY medium. It encodes guardrails (what breaks quality), a structured process (how to think about design), and verification (how to check your work).

**The skill is NOT a recipe book.** It doesn't prescribe specific CSS values, grid systems, or component patterns. It sets the QUALITY BAR and prevents the anti-patterns that reliably produce amateur or generic output.

## The 5-Phase Design Process

### Phase 1: ABSORB (Before any code)

Parse the brief:
- What is this? Who is it for? What feeling should it evoke?
- What medium? (website, pitch deck, terminal UI, LinkedIn, dashboard, email, doc)

**Design system discovery:**
- Check if the project has approved design work. Sources to explore:
  - Your project directory for any design-related files, approved HTML/CSS, branded assets
  - Existing approved implementations (HTML/CSS files, pitch decks)
  - Any previous design feedback or notes
- If approved work exists: analyze it to extract the design system (colors, fonts, spacing patterns, component conventions). The approved work IS the reference -- read it, understand the patterns, follow them.
- If no approved work exists: define design tokens FIRST (spacing scale, type scale, color palette, border radii, shadow levels) based on the brief and universal principles.

**Choose layout pattern based on content type** -- not default to cards.

### Phase 2: IDEATE (Think before building)

For a model, "imagining" the output is structural, not visual. Before writing any code, reason through:

- **Content hierarchy:** What is most important? Secondary? Supporting? This ordering drives every layout decision.
- **Emotional arc:** What should the viewer feel first, second, third?
- **Content type:** Is this narrative (prose/story), comparative (tables/side-by-side), demonstrative (show the product), informational (clear hierarchy)? Content type dictates the pattern.
- **Show > Tell check:** Can I show the actual thing instead of describing it?

Generate 2-3 structural approaches. For each, trace back to first principles: does this serve the content? Does it match the audience? Is it the simplest solution that's still premium?

Pick direction with rationale. Document WHY before building.

### Phase 3: BUILD (Code with the design system)

- Apply the project's design tokens systematically (no arbitrary values)
- Every spacing, color, and type choice traces back to the system from Phase 1
- Build all states (not just happy path) -- success, error, loading, empty
- Handle responsive breakpoints from the start (if web)
- Interpret guardrails (see [reference/guardrails.md](reference/guardrails.md)) for the medium at hand

### Phase 4: VERIFY (Adversarial -- attack your own work)

**For any visual output that can be rendered in a browser**, run the adversarial critique loop. This is MANDATORY. The old protocol (screenshot, check boxes, say "pass") produced garbage. The new one forces you to find what's wrong.

Full protocol: [reference/verification.md](reference/verification.md)

**Phase 4A: Adversarial Critique** (BEFORE any fixes)
1. Screenshot at all breakpoints (1440px, 768px, 375px) + section detail shots
2. Run programmatic layout checks via JavaScript evaluation in the browser (containment, overflow, effect visibility)
3. Write a brutal critique: "What would a design lead reject?" Be specific and spatial, not vague.
4. Intent comparison table: for each major design element, what did the brief intend vs what does the screenshot show?
5. Grade each finding: CRITICAL / MAJOR / MINOR

**Phase 4B: Fix Loop**
1. Fix all findings by severity
2. Re-screenshot, re-check, re-assess
3. Repeat until critique comes back clean
4. Clean up verification screenshots
5. THEN present to user

**The key shift:** You are not confirming your work passes. You are actively trying to find reasons it fails. The framing is adversarial, not confirmatory. If you can't find anything wrong, look harder -- the first pass almost always has issues.

**For non-renderable output** (terminal UI mockups, email copy, doc structure): same adversarial framing against the guardrails. Write the critique, do intent comparison, fix, re-assess.

### Phase 5: PRESENT (Only after Phase 4 passes)

- Show the work with rationale for key decisions
- If multiple directions were strong, present options with trade-offs
- Flag any decisions that need input
- If the user explicitly requests screenshots to review, keep those specific ones (don't clean up requested screenshots)

## Show > Tell Hierarchy (For Any Medium)

Always start from the top. Only drop to lower levels when higher ones genuinely don't apply.

1. **Best:** Show the actual product/UX (annotated screenshot, simulated interaction, live embed)
2. **Strong:** Real numbers and metrics (hard data, not promises)
3. **Good:** Concrete examples with before/after
4. **Acceptable:** Feature list with brief context
5. **Weak:** Abstract promises ("we make things better")
6. **Bad:** Decorative illustration with no informational content

## References

All reference paths below are relative to this skill's directory (e.g., `.claude/skills/design-discipline/` after installation).

- **Guardrails (hard rules):** [reference/guardrails.md](reference/guardrails.md)
- **Verification protocol:** [reference/verification.md](reference/verification.md)
- **Design knowledge (ideation reference):** [reference/design-knowledge.md](reference/design-knowledge.md)
