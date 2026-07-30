# Presentations and .pptx

Read this before building any deck.

## What is sourced, and what is not

This file separates the two, because guessing at the gap is how decks go wrong.

**Sourced from Figma or the reference slides:** all colours, type sizes, line
heights, spacing, radii, the colour families, the dark/light sandwich, and the
casing rules.

**Not specified anywhere:** the eyebrow style, chart series colours and order,
the exact composition of each slide type, and image treatment. If a task needs
one of these, use the nearest existing token and say plainly that it is
unspecified. Do not invent a value and present it as the house style.

## What the reference set actually shows

Observable across the agency's own slides:

- Shark backgrounds carry openings, section breaks and closings; content slides
  run light.
- One theme per surface. Never two.
- Large heavy uppercase titles against generous empty canvas.
- Small headings, card titles and labels are sentence case.
- No accent bars, stripes or underlines anywhere.
- A short sentence-case line sometimes sits above an uppercase title.

Anything beyond that list has not been measured. Vary layouts across a deck;
repeating one layout is what makes a deck look automated.

## Self-check before delivering

- Is the title clearly heavier than everything else? If not, go to Archivo Black.
- Is anything small in uppercase? Card titles, eyebrows and labels are sentence case.
- Are card corners 24px?
- Does the slide have any colour? Only data-dense slides may be all grey.
- If a surface is coloured, is the text Theme-Dark of that same theme?
- Two themes on one slide? Reduce to one.
- Any letter-spacing anywhere? Remove it. The system has none.
- Did I invent a value that is not in the tokens? Remove it or flag it.

Replace the body of the existing `aboutus-brand-guidelines` skill with this
document. That skill is currently wrong on almost every specific: it names
Bricolage Grotesque as the heading font, gives Rajah as `#F4B860` (it is
`#FFB985`), Perfume as `#D4A5FF` (it is `#F3AAFF`), and tells Claude to make
buttons Lavender. Leaving it in place means every generated deck is off-brand.

Slide-specific rules:

**Casing.** Only the main slide title is uppercase. Everything smaller is
sentence case: eyebrows, card titles, column headers, labels, body. A card
headed "Zekerheid" is sentence case, not "ZEKERHEID". Uppercasing small
headings is the most common error in generated decks.

**Weight.** Slide titles are heavy. Use Archivo Black, or Archivo at 700 to
900. A title set at 500 or 600 reads as a subheading and flattens the whole
slide. If a title does not look noticeably heavier than everything else on the
slide, it is wrong.

**The eyebrow.** Reference slides do place a short line above an uppercase
title, and it is set in sentence case, with no tracking. That much is settled.
Its typeface, size, colour and vertical spacing are NOT defined in Figma and
NOT measurable from the screenshots. Do not invent them: use an existing body
style and flag that the eyebrow still needs a real spec.

**No tracking.** Never letter-space anything, and least of all the eyebrow.
Small uppercase labels with tracking are a generic deck convention, not this
system. Figma defines every style at 0.

**Corners.** Cards and panels use the large card radius, 24px. Not 8, not 12.
Small radii make the deck look like a default template. Only images use 12.

**Colour is required.** A slide in nothing but black, white and grey is
reserved for dense data: tables, dashboards, anything where colour would
compete with the numbers. Every other slide carries at least one element of
colour, whether that is a tinted card set, a coloured panel, or one of the
brand graphic elements. An all-grey card row is not the house style.

**Coloured surfaces use a theme.** Pick one theme per slide — Purple, Pink,
Green or Orange — fill from Theme-Light or Theme-Primary, and take the text
from Theme-Dark of that same theme. Never two themes on one slide.

Other slide rules:

- Title slides: Shark background, white heading, one brand colour as accent
- Content slides: white or one pastel tint background, never two tints together
- Headings on slides: **Archivo Black**, uppercase, matching the H1 or H2 ramp
- Quotes and alt headings: **Archivo Thin 100 or Light 300**, not a serif
- Body: Public Sans Light
- Chart series order is NOT specified in Figma. The order in the old brand
  skill was never sourced. Ask a designer before charting multiple series.
- Keep the 1180 of 1440 content ratio. On a 16:9 slide that is roughly a 10%
  margin each side

Presentations always run the Archivo profile. Owners and IvyPresto are for
digital products only, because a deck opens on machines nobody controls.

Two consequences to expect in a deck. Wide headings are not reproducible,
PowerPoint cannot render variable axes, so use Archivo Black at regular width
and do not fake Wide with letter-spacing. And quotes lose the serif contrast
they have on web, so the difference between an alt heading and a default one
rests entirely on weight.

### Fonts in a .pptx do not travel with the file

A `.pptx` stores font *names*. PowerPoint resolves them against fonts installed
on whatever machine opens the deck. Archivo being a free Google Font means it
is free to install, not that it is present. On a client laptop without it, every
heading falls back to Calibri and the deck stops being branded at the exact
moment it matters.

Two things to do about it:

1. **Install Archivo, Archivo Black, Archivo Narrow and Public Sans on every
   machine that opens or edits these decks.** Free, one-time, and it makes the
   source file correct internally.
2. **Send PDF, not .pptx.** A PDF embeds its fonts, so it renders identically
   everywhere. For a pitch deck this is normal practice anyway, and it removes
   the problem completely.

Send an editable `.pptx` outside the agency only when the client genuinely needs
to edit it. In that case accept that the typography will degrade on their
machine, or build that specific deck in Arial and Calibri and treat it as an
unbranded working file.

### Fallback fonts, and why a .pptx has no chain

CSS falls through a list. **A .pptx cannot.** A text run stores exactly one
font name, and the theme stores one major (heading) and one minor (body) font.
When that font is missing, the operating system substitutes something, and you
do not get to say what.

So "fallback font" in PowerPoint is not a chain. It is a decision about which
font to write into the file:

| | Heading | Body |
|---|---|---|
| Machines with the fonts installed | Archivo / Archivo Black | Public Sans |
| Anything else | **Franklin Gothic** | **Aptos** |

That means two template variants rather than one clever file. A branded one for
decks that stay on machines you control, and a safe one for anything leaving
the agency in editable form. Presenting from your own laptop and sending a PDF
avoids the question entirely, which is why that stays the default advice.

**One caveat on Aptos.** It became the Office default in 2023 and ships with
Microsoft 365, so most corporate clients have it. Older perpetual Office
installs (2019, 2021) do not, and there it substitutes again to something
neither of you chose. Franklin Gothic does not have this problem, it has
shipped with Windows and Office for years.

If you want the body fallback to be genuinely bulletproof, use Calibri instead
of Aptos: it has been in Office since 2007 and is present everywhere Aptos is,
plus everywhere Aptos is not. It costs nothing and removes the only remaining
soft spot. Your call, and Aptos is what the tokens currently say.

A last consequence: automated visual checks render through LibreOffice, which
substitutes fonts it does not have. Text-fit checks on Archivo are approximate,
so leave roughly 10% slack in any container where overflow would be visible.
The same applies to Aptos, which has no metric-compatible substitute in most
preview environments.

---