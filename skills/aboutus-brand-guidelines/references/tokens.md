# Full token reference

Typefaces and the type ramp, colour across the five colour modes and the four
themes, components.

## Typefaces

Two profiles. Same sizes, same spacing, same colours. Only the families differ.

| | Web / digital product | Presentation |
|---|---|---|
| Headings, nav, buttons, card titles | **Owners** (XWide, Wide, Regular, Narrow, XNarrow) | **Archivo** / Archivo Black / Archivo Narrow |
| Quotes, alt headings | **IvyPresto Display** | **Archivo** (Thin / Light) |
| Body copy | **Public Sans** | **Public Sans** |
| UI icons | **Material Symbols Outlined**, weight 300 | same |
| Brand / social marks | Font Awesome 6 Brands | same |

Web is the default in `us-tokens.css`. Switch profiles by setting
`data-us-fonts="presentation"` on the root element. Archivo trails every web
stack as a fallback so a page still renders sensibly before the Owners webfont
files are hosted.

### Why the split

Owners and IvyPresto are licensed for digital products, where the fonts are
self-hosted and the rendering environment is controlled. A deck is not a
controlled environment: it opens on a client's laptop, gets exported to PDF,
gets pasted into someone else's template. Archivo and Public Sans are Google
Fonts, so a deck built on them renders correctly everywhere with nothing
installed.

### Widths

| Owners width | Web (family name) | Presentation (`font-stretch`) |
|---|---|---|
| XNarrow | `owners-xnarrow` (not in kit) | 62% |
| Narrow | `owners-narrow` (not in kit) | 75% |
| Regular | `owners` | 100% |
| Wide | `owners-wide` | 112% |
| XWide | `owners-xwide` | 125% |

The two profiles handle width by different mechanisms. On web the Adobe kit
serves static faces, so width is a family name and `font-stretch` does nothing.
In the presentation profile there is no "Archivo Wide" family, so width comes
from Archivo's variable width axis via the `--font-stretch-*` tokens.

PowerPoint and Word cannot render variable axes at all. In a real deck, use the
static families (`--typography-font-static-*`), accept regular width, and do
not fake Wide with letter-spacing.

**Archivo Black is single-weight (400).** Never apply `font-weight: 700` on top
of it. The renderer synthesises a fake bold over an already-heavy face and the
result looks smeared.

### Tracking

There is none. Every text style in Figma is set to letter-spacing 0, all 46 of
them, across both typefaces and every size and weight.

Do not add tracking to compensate for a small size, a heavy weight, or an
uppercase label. Loosened small caps read as a different brand.

- CSS: do not set `letter-spacing`. If a reset or component library adds it,
  override with `letter-spacing: normal`.
- pptxgenjs: never set `charSpacing`.
- PowerPoint by hand: character spacing stays Normal.

### Icons

UI icons are **Material Symbols Outlined at weight 300**. Same in both profiles,
since Material Symbols is a Google Font and works everywhere.

Note the family name. "Material Icons" is the legacy static font and has no
weight axis, so weight 300 is not expressible in it. Weight 300 requires
**Material Symbols**, the variable version.

Four axes, always set together:

| Axis | Range | Us value |
|---|---|---|
| `wght` | 100 to 700 | **300** |
| `FILL` | 0 to 1 | 0 default, 1 for active or selected states |
| `GRAD` | -50 to 200 | 0 default, **-50 on dark backgrounds** |
| `opsz` | 20 to 48 | match the rendered size |

```css
.icon {
  font-family: var(--typography-font-icons);
  font-size: var(--typography-font-size-icons-24);
  color: var(--icon-icon-10);
  font-variation-settings:
    "FILL" var(--typography-icon-fill),
    "wght" var(--typography-icon-weight),
    "GRAD" var(--typography-icon-grade),
    "opsz" var(--typography-icon-opsz);
}
```

The grade override is already wired into the colour modes: `dark` and
`color-dark` set `--typography-icon-grade` to -50, which is the recommended
correction for light icons on a dark field. Nobody has to remember it.

Three things to watch:

1. **The style is Outlined.** Confirmed, not an assumption. Material Symbols
   also ships Rounded and Sharp. Never mix them in one product.
2. **The 12px and 16px sizes sit below the optical size floor.** The `opsz`
   axis bottoms out at 20, so small icons cannot be optically corrected and
   weight 300 will look thin at 12px. Only 20px and 24px are drawn on a perfect
   pixel grid. Prefer 16px as the smallest, and check 12px against a real
   screen before using it.
3. **Font Awesome is for brand marks only.** Material Symbols has no logos,
   so LinkedIn, Instagram and YouTube come from Font Awesome 6 Brands at 12,
   16, 24 and 32px, matching the `Brand/` text styles in Figma. Font Awesome is
   never used for UI icons.

### Loading

Web, from two Adobe Fonts kits. Load both before the tokens file:

```html
<link rel="stylesheet" href="https://use.typekit.net/dbo7deg.css">
<link rel="stylesheet" href="https://use.typekit.net/rgx8kmt.css">
```

