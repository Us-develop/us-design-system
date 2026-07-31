# Project setup — Us Design System 3.0

Use this checklist when **creating any new project** that should follow the Us
brand. Complete it before writing UI code.

## 1. Add design system files

From [Us-develop/us-design-system](https://github.com/Us-develop/us-design-system):

```
your-project/
  design-system/
    us-tokens.css              ← copy from repo root
    us-design-system.md        ← copy from repo root (reference for humans + agents)
  .cursor/rules/
    us-token-enforcement.mdc   ← copy from this repo (required)
    us-design-system.mdc       ← optional; full rules (large)
```

Or add the design system repo as a **git submodule**:

```bash
git submodule add git@github.com:Us-develop/us-design-system.git design-system
cp design-system/.cursor/rules/us-token-enforcement.mdc .cursor/rules/
```

## 2. Import tokens and fonts

**Default — Web / digital product** (use for all Cursor web projects unless the
user explicitly asks for a presentation):

```html
<link rel="stylesheet" href="https://use.typekit.net/dbo7deg.css">
<link rel="stylesheet" href="https://use.typekit.net/rgx8kmt.css">
<link rel="stylesheet" href="/design-system/us-tokens.css">
```

Also load Public Sans, Material Symbols Outlined, and Font Awesome 6 Brands as
your stack requires — see `us-design-system.md` §3.

Checklist:

- [ ] Material Symbols Outlined loaded (see `us-design-system.md` §3)
- [ ] Reusable Icon component uses `--typography-font-icons` and icon axis tokens
- [ ] Feedback UI uses `--color-system-*` only (no emoji, no custom alert hex)

**Presentation / deck HTML** — **only when explicitly requested.** Add
`data-us-fonts="presentation"` on `<html>` and load Google Fonts (Archivo stack)
per `us-design-system.md` §3. Do not use this profile for normal web apps.

## 3. Enforce token-only styling

The Cursor rule **`us-token-enforcement.mdc`** must be present with
`alwaysApply: true`. It instructs agents to:

- use **only** `us-tokens.css` and `us-design-system.md` for styling
- use **only** documented font stacks — no other typefaces
- **stop and ask** if something is not defined — never invent values

Review `us-design-system.md` §0 (Token-only policy) with the team.

## 4. Map your stack (if applicable)

**Tailwind** — map `theme.extend` from CSS variables; do not duplicate hex values.

**React / Vue / etc.** — prefer `var(--token-name)` in CSS modules or a thin token
wrapper. Do not hard-code design values in components.

## 5. Blockers — ask first

If the project needs styling not covered by the design system, **do not proceed**
until:

- Figma is updated and `us-tokens.css` is regenerated, or
- a designer gives an explicit exception documented in the project

Common gaps are listed in `us-design-system.md` §10 (Known gaps).

## 6. Stay in sync

When Figma variables change, pull the latest `us-tokens.css` from the design
system repo. See [`FIGMA.md`](./FIGMA.md).
