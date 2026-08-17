# Landscape of Coding Agents

Tutorial slides for a 90-minute session at the NASA Responsible GenAI HACK Week (August 2026). This tutorial orients participants to the technology underneath AI coding tools, providing a shared mental model for the rest of the week.

## Instructors

- Anthony Arendt
- Anshul Tambay
- Don Setiawan

## Building the slides

```bash
cd slide_deck
./build.sh .
# Open build/index.html in a browser
```

For the second pass (with visuals added):
```bash
./build-visuals.sh .
# Open build/index-with-visuals.html
```

## Repository structure

- `slide_deck/` — the presentation itself
  - `SLIDES.md` — primary design brief (content, structure, slide order)
  - `VISUALS.md` — second-pass visual additions
  - `content/` — first-pass HTML slide fragments
  - `assets/` — fonts and diagram images
  - `shared/` — header/footer HTML
  - `build/` — assembled output
  - `mapping-exercise.md` — Google Form spec for the interactive audience survey
  - `topic-inventory.md` — full HACK Week curriculum context

## Acknowledgments

This tutorial was developed in collaboration with Anthropic's Claude models. All content was reviewed, edited, and approved by the human authors, and the pedagogical decisions and final phrasing are the authors' own.

Diagrams adapted from Jason Gilman (Element 84) are used with attribution on individual slides.
