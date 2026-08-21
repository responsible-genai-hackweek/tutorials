# Slide Deck — Agent Context

This directory contains slides for "Landscape of Coding Agents," a 90-minute tutorial at the NASA Responsible GenAI HACK Week (August 2026). The tutorial is conceptual and lecture-based with one interactive exercise (a Google Form audience survey at the ~30 minute mark). There is no live demo.

## Repository layout

- `content/` — first-pass slide HTML files (text and structure only, no images)
- `content-with-visuals/` — second-pass slide HTML files (adds photos, diagrams, and icons)
- `assets/` — shared images, fonts, and diagram source files
  - `assets/diagrams/` — extracted diagrams from Jason Gilman (Element 84), used with attribution
- `shared/` — shared header/footer HTML (design tokens, navigation JS, font loading)
- `build/` — final output; `index.html` is the assembled presentation

## Key files

- **`topic-inventory.md`** — a summary of topics being taught across the 5-day HACK Week. Provides curriculum context for how this tutorial connects to subsequent sessions.
- **`SLIDES.md`** — the primary design brief. It defines the deck's content, slide order, speaker notes, and layout guidance. Start here when adding or revising slides.
- **`VISUALS.md`** — governs the second pass; specifies photographs, diagrams, and iconographic elements to add to existing slides after the first pass is complete. Includes attribution requirements for reused diagrams.
- **`mapping-exercise.md`** — specification for a Google Form audience survey used during the tutorial.
- `build.sh` — stitches all HTML files in `content/` into `build/index.html` (ordered by SLIDES.md)
- `build-visuals.sh` — does the same for `content-with-visuals/` with fallback to `content/`
- `publish.sh` — produces a self-contained HTML file with inlined images

## Two-pass workflow

1. **First pass:** Use `SLIDES.md` to generate slides in `content/`. Typography, layout, color, and accent only — no images or decorative icons.
2. **Second pass:** Use `VISUALS.md` to generate enhanced versions in `content-with-visuals/`. This pass is additive; do not modify first-pass files.

**Before editing any slide**, check whether a file exists in `content-with-visuals/` for that slide. If it does, edit that file — `build-visuals.sh` uses it in preference to `content/`. Only edit `content/<slide>.html` if no corresponding file exists in `content-with-visuals/`.

## Design standards

All slides must follow the `uw-slides` plugin conventions in Claude Code. When in doubt about design decisions, consult that plugin for authoritative guidance on color tokens, typography, layout patterns, and logo usage.

## Attribution

Diagrams sourced from Jason Gilman (Element 84) must carry a visible footer credit on the slide where they appear. See VISUALS.md for specific attribution format.
