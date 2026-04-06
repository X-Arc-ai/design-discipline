# Design Knowledge Reference

This is reference material for IDEATION -- it informs choices but doesn't prescribe them. These are fundamentals (perceptual science, timeless principles), not trends or specific values.

**The test for inclusion:** "Does this help me make a BETTER choice, or just a SPECIFIC choice?" Only fundamentals survive.

## Perceptual Principles (Science, not opinion)

### Gestalt Principles
These explain WHY some layouts feel right. Naming them helps reason about layout decisions:

- **Proximity:** Elements close together are perceived as related. (Headings must be closer to the content below than the section above.)
- **Similarity:** Elements sharing visual characteristics (weight, color, size) are perceived as grouped.
- **Common Region:** Elements in an enclosed area (card, bordered section) are perceived as a unit.
- **Figure/Ground:** The brain separates foreground from background. Whitespace isn't empty -- it's the ground that makes the figure readable.

### Visual Hierarchy
Guide the eye through variation in scale, weight, contrast, and position. There must be a clear primary > secondary > tertiary reading order. When everything has equal weight, nothing stands out.

### Reading Patterns
- **F-pattern** (content-heavy): eye scans top, shorter pass below, then vertical down left
- **Z-pattern** (minimal pages): top-left to top-right, diagonal, bottom-left to bottom-right

Useful for deciding where to place key content. Not a rigid rule.

### Optical vs Mathematical Alignment
Sometimes elements need to be off-grid by 1-2px to LOOK aligned. Geometric center and perceived center differ. Triangular icons in circular buttons need rightward offset to feel centered. Subtle but noticeable when wrong.

## Design Judgment Principles (Timeless)

**"Less, but better" (Dieter Rams):** For every element, ask: can I remove this without losing meaning? Decoration without function is noise.

**"Knowing what to remove, not what to add" (Emil Kowalski on taste):** Taste manifests as appropriate restraint, clear hierarchy, consistency in every detail, and the absence of noise. Nothing arbitrary, nothing accidental.

**Content resilience:** Does the design handle edge cases? Long names, empty lists, missing images, error states, one-item grids. Designing only the happy path with perfect content is incomplete work. Every state matters.

**Nested radii:** When an element with border-radius contains a child with border-radius, the child radius must be smaller (parent radius minus the gap). When this is wrong, the curves don't flow concentrically. Subtle but a telltale of careless implementation.

**Heading belongs to what follows:** More space above, less below. Gestalt proximity applied to typography.

## Model-Specific Awareness

**I can't feel spacing.** A human designer senses "that's too tight." I can't. So I must be systematic: define spacing values in the design system, apply them consistently, then VERIFY via screenshot. This is why the verification loop is mandatory.

**I default to the median of my training data.** My first instinct trends toward the average of what I've seen -- which is generic. The guardrails (anti-patterns from validated rejections) exist specifically to pull me away from this median. When my output looks like "any AI-generated website," that's the signal to rethink.

**I'm strong at consistency, weak at novelty.** Once a design system is established, I can apply it perfectly across 100 components. But generating the INITIAL direction requires the Ideate phase -- deliberately considering multiple approaches before defaulting to the first one. Studying the project's existing approved work matters most here.
