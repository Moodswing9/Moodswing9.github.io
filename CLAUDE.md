# CLAUDE.md — Moodswing9.github.io

## What This Is

A single-file developer portfolio hosted on GitHub Pages. No build step, no framework, no dependencies — just `index.html`.

URL: https://moodswing9.github.io

## Editing

```bash
# Open locally
start index.html          # Windows
open index.html           # macOS

# Deploy — just push to main
git add index.html
git commit -m "..."
git push origin main
# GitHub Pages auto-deploys in ~30 seconds
```

## Architecture

Everything is in `index.html`. Structure:

| Section | What it is |
|---|---|
| `<head>` | GA4, SEO meta, Open Graph, Twitter Card, Google Fonts, all CSS in `<style>` |
| Nav | Fixed top bar — logo + GitHub link |
| Hero | Name, title, CTA buttons, avatar |
| Featured Work | 5 project cards (backup-log-analyzer, networker-ppdm, claude-deck-generator, ppdm-es-troubleshooter, ppdm-watch) |
| GitHub Repositories | Repo cards with tags and descriptions |
| Stats bar | Live GitHub stats (repos, stars) fetched from GitHub API |
| Footer | Links |
| `<script>` | GitHub API fetch at bottom of `<body>` |

## Design System

CSS custom properties on `:root`:

```css
--bg: #080b0f          /* page background */
--surface: #0e1318     /* card background */
--border: #1a2030      /* card borders */
--accent: #a855f7      /* purple — primary accent */
--accent2: #7c3aed     /* deeper purple — hover states */
--text: #c8d6e5        /* body text */
--muted: #4a5568       /* secondary text, tags */
--white: #f0f4f8       /* headings */
```

Fonts: `JetBrains Mono` (body/code) + `Syne` (display headings) — loaded from Google Fonts.

## Live GitHub Stats

At the bottom of `<body>`, a small inline `<script>` fetches from the GitHub API and populates two `<span>` elements:

```html
<span class="stat-num" id="stat-repos">5</span>   <!-- public_repos -->
<span class="stat-num" id="stat-stars">—</span>   <!-- sum of stargazers_count -->
```

If the API call fails (rate limit, network), the hardcoded fallback values remain. The stat for repos is hardcoded as `5` by default — update this if repo count changes before the API loads.

## Adding a New Project

Two places need updating:

1. **Featured Work section** — add a `.project-card` div in the 2×2 grid
2. **GitHub Repositories section** — add a `.repo-card` anchor

Also update the `stat-repos` fallback value and the README badge if the public repo count changes.

## Key Constraints

- **No external JS or CSS** — the `zero dependencies` claim on the portfolio is literal. All styles are inline in `<style>`, all logic is in the single `<script>` block. Do not add CDN links.
- Google Fonts is the only external load — acceptable as it's a font, not a script.
- GA4 tag `G-9BM08V94LW` is hardcoded — do not change it.
- Canonical URL is `https://moodswing9.github.io/` — keep the trailing slash.
- GitHub Pages serves only `main` branch — all deployments go directly to `main`, no staging branch.
- Open Graph image points to `https://github.com/Moodswing9.png` — the GitHub avatar, no local asset needed.

## Files

```
index.html    # Entire site
README.md     # GitHub profile README (shown on github.com/Moodswing9)
LICENSE
```
