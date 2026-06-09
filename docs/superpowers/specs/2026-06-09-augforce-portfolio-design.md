# Design: augforce Portfolio Site

**Date:** 2026-06-09
**Repo:** `augforce/maugustine.github.io` (to be renamed `augforce.github.io`)
**Status:** Approved design — ready for implementation plan

## Summary

A single-page, dark, technical portfolio for Michael Augustine, framed for
**freelance / consulting clients** in the AI-automation, cloud, and
security-compliance space. Built with **Jekyll** so it deploys natively on
GitHub Pages, with content stored as data (YAML) and rendered through small
reusable templates. No CSS framework, minimal vanilla JavaScript.

## Goals

- Convert visiting freelance leads: communicate what Michael does, show proof
  (real shipped projects), and make contact frictionless.
- Lead with the freelance niche: security/compliance and AI/RAG work up top.
- Be fast, accessible, responsive, and trivial to maintain (add a project =
  edit one YAML file).

## Non-goals (YAGNI)

- No blog / CMS.
- No server-side contact form (use `mailto:` + profile links).
- No analytics, no JS framework, no CSS framework.
- No private/sensitive tooling shown (the non-public "Security Review Agent"
  is intentionally omitted).

## Hosting & URL

- The repo will be **renamed to `augforce.github.io`** so GitHub Pages serves
  it at the clean root URL `https://augforce.github.io/`.
  - Renaming a GitHub repo auto-redirects the old URL, so the existing clone's
    remote keeps working after the rename.
- Because it becomes a **user site at the domain root**, Jekyll config uses:
  - `url: "https://augforce.github.io"`
  - `baseurl: ""` (empty — no path prefix)
  - All asset references use `{{ '/path' | relative_url }}` so a future move to
    a custom domain needs no template changes.
- A custom domain can be attached later via a `CNAME` file with no other code
  changes.

## Tech approach

- **Jekyll** (GitHub Pages native build — push to `main`, Pages builds it).
- **No CSS framework** — one hand-written stylesheet using CSS custom
  properties for the theme palette.
- **Vanilla JS only** — smooth-scroll, scroll-reveal fade-ins (IntersectionObserver),
  mobile nav toggle. Site is fully functional with JS disabled.

## File structure

```
augforce.github.io/
├── _config.yml              # site metadata, contact values, build config
├── index.html               # assembles section includes in order
├── _layouts/
│   └── default.html         # <head>, nav, {{ content }}, footer, asset links
├── _includes/
│   ├── nav.html             # sticky top nav + mobile toggle
│   ├── hero.html            # name, tagline, value prop, CTA
│   ├── skills.html          # grouped skill tags (loops _data/skills.yml)
│   ├── projects.html        # project cards (loops _data/projects.yml)
│   └── contact.html         # mailto + profile links
├── _data/
│   ├── skills.yml           # skill groups
│   └── projects.yml         # project cards (single source of truth)
├── assets/
│   ├── css/style.css        # dark theme, responsive
│   └── js/main.js           # nav toggle, scroll-reveal, smooth-scroll
└── docs/superpowers/specs/  # this design doc
```

## Sections

### 1. Hero / About
- Name: **Michael Augustine**.
- Tagline: **"AI Ops Engineer & AI Automation Consultant."**
- One-line value prop aimed at clients: building HIPAA-aware AI automation and
  secure cloud workflows that ship to production.
- 2–3 sentence bio (13+ yrs infrastructure, Azure + GCP certified, focus on
  applied AI for regulated/SMB environments).
- Primary CTA button → Contact section.

### 2. Projects
Cards rendered from `_data/projects.yml`, in this order (security/compliance and
RAG first, MLB last). Each card: title, problem→outcome blurb, tech tags, and a
"View on GitHub" link.

1. **audit-webapp** — Google Workspace login-audit PDF reports generated from
   BigQuery logs. Two-layer auth, idle-timeout sessions, cost-capped queries,
   ReportLab PDFs with embedded maps. *Tech: FastAPI, Cloud Run, BigQuery, ReportLab.*
