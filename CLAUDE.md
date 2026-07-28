# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Marketing site for **KADRI** — a productized web studio in Tbilisi that builds portfolio websites for photographers only. This repo is the studio's *own* site plus concept demos, not a client project. `PRD.md` is the source of truth for the business and product decisions; read it before changing copy, pricing, or structure.

There is **no build system, package manager, git repo, test suite, or lint config**. The deliverables are hand-authored, self-contained HTML files. To preview, open the file directly in a browser (`file://`) — everything is inline, so no server is required. To deploy, upload the HTML files as-is to any static host.

## Files that ship

- `index.html` — the KADRI studio landing page (hero, packages, process, FAQ, lead form).
- `concept-wedding.html` — concept demo: a **fictional** wedding photographer ("Tamar Beridze"), showing the by-couple story-gallery structure.
- `concept-commercial.html` — concept demo: a **fictional** commercial photographer ("Luka Meladze"), showing the flat-nav case-study structure.

`index.html`'s work grid links to the two concept pages (slots 01/02); slot 03 is a live "open founding slot."

## Reference assets (not part of the site — do not deploy)

- `PRD.md` — product requirements; the authority for all business/design decisions.
- `photography-portfolio-benchmark_1.html` / `.pdf` — a benchmark of 8 real photographer sites and the **six patterns every good one shares**. This is the quality bar the concept builds and any new page must meet.
- `*.webp`, `screencapture-*.png` — visual references (a conversion-template mockup and competitor screenshots).

## Architecture & invariants

Each HTML page is a **single self-contained file**: all CSS in one `<style>`, all JS in one `<script>`, no external stylesheets/scripts/fonts/images. Preserve this — it lets pages open from `file://` and keeps them portable. Embed any asset as a data URI (the film-grain texture is already an inline SVG data URI).

**Bilingual contract (KA + EN).** Every user-visible string carries both `data-en` and `data-ka` attributes; the element's initial text is the EN default. A `setLang(lang)` function swaps them and persists the choice in `localStorage` under the key **`kadri-lang`** (shared across all three pages, so language follows the visitor between them). When adding any visible text, add both attributes or it won't translate.

- **innerHTML vs textContent gotcha:** the concept files' `setLang` renders a value with `innerHTML` when it contains a tag (`/<[a-z]/i`), else `textContent`. `index.html`'s `setLang` is `textContent`-only. Consequence: if an element has child HTML (e.g. a `<b>` or an `<a>`), that HTML **must be mirrored inside both `data-en` and `data-ka`** using single-quoted attributes (`<a href='index.html'>`), or toggling language will wipe it. This was a real bug in the concept footers — keep it fixed.
- Georgian strings are **unreviewed drafts** pending a native speaker. Flag them for review; do not silently "correct" Georgian.

**Currency & timezone are fixed.** All money is GEL (`₾`); all times are `Asia/Tbilisi` (UTC+4, no DST). Never introduce USD/EUR or UTC. The lead-form payload hardcodes `currency: "GEL"` and `timezone: "Asia/Tbilisi"`.

**Design tokens are duplicated, not shared.** The `:root` CSS variables (dark theme, gold `--gold` accent) are copied into each file — there is no shared stylesheet. A token or palette change must be applied to all three files to keep them reading as one system.

**Lead form.** In `index.html`, the form POSTs JSON to `N8N_WEBHOOK_URL` (top of the `<script>`). It is currently `""` (not wired); while empty the form **validates and reports honestly** ("not connected yet") instead of faking success. Do not make it appear to succeed when unwired. Wiring it to the real n8n webhook is a separate, later phase.

## Honesty invariants (business-critical, from PRD.md)

The studio's positioning is honesty on day one — the audience are photographers who spot fakes. Enforce these:

- **No fake clients, testimonials, logos, or stock photography.** Empty proof slots stay visibly empty ("founding slot open") until real content exists.
- **Concept pages must stay unmistakably fictional:** keep the sticky gold `CONCEPT BUILD` banner and the footer disclaimer naming the photographer/clients/quotes as invented. Never present them as real client work.
- Image areas are intentional `.ph` placeholder blocks; contact details are placeholders (`kadri.ge`/`example.com`). These get swapped for real values by the owner, not invented.