Family names are Adobe's, lowercase and hyphenated. Use `"owners-wide"`, not
`"Owners Wide"`.

Two properties of these kits to design around:

**The faces are static, not variable.** Every `@font-face` declares a single
weight and `font-stretch: normal`. Do not apply `font-stretch` on web, it will
select nothing. Width comes from the family name.

**Adobe kits are domain-restricted.** They only serve fonts on domains
registered in their settings, and this applies to both kits separately. Add
`localhost` and any preview or staging domain to each, or the fonts silently
fall through to Archivo in local development while working fine in production.
That failure mode is easy to miss.

### What the kits contain

**`dbo7deg` — Owners.** Seven widths, all with the same weight set:

| Family | |
|---|---|
| `owners-xxnarrow`, `owners-xnarrow`, `owners-narrow` | narrower than regular |
| `owners` | regular |
| `owners-wide`, `owners-xwide`, `owners-xxwide` | wider than regular |

Weights per width: **200, 300, 400, 500, 700, 800, 900**, roman and italic.
No 100, no 600.

**`rgx8kmt` — IvyPresto Display.** One family, `ivypresto-display`, at weights
**100, 300, 400, 600, 700**, roman and italic. No 200, 500, 800 or 900.

Together these cover the entire type ramp. Every heading, nav item, button,
card title, alt heading and quote resolves to a real face. Nothing falls back
to Archivo on web.

Available but unused by the system: `owners-xxnarrow`, `owners-xxwide`, and the
full italic sets in both families. No Figma variable points at any of them.
Adding them is a design decision, not a technical one.

Minor housekeeping: these are two separate kits, so two requests and two domain
allowlists to maintain. Merging them into one kit in Adobe would remove both.

Presentation, from Google Fonts:

```html
<link href="https://fonts.googleapis.com/css2?family=Archivo:wdth,wght@62..125,100..900&family=Archivo+Black&family=Archivo+Narrow:wght@400..700&family=Public+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

Icons, both profiles:

```html
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" rel="stylesheet">
```

That URL loads the full axis ranges, which is a large file. Once the icon set
is settled, pin the axes to the values actually used
(`@20..48,300,0..1,-50..0`) or self-host via the `material-symbols` npm
package.

Axis order in the Archivo URL matters: registered axes are listed
alphabetically with `wght` always last. `wdth,wght` is correct, `wght,wdth`
will not load.

---

## Type ramp

Values are desktop / mobile. Line heights are fixed pixel values, not multipliers.

| Style | Web face | Weight | Size | Line height | Case |
|---|---|---|---|---|---|
| H1 | Owners Wide | 700 | 56 / 40 | 80 / 64 | UPPER |
| H1 small | Owners Wide | 700 | 48 / 40 | 64 / 56 | UPPER |
| H1 XL (hero) | Owners XWide | 700 | 112 / 64 | 136 / 80 | UPPER |
| H2 | Owners Wide | 700 | 40 / 32 | 56 / 56 | UPPER |
| H3 | Owners Wide | 700 | 24 / 20 | 40 / 32 | UPPER |
| H4 | Owners | 500 | 24 / 20 | 32 / 32 | Sentence |
| H5 | Owners | 500 | 20 / 20 | 32 / 32 | Sentence |
| H6 | Owners | 300 | 20 / 20 | 32 / 32 | Sentence |
| H1 alt | IvyPresto Display | 100 | 56 / 40 | 80 / 64 | UPPER |
| H2 alt | IvyPresto Display | 300 | 40 / 32 | 56 / 56 | UPPER |
| H3 alt | IvyPresto Display | 300 | 24 / 20 | 40 / 32 | UPPER |
| Quote small | IvyPresto Display | 100 | 32 / 24 | 48 / 32 | Sentence |
| Quote large | IvyPresto Display | 100 | 64 / 40 | 80 / 48 | Sentence |
| Nav | Owners | 500 | 16 | 24 | Sentence |
| Button | Owners | 500 | 18 / 16 | 24 / 20 | Sentence |
| Card title L | Owners | 500 | 24 | 38 | Sentence |
| Card title S | Owners | 500 | 20 | 32 | Sentence |
| CTA banner | Owners Wide | 700 | 32 / 32 | 48 | UPPER |
| Body | Public Sans | 300 | 16 / 16 | 28 / 24 | Sentence |
| Body large | Public Sans | 300 | 20 / 20 | 32 / 32 | Sentence |
| Body small | Public Sans | 300 | 14 / 16 | 24 / 24 | Sentence |
| Body bold | Public Sans | 600 | 16 | 28 / 24 | Sentence |

In the presentation profile every Owners row becomes Archivo at the matching
width, every IvyPresto row becomes Archivo at the same weight, and Public Sans
is unchanged. Sizes and line heights never change between profiles.

Narrow and XNarrow widths exist as tokens for headings that need to fit a tight
column. They are an exception, not a default.

Body copy is **Light 300**. This is deliberate and easy to get wrong. Do not
default to Regular 400.

---

## Colour

### The rule that matters

The interface is monochrome. Shark `#191A1B`, white, and the neutral ramp carry
almost all of the UI. The five brand colours appear as backgrounds, graphic
shapes, gradients and illustration, not as buttons, links or labels.

