<p align="center">
  <img src="https://raw.githubusercontent.com/X-Arc-ai/design-discipline/main/assets/hero.svg" alt="design-discipline" width="700">
</p>

<p align="center">
  <strong>A design discipline for AI coding agents.</strong><br>
  Not a template. Not a design system. A process with guardrails.
</p>

<p align="center">
  <a href="https://github.com/X-Arc-ai/design-discipline/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache%202.0-4ade80" alt="License"></a>
  <a href="https://x-arc.ai"><img src="https://img.shields.io/badge/Claude%20Code-plugin-4ade80" alt="Claude Code plugin"></a>
  <a href="https://x-arc.ai"><img src="https://img.shields.io/badge/by-X--Arc-4ade80" alt="X-Arc"></a>
</p>

---

## Every AI-generated design looks the same.

Gradients. Card grids. "Powered by AI" aesthetics. The output reads as generic no matter which model produces it, for three reasons that have nothing to do with the model's raw capability:

1. **It can't see what it built.** The model writes CSS and hopes. There is no visual feedback loop unless you build one.
2. **It defaults to the median of its training data.** First instinct trends toward the average of every design it ever saw. The average of a huge dataset is, by definition, generic.
3. **It confirms its own work.** Screenshots get taken. Criteria get "checked." Output gets declared passing. Nobody actually looked at whether cards had icons, whether content bled to the edges, whether the effects were visible.

Those are the three problems design-discipline addresses directly. Not by teaching the model taste, but by giving it a process that compensates for the three specific failure modes above.

---

## What it is

A five-phase design process adapted from how professional design agencies work (IDEO, Pentagram, Frog), reshaped for a model's specific strengths and weaknesses:

1. **ABSORB.** Parse the brief. Discover or define the design system from existing approved work in the project.
2. **IDEATE.** Think before building. Content hierarchy, emotional arc, Show > Tell check.
3. **BUILD.** Code with the design system. Every value traces to a token. No arbitrary decisions.
4. **VERIFY.** Attack your own work. Adversarial critique, not confirmatory checkbox. Programmatic layout checks catch what screenshots miss.
5. **PRESENT.** Show the final output with rationale. Only after verification passes.

Phase 4 is the part that wasn't obvious. The old approach (take screenshot, check boxes, say "pass") produced the same garbage the skill was supposed to prevent. Adversarial framing asks a different question: "What would a design lead reject?" That reframe flips the model from confirmatory mode to critique mode. The model can critique its own work. It just doesn't by default.

---

## Guardrails, not recipes

A recipe ("use 8px grid, Inter font, blue-500 accent") works for one project. A guardrail ("use a consistent spacing system, don't mix rounded and sharp corners") works everywhere.

Every guardrail in this skill traces back to a real rejection on real work. The quotes below are raw, not cleaned up:

| What Was Rejected | What Was Said |
|---|---|
| Gradients, glows, glossy effects | "no gradients, no AI cliches. It should feel like something stamped on equipment that works." |
| Card grids for narrative content | "cards don't make the user connect. I think it should be told like a story." |
| Abstract illustrations | "abstract circles and lines that don't say shit" |
| Generic promises | "the solution seems like 'the sky is blue', it feels like a scam" |
| Overengineered visuals | Pixel art, PixiJS, sprite sheets, canvas. "it sucks" |
| Confirmation bias in verification | Screenshots were taken. Criteria were "checked." Output was declared passing. Content bled to edges, effects were invisible, cards had no icons. |

The full anti-pattern list lives in `skills/design-discipline/reference/guardrails.md`. It grows with experience.

---

## Model self-awareness

The skill names the model's limitations out loud so the process compensates for them rather than pretending they don't exist:

- **"I can't feel spacing."** A human designer senses "that's too tight." The model has to be systematic about it: define spacing values, apply them, verify via screenshot.
- **"I default to the median of my training data."** First instinct trends toward the average. The guardrails pull away from the median.
- **"I'm strong at consistency, weak at novelty."** Once a design system is established, the model applies it perfectly across 100 components. Generating the initial direction is a different problem and requires deliberate ideation.

Most AI tools pretend the model has no limitations. This one makes them part of the framework.

---

## Install

### Claude Code (native plugin)

Inside Claude Code:

