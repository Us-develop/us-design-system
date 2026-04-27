# US Design System — Agent implementation brief

Single-file reference derived from the Figma-exported **Design Tokens Community Group (DTCG)** JSON in this repository. Use this document to implement CSS, component libraries, or design-to-code pipelines without opening every token file.

**Repository layout (source of truth)**

| Folder | Role |
|--------|------|
| `01. Primitive Tokens/Mode 1.tokens.json` | Base palette, spacing scale, font families, font-weight strings |
| `02. Color Tokens/*.tokens.json` | **Semantic** colors per theme: `Light`, `Dark`, `Grey`, `Color` |
| `03. Document Tokens/{Desktop,Mobile}.tokens.json` | Page width, content width, margins, grid, nav spacing |
| `04. Number Tokens/{Desktop,Mobile}.tokens.json` | Component spacing, radii, typography (sizes & line heights) |

**Units:** Numeric tokens are **px** in Figma (e.g. `16` = 16px). Map to `rem` in CSS as needed (1rem = 16px is typical).

**Theming:** Switch semantic color sets by `Light` / `Dark` / `Grey` / `Color` (see `02. Color Tokens/`). Document and number tokens are split by `Desktop` vs `Mobile` **modes**—use media queries to swap values.

---

## 1. Brand & primitives (color)

### Primary palette

| Token path | Hex |
|------------|-----|
| `Color.Primary.Lavender` | `#BDB4FF` |
| `Color.Primary.Perfume` | `#F3AAFF` |
| `Color.Primary.Mint Green` | `#8DFFB7` |
| `Color.Primary.Rajah` | `#FFB985` |
| `Color.Primary.Shark` | `#191A1B` |

### Secondary

| Token path | Hex |
|------------|-----|
| `Color.Secondary.Spring Wood` | `#FCFCF8` |
| `Color.Secondary.Ecru` | `#F5F4E5` |
| `Color.Secondary.Light.Titan White` | `#F2F0FF` |
| `Color.Secondary.Light.Selago` | `#FBE3FF` |
| `Color.Secondary.Light.Hint of Green` | `#E6FFEF` |
| `Color.Secondary.Light.Seashell Peach` | `#FFF3EB` |
| `Color.Secondary.Medium.Royal` | `#6257E8` |
| `Color.Secondary.Medium.Electric Violet` | `#B20CCC` |
| `Color.Secondary.Medium.Watercourse` | `#048255` |
| `Color.Secondary.Medium.Hawaiian Tan` | `#B35610` |
| `Color.Secondary.Dark.East Bay` | `#423A75` |
| `Color.Secondary.Dark.Disco` | `#7E1C74` |
| `Color.Secondary.Dark.Green Pea` | `#1E625A` |
| `Color.Secondary.Dark.Pablo` | `#872012` |

### Neutrals (10 → 100, plus 00)

| Token | Hex |
|-------|-----|
| `Neutrals.00` | `#FFFFFF` |
| `Neutrals.10` | `#FCFCFC` |
| `Neutrals.20` | `#F9F9F9` |
| `Neutrals.30` | `#F3F3F3` |
| `Neutrals.40` | `#EAEAEA` |
| `Neutrals.50` | `#D9D9D9` |
| `Neutrals.60` | `#A7A7A7` |
| `Neutrals.70` | `#707070` |
| `Neutrals.80` | `#494949` |
| `Neutrals.90` | `#2E2E2E` |
| `Neutrals.100` | `#000000` |

### System (status)

| Token | Hex |
|-------|-----|
| `System.Error` | `#DF2020` |
| `System.Info` | `#3C81E7` |
| `System.Success` | `#41BD73` |
| `System.Warning` | `#EB8916` |

---

## 2. Semantic colors (Light vs Dark) — high-signal tokens

Use **semantic** names in UI; bind them to **Light** or **Dark** (and other theme files as needed).

### Page & content

| Semantic role | Light (`Light.tokens.json`) | Dark (`Dark.tokens.json`) |
|----------------|-----------------------------|----------------------------|
| `Content.Heading` | `#191A1B` (Shark) | `#FFFFFF` (Neutrals/00) |
| `Content.Body` | `#191A1B` | `#FFFFFF` |
| `Content.Placeholder` | `#707070` (N/70) | `#F9F9F9` (N/20) |
| `Content.Quote` | `#191A1B` | `#FFFFFF` |
| `Content.Link (content)` | `#4F72CD` | `#CAD9F5` |
| `Page.Page-Background` | `#FFFFFF` | `#191A1B` (Shark) |

