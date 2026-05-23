# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file static portfolio website (`index.html`) for Aditya Singh — a freelance Python/VBA automation developer. No build step, no bundler, no package manager, no dependencies beyond a Google Fonts CDN import.

## Development

Open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

There are no tests, linters, or CI pipelines. Validate changes visually in the browser, including the 768px mobile breakpoint (use browser DevTools device emulation).

## Architecture

Everything lives in one file with three sections: `<style>`, `<body>` (markup), and a `<script>` block at the bottom.

### Design tokens (CSS custom properties)

All colours and the font are declared as variables on `:root`:

| Variable | Value | Role |
|---|---|---|
| `--bg` | `#0a0a0a` | Page background |
| `--text` | `#f2f2f0` | Primary text |
| `--muted` | `#555` | Subdued labels/indices |
| `--muted2` | `#888` | Body copy, descriptions |
| `--accent` | `#00c896` | Brand green — CTAs, highlights |
| `--border` | `rgba(255,255,255,0.07)` | Hairline dividers |

Change colour or font only via these variables, not inline.

### Page sections

Sections follow a numbered editorial convention (`01 — Origin`, `02 — Work`, …) and are anchored by `id`: `#hero`, `#story`, `#projects`, `#skills`, `#contact`.

### Scroll-reveal animations

Elements start hidden (`opacity:0; transform:translateY(Npx)`) and gain the `.visible` class via an `IntersectionObserver` (threshold 0.1) defined at the bottom of `<script>`. To make a new element animate in on scroll, add it to the `querySelectorAll` selector list in that observer block.

### JavaScript responsibilities

The inline `<script>` handles exactly three things:
1. **Custom cursor** — dot (`#cursor`) + lagging ring (`#cursor-ring`) with `requestAnimationFrame` lerp; scales on hover over `a`/`button` elements.
2. **Scroll progress bar** — `#bar` width tracks `scrollY` percentage.
3. **Scroll-reveal** — `IntersectionObserver` adds `.visible` to targeted elements.

## Conventions

- **Buttons** use `.btn-main`; filled/primary variant adds `.btn-filled`.
- **Project rows** use the three-column grid: index → info block → arrow. Match this pattern for new projects.
- **Section numbers** are decorative spans with class `section-num`; always use the `NN — Label` format.
- **Privacy**: do not add personal details (employer names, private repos, addresses, phone numbers) to the file unless the user explicitly provides them for that purpose. The publicly visible contact info (email `singh.aditya.1work@gmail.com`, GitHub `TheWorkAi`) is intentionally public.
