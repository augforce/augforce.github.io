# Design: Portfolio Rebrand (sales page → showcase)

**Date:** 2026-06-24
**Repo:** `augforce/augforce.github.io`
**Status:** Approved — implementing directly, iterating from the live result

## Summary

Re-cut the existing Jekyll site from a **consulting / lead-generation page** into a
**professional showcase portfolio** built around Michael Augustine's résumé. The
visual design system (fonts, colors, cards, grid background, dark/light toggle) is
**unchanged** — this is a change to sections, order, and copy only.

Audience: **hiring managers / recruiters**, but the tone is "this is who I am, my
background, and what I build" — *not* an active job hunt. No availability badges, no
sales CTAs.

Identity is a **blend**: "AI Conductor" (the human brand) paired with the résumé
title "AI Platform Operations & Technical Enablement Specialist" (what he does).

## Structure (Approach B — work-first)

```
Hero / About → 01 Selected Work → 02 What I Do → 03 Capabilities
            → 04 Experience → 05 Education & Certifications → Contact
```

Nav links: **Work · Experience · Capabilities · Contact** (brand anchors to top).
The nav "Available" status dot is removed.

## Section details

### Hero / About
- Kicker (mono): `AI Conductor · AI Platform Operations & Technical Enablement`
- Headline: "I keep AI platforms running — and build the tools that make them useful."
- Lead: from the résumé summary (15+ yrs enterprise IT & AI; administers Microsoft
  Foundry end to end; builds AI tools with Claude Code / Anthropic API / MCP /
  agentic workflows).
- CTAs: `See the work` · `Résumé (PDF)` · `Get in touch`. (No "Start a project.")
- Meta strip: `15+ yrs enterprise IT & AI` · `Microsoft Foundry platform admin` ·
  `Claude Code · MCP · agentic workflows` · `St. Louis, MO`. No availability badge.

### 01 — Selected Work (`_data/projects.yml`, `_includes/projects.html`)
Descriptive engineering blurbs (not sales). Path to Purpose stays flagship. Cards:
1. **Path to Purpose** *(flagship)* — Cloudflare Pages + Functions, server-side API
   proxy, rate limiting, client-voice Claude output; GoHighLevel/GeoNames/Astrology.
2. **Career Intelligence** — deterministic job-fit scorer + optional LLM analysis
   layer (`augforce/career-intelligence`, Python).
3. **Workspace Security Auditor** — CLI scans, FastAPI dashboard, SQLite findings, 20 checks.
4. **Workspace Login Audit (MCP)** — conversational audit reports, PDFs, login maps; BigQuery.
5. **AI Compliance Agent** — third-party app review (HIPAA/PII/CVE/vendor risk).
   **Internal — no public repo** (card renders without a GitHub link).
6. **Scout — IT Support Assistant** — RAG over Google Drive, cited sources.
7. **RAG Readiness Grader** — scores docs for retrieval quality before indexing.
8. **Model-Routing Chat** — LibreChat routing staff to the best model per task.

Removed: **MLB Pitch Predictor**. Projects include gains a conditional: cards with no
`url` show a muted note instead of the "View on GitHub" link.

### 02 — What I Do (`_data/focus.yml`, `_includes/focus.html`)
Renamed from the old client "verticals". Reuses the left-accent card component for
three focus areas: **AI Platform Operations**, **AI Tool Building & Enablement**,
**Cloud, Data & Integrations**. Sales foot paragraph removed. Grid → `auto-fit` so
three cards lay out cleanly.

### 03 — Capabilities (`_data/skills.yml`, `_includes/skills.html`)
Tag clusters replaced with the résumé's four exact groups: AI Platform Operations ·
AI Tool Building & Enablement · Cloud, Data & Integrations · Applied AI Workflows.

### 04 — Experience (new: `_data/experience.yml`, `_includes/experience.html`)
Vertical timeline, three roles (current-most-relevant first):
Network Ninja (AI Ops & Tech Support Eng, Oct 2023–present) · Independent AI
Solutions Builder (Feb 2026–present) · Ferguson Florissant School District (Sr.
Technology Specialist, 2011–2023). Styled with existing card/border tokens.

### 05 — Education & Certifications (new: `_data/credentials.yml`, `_includes/education.html`)
Two columns. Education: DeVry (BS, CIS/Computer Forensics), CCAF (AAS, Information
Management). Certifications (reusing `.chips`): Claude API · Google Generative AI
Leader · Azure AI Engineer Associate · Azure AI Fundamentals.

### Contact (`_includes/contact.html`)
Keep banner image + mailto and links (Email · GitHub · LinkedIn · Résumé). **Drop
Upwork.** Retitle to "Get in touch"; replace the "available for new work" line with a
neutral one.

## Global / `_config.yml`
- `tagline` → `AI Conductor · AI Platform Operations & Technical Enablement`
- `description` → rewritten from the résumé summary
- add `location: "St. Louis, MO"`
- Downloadable résumé at `/assets/files/Michael-Augustine-Resume.pdf` replaced with
  the latest PDF (done).

## CSS (`assets/css/style.css`)
Additive, reusing existing tokens: `.timeline`/`.job*` (experience),
`.credentials`/`.edu*` (education & certs), `.card__link--muted` (internal projects),
and a `.verticals` grid tweak (`auto-fit`). Responsive: credentials → 1 column on mobile.

## Verification
- `bundle exec jekyll build` (or serve) renders with no Liquid errors.
- All sections render; project links resolve; the internal card shows no broken link;
  résumé link downloads the new PDF; mobile nav and layout hold; works with JS off.

## Non-goals
- No change to fonts, palette, or component styling beyond the additive section CSS.
- No blog/CMS, no analytics, no JS framework.