### Navigation (labels)

| Token | Light | Dark |
|-------|-------|------|
| `Navigation.Nav_item-Default` | `#191A1B` | `#FFFFFF` |
| `Navigation.Nav_item-Hover` | `#191A1B` | `#FFFFFF` |

### Buttons (default: primary = filled dark on light; inverted on dark)

**Default state — Light theme**

- `Button-Bg-Default` (primary fill): `#191A1B`
- `Button-Prim_Label` / `Button-Prim_Icon`: `#FFFFFF`
- `Button-Sec_Label` / `Button-Sec_Icon` (secondary / outline text & icons): `#191A1B`
- `Button-Stroke`: `#191A1B`

**Default state — Dark theme** (inverts: light surface, dark text on primary)

- `Button-Bg-Default`: `#FFFFFF`
- `Button-Prim_Label` / `Button-Prim_Icon`: `#191A1B`
- (Read `Dark.tokens.json` for secondary, hover, disabled to match the same file structure as Light.)

**Hover (Light):** e.g. `Button-Bg-Hover` → `#494949` (N/80); secondary hover labels often flip to white on dark grey; `Button-Stroke` hover → `#494949`.

**Disabled (Light):** `Button-Bg-Disabled` → `#EAEAEA` (N/40); label/icon disabled → `#707070` (N/70).

**Borders (Light):** `Borders.Seperator` (note Figma spelling) and `Borders.Border 01` → `#EAEAEA`; `Borders.Border 02` → `#494949`.

Implement **hover** and **disabled** for Dark by following the same object paths under `Button` in `Dark.tokens.json`.

**Additional themes:** `Grey.tokens.json` and `Color.tokens.json` mirror the same semantic **paths** with different resolved colors—treat as alternate brand or neutral modes.

---

## 3. Typography

### Font families (primitives: `Typography.Font`)

**Impact (default product UI)**

| Use | Family |
|-----|--------|
| Headings, quote, navigation, button | `Bricolage Grotesque` |
| Body | `Public Sans` |

**Cocreate (alternate / campaign)**

| Use | Family |
|-----|--------|
| Headings 1 | `Owners XWide` |
| Headings 2 | `IvyPresto Display` |

Load via `@font-face` or Google Fonts / Fontshare as your stack allows. Ensure **Public Sans** and **Bricolage Grotesque** for core layouts.

### Font weights (string tokens → implement with `font-weight`)

| Token | Value |
|-------|--------|
| H1, H2, H3 | Bold (typically 700) |
| H4, H5 | Medium (500) |
| H6, Body_Default, Link | Light (300) |
| Body_Bold | Semibold (600) |
| Quote, Nav | Medium (500) |

Confirm numeric weights against the actual font files (variable fonts may differ).

### Type scale (Desktop) — `04. Number Tokens/Desktop.tokens.json`

Values are **font-size (px)** and **line-height (px)**.

| Style | Size | Line height |
|-------|------|-------------|
| H1 | 64 | 80 |
| H2 | 48 | 64 |
| H3 | 32 | 48 |
| H4 | 32 | 40 |
| H5 | 20 | 32 |
| H6 | 20 | 32 |
| Paragraph-Default | 16 | 28 |
| Paragraph-Small | 14 | 24 |
| Paragraph-Large | 20 | 32 |
| Quote | 32 | 48 |
| Nav | 16 | 24 |
| Button | 18 | 24 |

### Type scale (Mobile) — same file, `Mobile` mode

At minimum, **H1** scales to **48px** size and **64px** line height on mobile (vs 64/80 on desktop). Re-read `04. Number Tokens/Mobile.tokens.json` for any other overrides (H2–H6, body, etc.) when implementing responsive type.

---

## 4. Spacing primitives

Base scale (px): `0,25 rem`=4, `0,5`=8, `0,75`=12, `1`=16, `1,25`=20, `1,5`=24, `2`=32, `2,5`=40, `3`=48, `3,5`=56, `4`=64, `5`=80, `6`=96, `7`=112.

Use these for margin/padding/gap unless a **semantic** spacing token from section 5 applies.

---

## 5. Semantic spacing, radius, layout

### Border radius — Desktop & Mobile (same names; verify values in `04. Number Tokens`)