If a build has purple buttons, it is wrong.

### Brand palette

| Name | Hex | Where it belongs |
|---|---|---|
| Lavender | `#BDB4FF` | Section backgrounds, graphic elements, gradients |
| Perfume | `#F3AAFF` | Section backgrounds, graphic elements |
| Mint Green | `#8DFFB7` | Section backgrounds, graphic elements, gradients |
| Rajah | `#FFB985` | Section backgrounds, graphic elements |
| Shark | `#191A1B` | Text, buttons, dark sections. The workhorse |

Light tints (Titan White, Selago, Hint of Green, Seashell Peach) are the pastel
section backgrounds. Medium and dark secondaries (Royal, Electric Violet,
Watercourse, Hawaiian Tan, East Bay, Disco, Green Pea, Pablo) exist for accent
and contrast where a pastel needs a readable partner.

### Themes

Figma collection **06. Theme** holds four tokens across four modes. This is the
mechanism for coloured surfaces, and it replaces picking colours by hand.

| Token | Purple | Pink | Green | Orange |
|---|---|---|---|---|
| `Theme-Light` | Titan White `#F2F0FF` | Selago `#FBE3FF` | Hint of Green `#E6FFEF` | Seashell Peach `#FFF3EB` |
| `Theme-Primary` | Lavender `#BDB4FF` | Perfume `#F3AAFF` | Mint Green `#8DFFB7` | Rajah `#FFB985` |
| `Theme-Medium` | Royal `#6257E8` | Electric Violet `#B20CCC` | Watercourse `#048255` | Hawaiian Tan `#B35610` |
| `Theme-Dark` | East Bay `#423A75` | Disco `#7E1C74` | Green Pea `#1E625A` | Pablo `#872012` |

**Build against the tokens, not the colours.** A card written as `Theme-Light`
background with `Theme-Dark` text works in all four themes without being
rewritten. Switch with `data-us-theme="purple | pink | green | orange"` on a
page or section wrapper.

**The pairing rule:** a coloured surface takes its text from `Theme-Dark` of
the same theme. Light or Primary for the fill, Dark for the content. Medium is
for accents, icons and small marks.

Every Light+Dark and Primary+Dark pairing meets WCAG AA. The Light+Dark
pairings reach AAA. Lavender on East Bay is 5.32, Titan White on East Bay 8.92,
Mint Green on Green Pea 5.80, Rajah on Pablo 5.58.

One theme per surface. A slide or section commits to one; it never mixes two.

**Worth knowing:** the `Color - light` and `Color-dark` modes in the 02 Color
Tokens collection still reference the green primitives directly rather than the
Theme tokens. So switching theme does not currently change those two modes.
Wiring 02 to 06 would make the whole system theme-aware in one step.

### Gradients

Five gradient styles exist. The four tint gradients (Titan White, Selago, Hint
of Green, Seashell Peach) fade a single colour from full opacity to 10% alpha —
they fade to transparent, not to white, so they layer over what sits behind
them. Green-Purple is a two-colour blend from Mint Green to Perfume. Use is
deliberately limited. Never behind body copy.

### Colour modes

The system ships five modes: **Light**, **Dark**, **Grey**, **Color-light**,
**Color-dark**. A section, not just a page, can carry a mode. Set
`data-us-mode` on the section wrapper and every 02 token inside resolves
correctly. Never hand-pick a dark variant of a colour.

### System colours

Error `#DF2020`, Info `#3C81E7`, Success `#41BD73`, Warning `#EB8916`. These are
for feedback states only. Do not repurpose Success green as a brand accent, the
brand green is Mint Green and they are different.

---

## Components

The Figma library has 26 component pages: Accordion, Breadcrumb, Buttons,
Cards, Content, Elements, Stickers, FAQ, Feedback Messages, Filter, Footer,
Form elements, Graphic Elements, Icons, Imagery, List, Logo, Menu, Modal,
Navigation, Pagination, Progress, Slider, Search, Tabs, Tag.

**Before building anything, check whether a component already exists.** If it
does, match its structure. Building a bespoke accordion when the library has one
is the most common way a design system rots.

### Buttons

Three levels, all defined as 02 tokens:

- **Primary**: solid Shark background, white label, no stroke
- **Secondary**: transparent background, Shark stroke, Shark label
- **Tertiary**: text only, no background, no stroke

Hover darkens to Neutral 80 `#494949` (primary), or fills solid (secondary).
Disabled uses Neutral 40 background with Neutral 70 label. All three states are
tokenised, never compute a hover colour.

### Elevation

One shadow style exists: Dropshadow/Soft — blur 20, no offset, no spread, black
at 8%. There is no elevation scale. If something needs to lift off the page, it
uses that shadow or none at all.

---