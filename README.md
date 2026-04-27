# US Design System — tokens

Design tokens exported from Figma in **Design Tokens Community Group (DTCG)** JSON format. Use them to keep product UI aligned with design across codebases, tools, and AI-assisted workflows.

## Repository contents

| Path | Description |
|------|-------------|
| `01. Primitive Tokens/Mode 1.tokens.json` | Base colors, spacing scale, typography (families + weights) |
| `02. Color Tokens/` | Semantic colors per theme: `Light`, `Dark`, `Grey`, `Color` |
| `03. Document Tokens/` | Layout: page width, margins, grid — `Desktop` and `Mobile` |
| `04. Number Tokens/` | Component spacing, radii, type scale (px) — `Desktop` and `Mobile` |
| `DESIGN_SYSTEM_AGENT.md` | Single-file brief for **coding agents** (summarized tokens + implementation checklist) |

Numeric values in the JSON are typically **pixels** as defined in Figma.

## Quick start

### 1. Use the agent brief (recommended for AI tools)

If you use Cursor, ChatGPT, Copilot, or similar to implement UI:

1. Open or attach [`DESIGN_SYSTEM_AGENT.md`](./DESIGN_SYSTEM_AGENT.md) in the conversation, or add it under **Project / Cursor rules** so the model always sees it.
2. That file maps tokens to **hex**, **typography**, **layout**, and **Light/Dark** semantics without requiring the model to parse every JSON file.

### 2. Consume raw JSON in your app

**Option A — Style Dictionary**  
Point [Style Dictionary](https://amzn.github.io/style-dictionary/) at these files (you may need a preprocessor to flatten Figma’s nested keys and strip `$extensions`). Output CSS variables, JSON for React Native, SCSS, etc.

**Option B — Tailwind**  
Map token paths to `theme.extend.colors`, `spacing`, `fontSize`, `borderRadius` in `tailwind.config`. Use a small script to read DTCG JSON and generate the config, or maintain a hand-written map from the agent brief.

**Option C — CSS custom properties**  
Define `--color-*`, `--space-*`, etc. by hand or with a build step. The starter block in `DESIGN_SYSTEM_AGENT.md` shows a minimal Light-theme pattern; duplicate for Dark using `02. Color Tokens/Dark.tokens.json`.

**Option D — Design token tools**  
Tools that support DTCG (e.g. [Tokens Studio](https://tokens.studio/) pipelines, internal design ops) can import these files directly if their Figma extensions are compatible.

### 3. Theming

- **Color:** Choose a file under `02. Color Tokens/` (`Light`, `Dark`, `Grey`, `Color`). Semantic paths (e.g. `Content.Heading`, `Button.Default State`) stay consistent; resolved colors change per file.
- **Responsive layout & type:** `03. Document Tokens` and `04. Number Tokens` split **Desktop** vs **Mobile**. At build time you can emit two sets of variables, or merge with media queries (`@media (min-width: …)`) using your chosen breakpoint.

### 4. Updating tokens

1. Change variables in Figma and export **variables to JSON** (or your team’s standard export) into this repo.
2. Replace the matching `*.tokens.json` files.
3. Regenerate any derived assets (CSS, Tailwind theme, iOS/Android) from your pipeline.
4. Commit with a short note (e.g. “Sync tokens from Figma — [date or release]”).

## Git workflow

```bash
git clone <your-remote-url>
cd us-design-system
# edit tokens or documentation
git add .
git commit -m "Describe your change"
git push
```

After `git init`, add a remote when you have one:

```bash
git remote add origin <your-repo-url>
git push -u origin main
```

## License and usage

Add a `LICENSE` file and team policy as needed. Until then, usage is governed by your organization’s rules for this project.

## See also

- [`DESIGN_SYSTEM_AGENT.md`](./DESIGN_SYSTEM_AGENT.md) — **implementation brief for developers and AI agents**
- [DTCG format](https://design-tokens.github.io/community-group/format/) — token file structure
