# Ultragoal: cmux-config GitHub Pages landing page (Stitch-generated)

## Goal
Ship a minimal but polished landing page for the `cskwork/cmux-config` repo, generated via Stitch MCP and hosted on GitHub Pages from the same repo's `/docs` folder on `main`.

## Context
- Repo: https://github.com/cskwork/cmux-config (public, created 2026-05-23)
- The repo currently holds a single `cmux.json` (cmux 0.64.9 file-managed config) and a `README.md`.
- The landing page exists so that the public URL of the repo is more inviting than a bare README — it should pitch what the repo is, who it's for, and how to use it.

## Audience
- macOS users evaluating or already running [manaflow-ai/cmux](https://github.com/manaflow-ai/cmux) who want a starting-point config file they can drop into `~/.config/cmux/cmux.json`.

## Hosting decision (locked)
- Single repo, `main` branch, GitHub Pages source = `/docs` folder.
- Final live URL: https://cskwork.github.io/cmux-config/

## Content scope (Minimal — locked)
The page should contain:
1. **Hero**: name (cmux-config), one-line value prop, primary CTA = "View on GitHub" linking to the repo.
2. **What it is**: 1–2 short paragraphs explaining that this is a portable, file-managed cmux config snapshot, separated from the in-app plist state.
3. **Install snippet**: copy-pasteable shell block:
   ```sh
   mkdir -p ~/.config/cmux
   curl -fsSL https://raw.githubusercontent.com/cskwork/cmux-config/main/cmux.json \
     -o ~/.config/cmux/cmux.json
   ```
   plus a note about `cmd+shift+,` (Reload Configuration) inside cmux.
4. **What is overridden**: a small table mirroring the README's active overrides (`app.appearance: "dark"` for now).
5. **Footer**: link to cmux upstream, link to the JSON Schema URL, "tested with cmux 0.64.9 (89)".

## Design tone (locked)
- **Modern dev-tool dark** (Vercel / Linear / Geist aesthetic).
- Near-black background, generous whitespace, monospace accents for code, subdued primary color, sans-serif body (Geist / Inter / DM Sans family).
- No emoji. No stock illustrations. Distinctive — not generic AI-template feel.

## Quality bar (final-gate evidence)
- HTML validates, no broken links, install snippet exact-match with repo state, page renders on mobile widths.
- `ai-slop-cleaner` clean. `verification` clean (live URL returns 200, expected title, expected install block string present). `$code-review` APPROVE + CLEAR.

## Stories (proposed)

- **G001 — Stitch design + screen generation**
  Create a Stitch project, configure a `Modern dev-tool dark` design system (dark color mode, Geist/Inter body, low roundness, monochrome/neutral accent), then `generate_screen_from_text` for the landing page using the content scope above. Capture screen id.

- **G002 — Extract to static HTML/CSS**
  Use Stitch's `extract-static-html` capability (or `code-to-design` / generate code path) to pull self-contained HTML + CSS out of the generated screen. Land output under `docs/` in the local repo working tree. No external runtime dependencies beyond what Stitch emits.

- **G003 — Localize content + polish**
  Edit copy/links so they match the locked content scope (real repo URL, exact install snippet, real overrides table, real cmux version). Verify no Lorem Ipsum, no placeholder hrefs, no broken asset paths. Render `docs/index.html` in the local browser (claude-in-chrome) and visually verify hero + install block + table read correctly at desktop and ~390px widths.

- **G004 — Publish + enable Pages + verify live**
  Commit `docs/` to `main`, push to `cskwork/cmux-config`, enable GitHub Pages with source = `main` branch / `/docs` folder (via `gh api`), wait for build, then curl the live URL and confirm 200 + expected title string + expected install snippet substring.

- **G005 — Final gate (mandatory)**
  Run `ai-slop-cleaner`, rerun `verification` (live URL + content checks), run `$code-review` on the diff. Pass `--quality-gate-json` with APPROVE + CLEAR on all three before clearing the Claude `/goal`.

## Out of scope
- Custom domain / DNS.
- Analytics / cookies / consent banner.
- Multi-page docs site, blog, changelog page.
- JS framework bundles.
