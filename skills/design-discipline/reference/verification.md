# Visual Verification Protocol

This protocol compensates for the model's inability to see rendered output natively. It is MANDATORY for any design output that can be rendered in a browser.

**Core principle:** You are not CHECKING your work. You are ATTACKING it. The question is never "does this pass?" -- it's "what would get this rejected?"

## Phase 4A: Adversarial Critique

After building, BEFORE any fixes:

```
1. Open the output in a browser (navigate to the URL)
2. Screenshot at desktop (1440px) -- full page + individual sections
3. Screenshot at tablet (768px) -- full page
4. Screenshot at mobile (375px) -- full page
5. Run programmatic layout checks (see below)
6. Write the CRITIQUE (see below)
7. Do NOT skip to fixing. Write the full critique first.
```

### The Critique

For EACH screenshot, write a brutal assessment answering:

**"If a design lead reviewed this, what would they reject and why?"**

Rules for the critique:
- **Be specific and spatial.** Not "alignment is off" but "the left card title starts at the viewport edge with 0px margin -- containment is broken."
- **Be visual, not structural.** Don't check if the HTML is correct. Describe what you SEE in the screenshot. Is the glass effect actually visible or just theoretically present? Are the cards visually distinct from the background or do they blend in?
- **Compare intent vs reality.** For each major design element, state what the brief/design system intended and what the screenshot actually shows. "Brief specifies liquid glass with visible glassmorphic elements. Screenshot shows flat dark rectangles with no visible glass effect."
- **Grade severity.** Tag each issue as CRITICAL (fundamentally broken), MAJOR (clearly wrong), or MINOR (polish).

### Programmatic Layout Checks

Certain issues are invisible to screenshot analysis but trivially caught with JS. Run these ALWAYS:

```javascript
// 1. Containment check -- are max-width containers actually centered?
() => {
  const containers = document.querySelectorAll('[class*="max-w"]');
  return [...containers].map(el => {
    const rect = el.getBoundingClientRect();
    const style = getComputedStyle(el);
    return {
      class: el.className.match(/max-w-\S+/)?.[0],
      left: Math.round(rect.left),
      marginLeft: style.marginLeft,
      parentWidth: Math.round(el.parentElement?.getBoundingClientRect().width)
    };
  }).filter(c => c.left < 20 && c.parentWidth > 1200); // flag edge-hugging containers
}

// 2. Overflow check -- anything breaking out of viewport?
() => {
  const all = document.querySelectorAll('*');
  const vw = window.innerWidth;
  return [...all].filter(el => {
    const rect = el.getBoundingClientRect();
    return rect.right > vw + 5 || rect.left < -5;
  }).map(el => el.tagName + '.' + el.className.split(' ')[0]).slice(0, 10);
}

// 3. Visibility check -- are "glass" or "blur" elements actually visible?
() => {
  const glass = document.querySelectorAll('[class*="glass"], [class*="blur"]');
  return [...glass].map(el => {
    const style = getComputedStyle(el);
    return {
      tag: el.tagName,
      bg: style.backgroundColor,
      backdropFilter: style.backdropFilter,
      border: style.border,
      opacity: style.opacity
    };
  }).slice(0, 5);
}
```

If ANY programmatic check reveals an issue (containers at left=0, overflow elements, invisible effects), it's automatically a CRITICAL finding in the critique.

### Intent Comparison (MANDATORY)

For each major visual element in the brief, explicitly compare:

| Element | Brief Intent | Screenshot Reality | Match? |
|---------|-------------|-------------------|--------|
| [e.g. Glass cards] | Visible glassmorphic with translucent bg, blur, border gradient | [what you actually see] | YES/NO |
| [e.g. Containment] | Content centered with margins | [what you actually see] | YES/NO |
| ... | ... | ... | ... |

Every NO becomes a CRITICAL or MAJOR finding.

## Phase 4B: Fix Loop

After the critique is complete:

```
1. Fix ALL critical issues first, then major, then minor
2. Re-screenshot the affected sections
3. Re-run programmatic checks
4. Write a SHORT re-assessment: "Fixed X. Before: [problem]. After: [result]."
5. If new issues emerged from fixes, add them and continue
6. Repeat until the critique comes back clean
7. Clean up any verification screenshots
8. THEN proceed to Phase 5
```

**The fix loop is NOT optional.** You cannot skip from critique to presentation. Every CRITICAL and MAJOR issue must be resolved and visually confirmed resolved.

## Evaluation Criteria (Reference for Critique)

Use these as a LENS for the adversarial critique, not as a checkbox to tick "pass" on:

| Criterion | What Makes It FAIL (be specific) |
|-----------|----------------------------------|
| **Spacing rhythm** | Elements at different indentation levels. Sections with inconsistent padding. Cards with varying internal spacing. |
| **Typography hierarchy** | H2 and body text look the same weight. Caption text is same size as body. Heading doesn't command attention. |
| **Color balance** | Accent color on too many elements. Background elements competing with foreground. Dark-on-dark with no contrast. |
| **Alignment** | Content starting at different left edges across sections. Centered content mixed with left-aligned without reason. |
| **Content legibility** | Text over busy background without sufficient overlay. Small text at mobile. Muted text that's too muted to read. |
| **Design effect visibility** | Glass/blur/shadow effects that are technically present but visually invisible. Borders too subtle to see. |
| **Content containment** | Text or cards touching viewport edges. Max-width containers not centering. Padding insufficient on mobile. |
| **Responsive integrity** | Columns that should stack but don't. Text that overflows. Touch targets too small on mobile. |
| **Visual weight distribution** | All elements same visual weight -- nothing stands out. No visual anchor per section. |
| **Design system match** | Colors not matching tokens. Spacing not from the scale. Fonts wrong. Border-radius inconsistent. |

## Screenshot Management

- **Verification screenshots are ephemeral.** They exist only for the critique loop.
- After verification completes successfully, clean up any verification screenshots.
- **Exception:** If the user explicitly asks to see a screenshot or save one, keep it and save to the location they specify. Don't clean up requested screenshots.

## For Non-Renderable Output

When the output can't be opened in a browser (terminal UI concepts, email text, doc outlines):

1. Write the adversarial critique against the guardrails -- same "what would get rejected?" framing
2. Do the intent comparison table
3. Fix and re-assess
4. Document the critique and resolution

## Verification Tools

This protocol works with any tool that can:
1. Open a URL in a headless browser
2. Resize the viewport
3. Take a full-page screenshot
4. Execute JavaScript in the page context

**The protocol matters more than the tool.** The adversarial framing, intent comparison, and severity grading are what make verification work. The screenshot tool is just the mechanism.

**Common tools:**
- **Playwright MCP** (Claude Code default) -- `mcp__playwright__browser_navigate`, `mcp__playwright__browser_resize`, `mcp__playwright__browser_take_screenshot`, `mcp__playwright__browser_evaluate`
- **Puppeteer** -- `npx puppeteer screenshot <url>` (Node.js)
- **Manual browser** -- Open DevTools, use device toolbar for viewport sizes, take screenshots manually

The programmatic layout checks (JavaScript snippets in Phase 4A) work in any browser console. Copy-paste them into DevTools if you don't have automated browser access.
