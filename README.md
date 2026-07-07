# hrdlabs.org

Website for **HRD Labs** — we study optimization and world models (and we really like compute).

The site is a static, dependency-free site served through GitHub Pages (`CNAME` → hrdlabs.org). The design language is a minimal, y2k pixel-art terminal: every page is a path in the same shell (`~`, `~/team`, `~/research/...`), JetBrains Mono everywhere, and a family of pixel-cat sprites as the lab mascot. Light theme by default with a dark theme behind the sun/moon toggle (persisted in `localStorage`, shared across all pages including the research article).

## Structure

| Path | What it is |
| --- | --- |
| `index.html` | Main page (`~`): research log, team teaser, about, contact |
| `team.html` | Team page (`~/team`): the KRABS crossword with one pixel cat per member |
| `research.html` | Redirect stub to `team.html` (kept so old links don't break) |
| `research/interactive-world-models/` | Research article "Training-Free Interactive World Models" (static Astro export, restyled to the site theme) |
| `css/style.css` | Shared styles for the hand-written pages |
| `css/article.css` | Dark-terminal override theme applied on top of the article template's CSS |
| `assets/` | Pixel-art SVG sprites: masthead cat, sitting cat (`currentColor`, tintable), sleeping cat |

## Changelog

### 2026-07-07 — Article rewrite: plainer voice, verified facts, real ablations
- Rewrote the intro, results, and closing of the interactive-world-models article to match the team's own writing voice, dropping the marketing framing.
- Corrected the method description against the actual code (github.com/bryandong24/SPED): the shipped interpolation is a **per-token slerp with min-jerk easing over a 4-chunk (~3 s) ramp**, not a plain linear interpolation; the chunkwise model uses **4 denoising steps**, not 5; added resolution (480×832 @ 16 fps), umT5-xxl conditioning, and the 21+3 sliding window to Setup.
- **SPEED is now credited as Xiao et al. (arXiv:2605.18736)** with the team's causal-streaming port described (RoPE striding + full-res cache commits) and the measured 22.2 → 24.3 FPS result with honest context.
- Expanded "What didn't work" with the real experiment log (window shrinking, LongLive-style KV backfill, cache surgery variants, α/β sweeps).
- Footer now credits the hackathon sponsors, the $50,000 grand prize win, and links the code repo. `llms.txt` regenerated to match.

### 2026-07-07 — Light mode by default + interactive mascot
- **Light theme added and made the default**, with the previous dark look one toggle away. Both palettes live as CSS variables in `css/style.css` (site) and `css/article.css` (article template overrides); the choice persists via `localStorage` and applies across every page.
- **Pixel sun/moon theme toggle** on the main page, team page, and article terminal bar. Mermaid diagrams re-render to match the active theme.
- **The masthead cat is alive now**: it blinks at random intervals, flicks its tail up on hover, and meows (`meow!`, `mrrp?`, `purrr`, `:3`) when clicked. Honors `prefers-reduced-motion`.
- All cat sprites now use `currentColor`, so they recolor with the theme (ink cat on light, chalk cat on dark).

### 2026-07-07 — Unified dark pixel-art UI across the whole site
- **Article pages now match the main site.** The research article was light-mode with system fonts; it is now permanently dark with the site palette and JetBrains Mono, done via CSS-variable overrides in `css/article.css` (the theme toggle was removed and the theme is pinned to dark).
- **Back navigation everywhere.** Articles get a terminal bar (pixel cat · `HRD Labs` · current path · `$ cd ~` back link); the team page gets a `$ cd ~` crumb.
- **Team page reachable from the main page** via a new `$ ls team/` row (`krabs/` + five tinted pixel cats).
- **Article hero fixed to actually reflect the work.** The decorative D3 galaxy banner was replaced with a live demo video from the system (meadow dog → winter wolf via mid-generation prompt injection).
- **Cleaned up leftover template chrome:** dead "Download PDF" cell and Hugging Face Pro upsell removed, JSON-LD publisher corrected to HRD Labs, favicon added.
- **New pixel-art assets:** tintable sitting cat and a sleeping cat, used for the team pages and about section.
- `research.html` renamed to `team.html` (redirect kept), and the article's palette-helper script path fixed to its real location (it previously pointed at an untracked symlink that GitHub Pages would 404).

### Earlier
- Front page redesign: pixel-cat masthead, darker palette, slower cursor.
- First research article published: Training-Free Interactive World Models.
- Initial single-page dark lab-notes design.
