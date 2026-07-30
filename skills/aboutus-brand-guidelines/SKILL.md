---
name: aboutus-brand-guidelines
description: "The official Us (About-us.be) design system — colours, typography, spacing, layout and component rules, derived directly from the agency Figma file. Use this skill whenever producing anything that carries the agency visual identity — presentations, pitch decks, proposals, Word documents, PDFs, dashboards, web pages, React components, HTML artifacts, charts, diagrams or one-pagers. Trigger it even when branding is not mentioned explicitly; if the person works at Us and is making something people will look at, it applies. Also trigger on onze huisstijl, onze kleuren, brand guidelines, on-brand, agency style, make it look like us, or any mention of Owners, IvyPresto, Archivo, Lavender, Mint Green or Shark in an About-us context."
---

# Us design system

Source of truth is the Figma file **Us - Design System**. This skill mirrors it.
If they ever disagree, Figma wins.

## First: which profile?

Two output profiles. They share every colour, size and spacing value and differ
only in typeface. Pick one before writing anything.

| Output | Profile |
|---|---|
| Web pages, React, HTML artifacts, dashboards | **Web** — Owners + IvyPresto + Public Sans |
| Presentations, .pptx, Word, PDF | **Presentation** — Archivo + Public Sans |

Presentations use Archivo because a deck opens on machines nobody controls.
Never mix profiles inside one deliverable.

## The non-negotiables

1. **Never invent a value or a style.** Every colour, size, space and radius
   comes from the token list, and every rule comes from Figma or the reference
   slides. If something is not specified — an eyebrow style, a chart palette, a
   slide composition — **stop, tell the user what is missing, and ask before
   continuing**. Do not approximate with a nearby token. A plausible-looking
   invention is worse than an obvious gap, because nobody catches it.
2. **Never use a primitive colour directly.** Lavender is a palette entry, not
   a UI colour. Use the semantic tokens: page background, content heading,
   button background.
3. **Buttons are black, not purple.** Primary is Shark `#191A1B` with a white
   label. The brand pastels are backgrounds and graphics, never interface
   chrome. Purple buttons are the single most common way to get this wrong.
4. **Uppercase is for large headings only.** H1 to H3 and CTA banners.
   Everything smaller — card titles, eyebrows, labels, body — is sentence case.
   In a deck, only the main slide title is uppercase.
5. **Never apply letter-spacing.** All 46 Figma text styles are 0. No
   tracking, at any size or weight, including small uppercase labels and
   eyebrows. In CSS do not set the property; in pptxgenjs never set
   `charSpacing`.
6. **Spacing comes from the scale**: 4, 8, 12, 16, 20, 24, 32, 40, 48, 56, 64,
   80, 96, 112. Nothing in between. No 10, no 15, no 30.
7. **Body copy is Light (300).** Easy to get wrong by defaulting to Regular.
8. **One theme per surface**, and text comes from Theme-Dark of that same
   theme. Never two themes on one slide or section.
9. **Titles are heavy.** Slide and page titles use the bold or black weight. A
   title that is not visibly heavier than its surroundings is wrong.
10. **Cards are 24px rounded.** A generous curve, not a hint of one.
11. **Colour is not optional.** All-grey is reserved for data-dense slides.
    Everything else carries at least one coloured element.

## Fast reference

Enough for most tasks. Read the reference files for anything beyond this.

**Themes** — four modes of the same four tokens. Build against the tokens, not
the colours, and the component works in every theme. One theme per surface,
text always from Theme-Dark.

| Token | Purple | Pink | Green | Orange |
|---|---|---|---|---|
| Theme-Light (fill) | `#F2F0FF` | `#FBE3FF` | `#E6FFEF` | `#FFF3EB` |
| Theme-Primary (fill) | `#BDB4FF` | `#F3AAFF` | `#8DFFB7` | `#FFB985` |
| Theme-Medium (accent) | `#6257E8` | `#B20CCC` | `#048255` | `#B35610` |
| Theme-Dark (text) | `#423A75` | `#7E1C74` | `#1E625A` | `#872012` |

All Light+Dark and Primary+Dark pairings meet WCAG AA. Shark `#191A1B` is the
neutral dark, for text on white and for dark surfaces.

**Neutrals** — white `#FFFFFF`, `#F9F9F9`, `#EAEAEA`, `#A7A7A7`, `#707070`,
`#494949`, `#2E2E2E`. Never pure black except Neutrals/100.

**Type ramp**, desktop values — H1 56/80, H2 40/56, H3 24/40, H4 24/32,
H5 20/32, H6 20/32, body 16/28, small 14/24, large 20/32.

**Layout** — content maxes at 1180 inside a 1440 canvas, fluid below. Section
rhythm defaults to 96. Cards 24 radius, buttons pill.

**Charts** — series order Lavender, Mint Green, Rajah, Perfume.

## Reference files

Read the one that matches the task. Do not read all three.

- `references/presentations.md` — decks and .pptx. Slide patterns, the
  dark/light sandwich, font fallbacks, and the PowerPoint-specific traps.
  **Read this before building any deck.**
- `references/web.md` — web and Cursor. How to load the tokens, the container
  pattern, the fluid responsive model, Tailwind mapping.
- `references/tokens.md` — the full token list. Every semantic colour across
  all five modes, the complete type ramp, spacing, radii, icons.

`assets/us-tokens.css` is the generated token file. Copy it into web projects
rather than retyping values.

## What to avoid

These read as generic AI output and are wrong for this brand specifically:

- Accent bars or stripes under headings. The design never uses them.
- Uppercase card titles, eyebrows or labels.
- Letter-spaced anything. The system has no tracking at all.
- Titles set at medium weight.
- Card corners under 24px.
- Slides with no colour at all, unless they are data-dense.
- Two themes competing on one surface.
- Purple or mint buttons.
- Centred body copy. Left-align paragraphs and lists; centre only titles.
- Drop shadows beyond the single soft shadow in the system.
- Decorative gradients behind body text. Gradients are used sparingly and only
  as background washes.
