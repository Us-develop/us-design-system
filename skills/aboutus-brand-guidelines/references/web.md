# Web and Cursor

Put both files in the repo:

```
/design-system/us-tokens.css
/.cursor/rules/us-design-system.mdc
```

The `.mdc` file is this document with frontmatter at the top:

```
---
description: Us design system rules. Apply to all UI work.
alwaysApply: true
---
```

Import `us-tokens.css` once at the app root. Cursor then has both the values and
the rules on every request, without anyone pasting anything.

For Tailwind projects, map the tokens rather than duplicating them:

```js
// tailwind.config.js
theme: {
  extend: {
    colors: {
      'page-background': 'var(--page-page-background)',
      'content-heading': 'var(--content-heading)',
      'content-body': 'var(--content-body)',
      'button-bg': 'var(--button-default-state-button-bg-default)',
      'button-label': 'var(--button-default-state-button-prim_label)',
      'border-01': 'var(--borders-border-01)',
    },
    fontFamily: {
      h1: 'var(--typography-font-headings-default-h1-wide)',
      h4: 'var(--typography-font-headings-default-h4)',
      body: 'var(--typography-font-body)',
      quote: 'var(--typography-font-quote)',
    },
    borderRadius: {
      card: 'var(--radius-radius-cards-lg)',
      pill: 'var(--radius-radius-round)',
    },
  },
}
```

Mapping means one place to change when Figma changes.

---

---

## Layout and the responsive model

The system is **fluid, not breakpointed**. Figma defines two modes, Mobile at
360 and Desktop at 1440. Every dimensional token interpolates linearly between
them with `clamp()`, so a 900px viewport gets a value partway between rather
than snapping to one or the other.

| | at 360 | at 1440 |
|---|---|---|
| Page margin | 20 | 130 |
| Content width (max) | 320 | 1180 |
| Grid column width | 40 | 80 |
| Gutter | 16 | 20 |
| Max column text width | 320 | 330 |

**Do not use `--margins-maxcols` as paragraph `max-width`.** In Figma this value
is a layout helper (right-margin / column boundary for designing non-full-width
content), not the readable width for body copy. At ~330px it is too narrow for
normal paragraphs.

For body text and intros, use a prose width derived from the content area until a
dedicated token exists in Figma (e.g. `--content-prose-max-width`):

```css
.prose-width {
  max-width: min(100%, calc(var(--page-content-width) * 0.62));
}
```

That yields ~732px at the 1180px content max — readable without spanning the full
container. Adjust the ratio in Figma if designers want a different measure; then
regenerate tokens rather than hand-editing.

Below 360 and above 1440 the values clamp. 1440 is the design canvas, so the
layout stops growing there and centres.

**One discrete breakpoint exists, at 768px, and it only switches grid column
count from 12 to 6.** A grid cannot be 9.4 columns. Everything else is
continuous.

### The container

Do not build a fixed 1440 page. The standard container is:

```css
.container {
  width: 100%;
  max-width: var(--page-content-width);
  margin-inline: auto;
  padding-inline: var(--margins-page-margin);
}
```

Full-bleed backgrounds sit outside this; content sits inside it.

### Reading the token values

A consequence worth knowing before someone opens the file and panics: the
numbers no longer read as the plain Figma values. `--typography-font-size-h1-default`
is `clamp(40px, 34.667px + 1.4815vw, 56px)`, not `56px`. The endpoints are
exact, 40 at mobile and 56 at desktop, but the middle is interpolated. Change
the variable in Figma and regenerate, never hand-edit a clamp.

### Vertical rhythm

Space between page sections uses the row indent scale, fluid across the range:

- Small 24 to 32
- Medium 48 to 64
- **Large 64 to 96 (default)**
- XLarge 112 to 128

### Spacing inside a block

Three of these run backwards, larger on mobile than desktop, which is
deliberate and comes straight from Figma:

- Heading to content (large): 24 to 32
- Heading to content (medium): **24 down to 16**
- Content to button (small): **20 down to 16**
- Content to button (large): 32 to 48
- Between two adjacent buttons: 16 to 20

The pattern to internalise: outer containers get more space than inner
elements. If a nested gap is larger than its parent gap, the hierarchy reads
backwards.

### Radius

None 0, XS 2, S 4, M 8, L 24, XL 32, Round 500. Images 12. Cards 24 large.
Small cards run 24 on mobile down to 12 on desktop, the only fluid radius.

Buttons are pill-shaped (Round). Cards are 24, and that is a visible, generous
curve — not a hint of a corner. Do not invent 8, 12 or 16 for a card.

---