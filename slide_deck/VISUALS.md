# Visual Elements — Landscape of Coding Agents

Companion file to SLIDES.md. This file governs the **second pass** of the two-pass workflow.

# How to use this file (instructions for the slide generator)

**This is an additions document, not a parallel specification.** The first pass (governed by SLIDES.md) has already produced rendered HTML slides. This file specifies visual elements — photographs, diagrammatic accents, icons — to **add** to those existing slides.

- Modify the existing HTML for each slide; do not regenerate from scratch.
- Add only what this file specifies. Slides not listed here remain unchanged.
- If a visual element here would conflict with the first-pass layout, the first-pass layout wins — flag the conflict rather than overriding it.
- Slide identifiers (`## 01-title`, `## 02-framing`, etc.) match SLIDES.md exactly. Use them as anchors.

# Global styling for diagrammatic elements

- **Line weight:** thin, uniform. No filled shapes.
- **Color:** gold accent on transparent or neutral background.
- **Level of abstraction:** geometric and minimal. No literal pictograms.
- **Scale:** small. Visual accents, not focal elements. Typography remains primary.

# Global styling for photographs

- **Source:** misc-ai-slides.pdf (Jason Gilman, Element 84) contains reusable diagrams. Other sources TBD.
- **Composition preference:** wide-frame moments showing relational context over tight portraits.
- **Treatment:** consistent color grading across the deck.
- **Rule:** one photograph or diagram per slide maximum.

# Attribution

Diagrams sourced from Jason Gilman (Element 84) must carry visible attribution on the slide where they appear. Use a small footer-style credit line: "Diagram adapted from Jason Gilman, Element 84". If the diagram is redrawn in UW brand style, use "Adapted from Jason Gilman, Element 84". If used unmodified, use "Credit: Jason Gilman, Element 84".

---

# Per-slide additions

## 01-title
- **Source:** assets/images/escience-logo.png, assets/images/SSEC-logo.png
- **Description:** place institutional logos for eScience and SSEC across the bottom of the slide, big enough to be visible in a slide presentation.

## 02-framing
No additions.

## 03-what-is-an-llm
- **Source:** assets/diagrams/token-prediction-diagram.png
- **Description:** "Non-deterministic" diagram showing tokenized input ("The sky is") → LLM network → probability distribution (blue = -0.96, clear = -1.60, usually = -2.47, etc.) → gradient bar (more likely / less likely) → selected output ("The sky is blue"). Color-coded tokens throughout.
- **Placement:** Below or beside the bullet content. This diagram visually demonstrates next-token prediction and non-determinism — the two core concepts of this slide.
- **Adaptation notes:** May need to be redrawn in UW brand colors (purple/gold) to match the deck. The conceptual layout and flow are the key elements to preserve. Original source cited in Jason's deck: NVIDIA developer blog.
- **Attribution:** Include footer credit "Adapted from Jason Gilman, Element 84" on this slide.

## 04-chat-vs-agent
Original inline SVG diagram built directly into the first-pass HTML. No second-pass additions needed. No attribution required.

## 05-six-pieces
No additions.

## 06-trained-in-vs-prompt
No additions.

## 07-post-training
No additions.

## 08-convergent-training
No additions.

## 09-diagnosis-slide
No additions.

## 10-failure-modes
No additions.

## 11-mapping-exercise
- **Source:** assets/images/qrcode.png
- **Placement:** place this where the QR code belongs in the slide.

## 12-landscape-of-tools
No additions.

## 13-five-axes
No additions.

## 14-context-window
- **Source:** assets/diagrams/context-window-diagram.png
- **Description:** "Context limits are the cause of almost all problems" — context window visualized as a rounded-rectangle container with stacked colored blocks: System Instructions/Tools/Agent Instructions (pink), User Messages (green), Agent Thoughts (light blue), Tool Call Input and Responses (yellow), Agent Responses (blue). Arrow pointing from the container to an LLM icon.
- **Placement:** Primary visual for this slide, replacing or supplementing the bullet list. The stacked container makes the "shared budget" concept immediately graspable.
- **Adaptation notes:** Redraw with UW color palette. Keep the stacked-block metaphor and the finite container boundary. Label the blocks with the terminology used in our deck (system prompt, project memory, conversation history, tool results, model reasoning).
- **Attribution:** Include footer credit "Adapted from Jason Gilman, Element 84" on this slide.

## 15-data-privacy-preview
No additions.

## 16-four-surfaces
No additions.

## 17-reproducibility
No additions.

## 18-git-workflows
No additions. The inline SVG git graph serves as the primary visual.

## 19-week-ahead
- **Diagram:** A vertical or horizontal "building-up" arc showing the week's tutorials as stacked layers, each building on the one below it. The structure should convey that each tutorial adds a layer of capability, and each layer requires the one before it.
- **Suggested layout:** Bottom-to-top stack or left-to-right progression:
  - Foundation: Landscape of Coding Agents (Monday AM — this tutorial)
  - Layer 2: Context Engineering — AGENTS.md + Skills (Monday PM)
  - Layer 3: MCP — structured access to real systems (Tuesday AM)
  - Layer 4: Workflow Patterns — Research/Plan/Implement (Tuesday AM)
  - Layer 5: Sandboxing & Security — constraining capability (Thursday)
  - Layer 6: Verification & Reproducibility — knowing it is correct (Thursday)
- **Design notes:** This is not a schedule list — it is a dependency diagram. Each layer should visually rest on the one below it. Use the UW brand palette to distinguish layers. Keep text minimal (just the layer name). The point is to show participants that skipping a layer means the ones above it do not work.

## 20-closing
No additions.

---

# Additional diagrams available but not yet placed

These are from misc-ai-slides.pdf and may be useful in future passes or for other tutorials in the HACK Week:

- **Page 45–46:** "Typical Agent Harness Flow" (Parts 1 & 2) — hand-drawn style. Not used; slide 04 instead uses an original inline SVG with a simpler framing appropriate for early in the tutorial.
- **Page 47:** "AI Agents" comprehensive architecture — User → Loop → Model, with Tool Registry, Tool Dispatcher, Plans/Memory, System Prompt. Labeled "Choice on Each Loop: Use a Tool, Write/Read a Plan, Answer the user." Most detailed view of the agent loop.
- **Page 15:** "An LLM is like a CPU" — Context/Instructions → AI chip → outputs. Alternative framing for slide 03.
- **Page 37:** Agent example with Lyme disease query — Broker → LLM → Catalogs/Data/Docs/API. NASA-relevant but uses "Broker" terminology rather than our "harness" framing.
