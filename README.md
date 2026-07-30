# US Design System 3.0

Design tokens and build rules for Us (About-us.be) products, synced from the live Figma library.

**Figma source of truth:** [Us - Design System](https://www.figma.com/design/ObyTQ40kofwt9Ve44lzAQv) (`ObyTQ40kofwt9Ve44lzAQv`)

If Figma and this repo disagree, **Figma wins**. See [`FIGMA.md`](./FIGMA.md) for the sync workflow.

---

## Repository contents

| Path | Description |
|------|-------------|
| [`us-tokens.css`](./us-tokens.css) | **Token values** — CSS custom properties generated from Figma. Do not hand-edit. |
| [`us-design-system.md`](./us-design-system.md) | **Build rules** — typography, colour, layout, components, non-negotiables |
| [`.cursor/rules/us-token-enforcement.mdc`](./.cursor/rules/us-token-enforcement.mdc) | **Required Cursor rule** — tokens/fonts only; stop and ask if undefined |
| [`.cursor/rules/us-design-system.mdc`](./.cursor/rules/us-design-system.mdc) | Full Cursor rule (always-on) for AI-assisted UI work |
| [`PROJECT_SETUP.md`](./PROJECT_SETUP.md) | Bootstrap checklist for new projects |
| [`skills/aboutus-brand-guidelines/`](./skills/aboutus-brand-guidelines/) | Agent skill for presentations, decks, and branded deliverables |
| [`FIGMA.md`](./FIGMA.md) | How to regenerate tokens when Figma changes |
| [`legacy/`](./legacy/) | Archived DTCG JSON exports (superseded by `us-tokens.css`) |

---

## Quick start

**Default profile: Web.** Cursor and digital projects use Owners, IvyPresto
Display, and Public Sans. Presentation (Archivo) applies only when you explicitly
ask for a deck or presentation deliverable.

### Web / React / HTML

1. Copy or submodule this repo into your project.
2. Import the tokens once at the app root:

```html
<link rel="stylesheet" href="https://use.typekit.net/dbo7deg.css">
<link rel="stylesheet" href="https://use.typekit.net/rgx8kmt.css">
<link rel="stylesheet" href="/path/to/us-tokens.css">
```

3. Use semantic tokens only — never raw hex or primitive colours:

```css
.card {
  background: var(--page-page-background);
  color: var(--content-body);
  border-radius: var(--radius-radius-cards-lg);
}
```

4. Switch colour mode and theme on section wrappers:

```html
<section data-us-mode="dark">...</section>
<section data-us-theme="purple">...</section>
```

5. **Presentation only on request** — set `data-us-fonts="presentation"` and load
   Archivo only when building decks or slide exports, not for normal web apps.

### Cursor / AI agents

**Web profile is the default.** Agents should use Owners + IvyPresto + Public Sans
unless you explicitly ask for a presentation.

**Every new project must include** the token enforcement rule before any UI work:

```
design-system/us-tokens.css
design-system/us-design-system.md
.cursor/rules/us-token-enforcement.mdc   ← required
```

Optional: copy `.cursor/rules/us-design-system.mdc` for the full rule set.

Full bootstrap steps: [`PROJECT_SETUP.md`](./PROJECT_SETUP.md).

**Policy:** Only tokens and rules from this design system may be used — no other
fonts, colours, or styling. If something is not defined, **stop and ask**; do not
invent values or continue building affected UI.

Read [`us-design-system.md`](./us-design-system.md) §0 (Token-only policy) and §1
(Non-negotiables) before any UI work.

### Presentations / Claude

Install the skill from [`skills/aboutus-brand-guidelines.skill`](./skills/aboutus-brand-guidelines.skill) or use the extracted folder under `skills/aboutus-brand-guidelines/`.

---

## Updating tokens

1. Change variables in **Us - Design System** (Figma).
2. Regenerate `us-tokens.css` via your export pipeline.
3. Replace the file in this repo (and the copy in `skills/.../assets/` if bundled).
4. Commit: `Sync tokens from Figma — [date]`.

Full steps: [`FIGMA.md`](./FIGMA.md).

---

## Git workflow

```bash
git clone git@github.com:Us-develop/us-design-system.git
cd us-design-system
git checkout -b feature/your-change
# edit us-design-system.md or regenerate us-tokens.css from Figma
git add .
git commit -m "Describe your change"
git push -u origin feature/your-change
```

---

## See also

- [`us-design-system.md`](./us-design-system.md) — full implementation brief
- [`FIGMA.md`](./FIGMA.md) — Figma file link and regeneration workflow
- [`legacy/README.md`](./legacy/README.md) — archived DTCG JSON format