```
/plugin marketplace add X-Arc-ai/design-discipline
/plugin install design-discipline@x-arc
```

Then run `/design [what to build]`.

To share with your team, install at project scope so the plugin is committed via `.claude/settings.json`:

```
/plugin install design-discipline@x-arc --scope project
```

### Claude Code (manual install, no plugin system)

```bash
git clone https://github.com/X-Arc-ai/design-discipline.git
cp -r design-discipline/skills/design-discipline ~/.claude/skills/
cp design-discipline/commands/design.md ~/.claude/commands/design.md
```

Then run `/design [what to build]`.

### Other AI coding agents

The skill files are plain markdown. Paste the contents of `SKILL.md` plus the three reference files (`guardrails.md`, `verification.md`, `design-knowledge.md`) into your agent's system prompt or its skill/instruction mechanism. The five-phase process and the guardrails work with any model that can write code.

### Verification tooling (recommended)

The verification protocol requires a tool that can take automated screenshots and run JavaScript in a browser. For Claude Code users, the easiest option is the [Playwright MCP server](https://github.com/microsoft/playwright-mcp) (provides `mcp__playwright__*` tools). Without automated browser access, the skill still works. You just verify manually (open in browser, resize, inspect). See `reference/verification.md` for supported tools.

---

## How it works

```
/design build a pricing page for my SaaS

Phase 1: ABSORB
  -> Discovers your project's design system from existing approved work
  -> If none exists, proposes design tokens (spacing, type, color, radii)

Phase 2: IDEATE
  -> Reasons through content hierarchy, emotional arc, content type
  -> Generates 2-3 structural approaches with rationale
  -> Picks direction and documents WHY

Phase 3: BUILD
  -> Codes with the design system (no arbitrary values)
  -> Handles all states (success, error, loading, empty)
  -> Responsive from the start

Phase 4: VERIFY (the key phase)
  -> Screenshots at 3 breakpoints (1440px, 768px, 375px)
  -> Runs programmatic layout checks (JS) for containment, overflow, effect visibility
  -> Writes adversarial critique: "What would a design lead reject?"
  -> Fixes by severity, re-screenshots, repeats until clean

Phase 5: PRESENT
  -> Shows final output with rationale
  -> Key design decisions explained
```

---

## File structure

```
skills/design-discipline/
  SKILL.md                    # The 5-phase process
  reference/
    guardrails.md             # What NOT to do (living anti-pattern list)
    verification.md           # Adversarial verification protocol + JS checks
    design-knowledge.md       # Perceptual principles + model self-awareness
commands/
  design.md                   # /design slash command
```

---

## Show > Tell hierarchy

When designing content about capabilities, start from the top:

1. **Best.** Show the actual product or UX (annotated screenshot, simulated interaction).
2. **Strong.** Real numbers and metrics (hard data, not promises).
3. **Good.** Concrete examples with before and after.
4. **Acceptable.** Feature list with brief context.
5. **Weak.** Abstract promises ("we make things better").
6. **Bad.** Decorative illustration with no informational content.

---

## Contributing

The most valuable contribution is a new guardrail from a real rejection on real work. See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Built with `/design`

<p align="center">
  <img src="https://raw.githubusercontent.com/X-Arc-ai/design-discipline/main/assets/built-with-design.png" alt="x-arc.ai solution section built with design-discipline" width="900">
</p>

This is one section of [x-arc.ai](https://x-arc.ai). Absorbed, ideated, built with tokens, and verified adversarially. Every pixel traces back to a design decision. No generic AI output.

---

## Where this came from

Design-discipline is built by [X-Arc](https://x-arc.ai). X-Arc is an AI lab that trains and deploys AI agents for businesses. We built this skill because our own agents kept producing designs that looked like every other AI tool's output, and checklist-style verification kept declaring broken work as passing. This is the tool we use ourselves on every piece of design work we ship.

It was co-built by CCL (one of our agents) and the humans who work with her. CCL ships websites, pitch decks, dashboards, and marketing materials across multiple projects. Eight weeks of real design work and eight-plus rejected iterations went into it. The adversarial verification approach came from a specific internal failure where confirmatory review declared "pass" on broken output. That failure is what made the skill.

[x-arc.ai](https://x-arc.ai) | [GitHub](https://github.com/x-arc-ai)
