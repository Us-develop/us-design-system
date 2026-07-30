# Figma sync workflow

The live design system lives in Figma. This repository mirrors it for code and AI tooling.

## Source file

| | |
|---|---|
| **Name** | Us - Design System |
| **File key** | `ObyTQ40kofwt9Ve44lzAQv` |
| **URL** | https://www.figma.com/design/ObyTQ40kofwt9Ve44lzAQv |

## What maps to what

| Figma | Repository file | Editable? |
|---|---|---|
| Variables (01–04 collections) | `us-tokens.css` | **No** — regenerate |
| Components, patterns, rules | `us-design-system.md` | Yes — update when Figma behaviour changes |
| Presentation / deck rules | `skills/aboutus-brand-guidelines/` | Yes — keep aligned with `us-design-system.md` |

**Rule:** If Figma and this repo disagree, **Figma wins**. Change the variable in Figma, regenerate `us-tokens.css`, commit.

## Regenerating `us-tokens.css`

1. Open **Us - Design System** in Figma.
2. Export or generate CSS from the current variables (your team's export pipeline — Tokens Studio, Figma Variables API, or internal script).
3. Replace `us-tokens.css` in this repo. Do not hand-edit token values.
4. Update the generation comment at the top of the file if your pipeline supports a date or commit hash.
5. Sync the copy inside `skills/aboutus-brand-guidelines/assets/us-tokens.css` if that skill bundles tokens.
6. Commit: `Sync tokens from Figma — YYYY-MM-DD`.

The CSS file header documents the naming transform (Figma path → `--kebab-case` variable).

## Cursor integration

Projects that consume this repo should:

1. Copy or link `us-tokens.css` (e.g. `design-system/us-tokens.css`).
2. Copy `.cursor/rules/us-design-system.mdc` or reference this repo's rule.
3. Import `us-tokens.css` once at the app root.

## Checking for drift

Before a release or after a Figma variables change:

- Diff `us-tokens.css` against a fresh export.
- Review `us-design-system.md` §10 (Known gaps) for items still stale in Figma (e.g. icon text styles).
- Confirm Adobe Fonts kit domains include staging/preview hosts if typography looks wrong locally.

## Related Figma files

- **Us Website 2.0** — product layouts; section naming is still generic (see known gaps in `us-design-system.md`).
