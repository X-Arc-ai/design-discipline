# Design Guardrails

These are hard rules. They encode lines that, when crossed, reliably produce amateur or generic output. Every anti-pattern traces to a specific rejection during design work. They apply across ALL mediums -- interpret each for the medium at hand.

**Philosophy:** Guardrails tell you what NOT to do. They don't prescribe HOW to do it. A design system can use any spacing scale, any type scale, any palette. But it must be a SYSTEM, not arbitrary decisions per element.

## Consistency Guardrails (Break these and the system falls apart)

| Guardrail | Why It Breaks Quality When Violated |
|-----------|-------------------------------------|
| **Use a spacing system** | Arbitrary spacing between elements makes the whole thing feel uncoordinated. Pick any scale. Apply it everywhere. |
| **Use a type hierarchy** | When heading sizes, weights, and spacing don't follow a predictable pattern, the page feels random. |
| **Use a restrained color palette** | Too many colors = visual noise. The specific colors don't matter. The restraint does. |
| **Consistent border-radius** | Mixing rounded and sharp corners on the same page signals carelessness. |
| **Consistent component patterns** | If cards look different in each section, it breaks the design language. |
| **Consistent elevation model** | Mixing shadows, borders, and background shifts randomly breaks spatial hierarchy. Pick an approach. |

## Quality Floor (Below these, output reads amateur)

| Guardrail | What Happens Below |
|-----------|--------------------|
| **Sufficient contrast** | Text becomes unreadable. Accessibility fails. Instant amateur signal. |
| **Readable body text** | Text too small to scan comfortably signals you didn't test your own output. |
| **Adequate whitespace** | Cramped layouts feel cheap. Generous spacing is the universal marker of premium. |
| **Heading proximity to content** | Headings floating equidistant between sections lose their association. A heading belongs to what follows it. |
| **Content never touches edges** | Zero padding between text and container borders looks broken. |
| **Responsive integrity** | If it breaks or overflows at common breakpoints, it shipped unfinished. |

## Anti-Patterns (Validated Rejections)

**This is a living list.** When a new pattern is rejected in future work, add it here with the quote and date. This list grows with experience.

| Anti-Pattern | Rejection | Date | Applies To |
|--------------|-----------|------|------------|
| Gradients, glows, glossy effects | "no gradients, no AI cliches. It should feel like something stamped on equipment that works." | Feb 26, 2025 | Any visual output |
| Emoji-based icons/elements | Design with emoji checkmarks was rejected -- "breaks the clean aesthetic" | Feb 26, 2025 | Any visual output |
| Hype words, rhetorical questions | "language has to be very simple and clear. no weird posts with words then question marks." | Multiple, 2025 | Any content |
| Card grids for narrative content | "cards don't make the user connect. I think it should be told like a story." | Feb 27, 2025 | Any medium where content tells a story |
| Abstract illustrations that don't communicate | "abstract circles and lines that don't say shit" | Mar 6, 2025 | Any visual -- covers, banners, diagrams, slides |
| Generic/dreamy promises without substance | "the solution seems like 'the sky is blue' -- it feels like a scam" | Feb 26, 2025 | Any content that explains capabilities |
| Inline CTAs that feel like alerts | "The CTAs in cards feel like some sort of alerts. They should be simple and clear." | Feb 26, 2025 | Any interactive output |
| Em dashes | "avoid em dashes please (learn this once and for all)" | Permanent | All written content |
| Dashboard mockups for brand pieces | Self-diagnosed: "Still feels like a dashboard mockup, not a brand piece" | Mar 6, 2025 | Brand/marketing material |
| Overengineered visual systems | Pixel art, PixiJS, sprite sheets, canvas -- "it sucks" | Feb 21, 2025 | Any visual output -- simplest approach that looks premium |
| Merging sections that should stay separate | "not good - bring it back how it was, keep them separated" | Feb 26, 2025 | Any structured content |
| Changing design approach of working elements | "on the team, it's wrong and bad - keep the cards, just change their design" | Feb 26, 2025 | Any design iteration |
| Generic/AI aesthetic output | Every V1 attempt defaulted to the same patterns. The bar is enterprise/agency-grade. | Structural | Everything |
| Ornamental design elements (italic quotes, colored dashes, section labels) | "the italic, green dashes, etc isn't minimalistic -- premium and minimalistic is a way for us to help the viewer to understand instantly what they're seeing, not to make it complicated with crowded design elements" | Mar 22, 2025 | Any visual output -- especially slides. Strip to essentials: headline, data, capabilities. No decorative quotes, colored bullet markers, or labeled sections. |
| Slides that overflow the viewport | "the case studies slides are too big" -- slides are meant to be viewed one at a time, not scrolled. Every slide must fit one viewport. | Mar 22, 2025 | Slide decks, presentations |
| Confirmation bias during verification | Real project: screenshots were taken, criteria were "checked," output was declared passing -- but content bled to edges, glass effects were invisible, cards had no icons. Checklist-passing is not quality-passing. The fix: adversarial critique ("what would get rejected?") + programmatic layout checks + intent-vs-reality comparison. | Mar 25, 2025 | ALL verification -- the model defaults to confirming its own work unless forced into adversarial framing |