2. **google-workspace-security-audit** — Self-hosted Workspace security auditor;
   enterprise-tier posture insights without the enterprise upgrade.
   *Tech: Python, Google Admin SDK.*
3. **scout-it-assistant** — "Scout," an IT-support assistant doing RAG over a
   Google Drive knowledge base. *Tech: FastAPI, HTMX, Chroma, Claude.*
4. **document-rag-readiness-grader** — QA tool that scores documents for
   RAG-ingestion quality before they degrade an index. *Tech: Python, LLM.*
5. **custom-librechat-demo** — LibreChat configured to route staff to the best
   model per task — removes model-selection guesswork. *Tech: LibreChat, multi-model.*
6. **path-to-purpose-case-study** — Engineering case study: a Hellenistic
   astrology lead-magnet built for a client. *Tech: Cloudflare Pages, Claude API, GeoNames.*
7. **mlb-pitch-predictor** *(bottom)* — ML model predicting pitch type, trained
   on 4,000+ pitches with drift analysis. *Tech: Vertex AI, Python.*

### 3. Skills
Grouped tag clusters from `_data/skills.yml`:
- **Cloud & Infrastructure** — GCP, Azure, Cloud Run, Cloudflare, BigQuery, 13+ yrs infra.
- **AI & Automation** — Claude / OpenAI APIs, RAG, agents, n8n, Vertex AI.
- **Security & Compliance** — HIPAA, SOC 2, Google Workspace security.
- **Languages & Frameworks** — Python, FastAPI, HTMX.
- **Certifications** — Azure certified, GCP certified.

### 4. Contact
- Channels rendered from `_config.yml` values (so they live in one place):
  `email`, `github` (github.com/augforce), `linkedin`, `upwork`.
- Email is a `mailto:` link; the rest are external profile links.
- Actual email / LinkedIn / Upwork URLs are supplied by Michael during
  implementation and stored as `_config.yml` keys; GitHub is `augforce`.

## Visual design system

- **Palette (dark):** deep near-black background (`~#0d1117`), slightly raised
  card surface (`~#161b22`), light-gray body text (`~#c9d1d9`), one accent color
  for links/CTAs/active states (default cyan-green `~#39d3bb`; confirm during build).
- **Typography:** a clean sans for body/headings; a **monospace** face for the
  tagline, section labels, and skill/tech tags to give the technical feel.
- **Layout:** centered max-width content column, generous vertical spacing
  between sections, project cards in a responsive grid (1 col mobile → 2–3 cols
  desktop).
- **Motion:** subtle scroll-reveal fade/slide on sections (IntersectionObserver),
  hover lift + accent border on project cards. Respect `prefers-reduced-motion`.
- **Nav:** sticky top bar with anchor links to each section; collapses to a
  toggle on mobile.

## Accessibility & performance

- Semantic HTML landmarks (`header`, `nav`, `main`, `section`, `footer`),
  sufficient color contrast, visible focus states, `alt` text on any images.
- No render-blocking third-party assets; self-hosted or system fonts preferred.
- Honors `prefers-reduced-motion`.

## Deploy

1. Rename repo to `augforce.github.io`.
2. Push site to `main`.
3. Repo **Settings → Pages** → source = `main` branch (root).
4. GitHub builds and serves at `https://augforce.github.io/`.

## Verification

- Local preview with `bundle exec jekyll serve` if Ruby/Bundler is available;
  otherwise verify on the live Pages build after push.
- Manual checks: all four sections render, all seven project links resolve to
  the correct repos, mobile nav toggles, layout holds at mobile/tablet/desktop
  widths, and the page works with JavaScript disabled.

## Rough implementation milestones

1. Jekyll scaffold + `_config.yml` + `default.html` layout + base dark CSS.
2. Hero + nav.
3. `projects.yml` data + projects include + card styles.
4. `skills.yml` data + skills include.
5. Contact include + footer.
6. JS interactions (nav toggle, scroll-reveal, smooth-scroll) + reduced-motion.
7. Responsive pass + accessibility pass.
8. Rename repo, enable Pages, verify live.