| Token | Typical value (px) |
|-------|--------------------|
| `Radius-None` | 0 |
| `Radius-XS` | 2 |
| `Radius-S` | 4 |
| `Radius-M` | 8 |
| `Radius-L` | 24 |
| `Radius-XL` | 32 |
| `Radius-Round` | 500 (pill) |
| `Radius-Image` | 12 |
| `Radius-Cards` | 24 |

### Content spacing (examples — `Spacing.Content` in number tokens)

**Desktop:** e.g. `H - Content (Large)` 32, `H - Content (Small)` 16, `Content - Button` 48, `Nav - content (Default)` 96, `Nav - content (Large)` 160, `2 buttons` gap 20.

**Mobile:** often reduced (e.g. `Nav - content` 64, `Content - Button` 32, `2 buttons` 16). Use the `Mobile` JSON for exact values.

### Document / layout — Desktop (`03. Document Tokens/Desktop.tokens.json`)

| Token | Value (px) |
|-------|------------|
| `Page.Page-Width` | 1440 |
| `Page.Content-Width` | 1180 |
| `Margins.Page-Margin` | 130 |
| `Margins.Footer-Margin` | 112 |
| `Margins.Row_Indent-Small` | 32 |
| `Margins.Row_Indent-Medium` | 64 |
| `Margins.Row_Indent-Large (Default)` | 96 |
| `Margins.Row_Indent-XLarge` | 128 |
| `Margins.MaxCols` | 330 |
| `Grid.Grid-Width` (column) | 80 |
| `Grid.Grid-Gutter` | 20 |
| `Grid.Grid-Column_Count` | 12 |
| `Navigation.Margin-Top_Bottom` | 12 |

### Document / layout — Mobile

| Token | Value (px) |
|-------|------------|
| `Page.Page-Width` | 360 |
| `Page.Content-Width` | 320 |
| `Margins.Page-Margin` | 20 |
| `Margins.Footer-Margin` | 64 |
| `Row_Indent` variants | 24, 48, 64, 112 (read file for key names) |
| `MaxCols` | 320 |

**Breakpoint strategy:** Figma does not export a single “breakpoint” token. Practical approach: use **~768px** or **min-width: 1024px** to switch from Mobile document values to Desktop, and align `04. Number Tokens` mode accordingly—adjust to your product’s art direction.

---

## 6. Agent checklist (implementation)

1. **Tokens pipeline:** Map DTCG JSON to CSS custom properties, Tailwind theme, or Style Dictionary. Strip `com.figma.*` extensions; keep `hex` and numeric values.
2. **Themes:** Implement at least **Light** and **Dark** using paths under `02. Color Tokens/`. Add **Grey** / **Color** as optional `data-theme` or class variants.
3. **Typography:** Load **Bricolage Grotesque** + **Public Sans**; apply desktop/mobile scales from `04. Number Tokens`.
4. **Layout:** Max content width 1180px on desktop; 12-column grid with 80px tracks and 20px gutter (from document tokens); respect page margins.
5. **Components:** Buttons must implement **default, hover, disabled** (and any focus ring your a11y spec requires—tokens do not include focus). Use semantic colors, not raw primaries, for standard UI.
6. **Accessibility:** Pair Light/Dark text and background from semantic tokens; verify contrast for custom combinations.

---

## 7. Starter CSS custom properties (Light theme, illustrative)

Agents can expand this pattern for Dark and other modes.

```css
:root {
  /* Primitives (sample) */
  --color-shark: #191a1b;
  --color-neutral-00: #ffffff;
  --color-neutral-40: #eaeaea;
  --color-neutral-70: #707070;
  --color-neutral-80: #494949;

  /* Semantic — Light */
  --color-page-bg: var(--color-neutral-00);
  --color-text: var(--color-shark);
  --color-text-placeholder: #707070;
  --color-link: #4f72cd;

  --color-button-primary-bg: var(--color-shark);
  --color-button-primary-fg: var(--color-neutral-00);
  --color-button-hover-bg: var(--color-neutral-80);
  --color-button-disabled-bg: var(--color-neutral-40);
  --color-button-disabled-fg: var(--color-neutral-70);

  --font-heading: "Bricolage Grotesque", system-ui, sans-serif;
  --font-body: "Public Sans", system-ui, sans-serif;

  --space-1: 0.25rem; /* 4px */
  --space-4: 1rem;    /* 16px */
  --radius-m: 8px;
  --radius-card: 24px;
}
```

---

## 8. Version note

This brief reflects the JSON committed in this repository. Re-export or sync from Figma when design tokens change, then update this file or regenerate from tooling.
