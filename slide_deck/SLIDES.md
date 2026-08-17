# Landscape of Coding Agents

Target audience: NASA earth science researchers attending a 5-day HACK Week — mixed coding fluency, diverse domains, some familiarity with generative AI tools
Duration: 90 minutes
Co-instructors: Anthony Arendt, Anshul Tambay

## How to render this deck (instructions for the slide generator)

**This document is a design brief, not slide copy.**

**Two-pass workflow.** This deck is built in two passes, and SLIDES.md governs only the first.

- **First pass (this file): content and structure only.** Build the deck to a publishable-looking, intentional state using only typography, layout, color palette, and accent following the specified design templates. Use no photographs and no decorative icons in this pass. The deck should look complete on its own — if it had to be presented tomorrow with no images, it should feel finished rather than naked.
- **Second pass (separate VISUALS.md): additive visual elements.** After the first pass is rendered and rehearsed, VISUALS.md specifies photographs, diagrams, and iconographic elements to *add* to existing slides.
- **Do not anticipate the second pass during the first.** If a slide feels visually sparse, the correct response is stronger typography or layout, not a placeholder.

**General rules:**

- The **Key message** line is the main idea to convey in the slide. The title of the slide is usually extracted as a subset of the key message.
- **Bullets** are suggested layout of content and not necessarily meant to be verbatim on the slide.
- **Note to self** lines are for the speaker only. Never render them on the slide.
- Default to one anchoring element per slide: a phrase, a number, or a small structural composition. When in doubt, less text.
- Maintain visual continuity: consistent type scale, generous whitespace, and the gold accent from the title slide.
- Any other text is general context that should be used to thoughtfully craft the content of the slide. Be concise but don't be afraid to include some amount of text - just enough to get the key message across. I favor complete sentences over em-dashes. Avoid the short, pithy one-liners. Stay with more scientific writing and complete sentences.

---

## 01-title

Title slide with UW branding. **Edit existing HTML — update text only.**

- Presenter names: Anthony Arendt, Anshul Tambay, Don Setiawan
- Date: August 18, 2026
- Session title: Landscape of Coding Agents
- NASA Responsible GenAI HACK Week, CryoCloud

## 02-framing

- Title: Goal for this week: a shared mental model of fundamental concepts
- Bullets:
  - By the end of this session you will have a framework for understanding any AI coding tool you encounter, regardless of vendor or interface.
  - The core architecture of generative AI tools have stabilized. We will focus on the concepts that persist across tools and vendors, rather than the rapidly shifting product landscape.

## 03-what-is-an-llm

- Key message: A large language model is a statistical model that predicts the next chunk of text given the text that came before it. It is a prediction machine, not a knowledge base.
- Bullets:
  - The model works in tokens — roughly three-quarters of a word, or a few characters of code. Everything about the model (context limits, cost, speed) is measured in tokens.
  - At each step the model picks a likely next token given everything that came before. This is all it does. Every capability you observe emerges from this one mechanism.
  - Randomness in this process is why you get different answers to the same question and why the model can sound confident while being wrong.
- Note to self: The audience includes people who may think of LLMs as search engines or databases. The "prediction machine" framing corrects that without being condescending.

## 04-chat-vs-agent

**Rebuild this slide.** Replace the harness callout text block with an original inline SVG diagram. Do not extract from the PDF source.

- Key message: The chat experience many of us have with LLMs is around answering questions. An agent is different because it reads your files, runs your code, and edits your project.
- Bullets:
  - Same LLM underneath, but different harness around it
  - Saying "I'm using Claude" is under-specified: browser Claude, Claude Code, and Claude in Cursor all behave differently
  - The harness, not the model, is what has changed in the last two years
- Diagram: Two-panel SVG showing the contrast between chat and agent configurations.
  - Left panel (Chat): a single box labeled "LLM" with one arrow in (user message) and one arrow out (response). Minimal. No surrounding elements.
  - Right panel (Agent): the same "LLM" box at center, surrounded by a visible boundary labeled "Harness". Inside the boundary, small labeled nodes around the LLM: "Files", "Terminal", "Tools", "Memory". Arrows connect the nodes to the LLM, and one arrow exits to the user.
  - The two panels are separated by a vertical divider. The LLM box is visually identical in both panels — the point is that the shell changed, not the core.
  - Style: thin lines, no filled shapes, gold accent on the harness boundary, white labels, consistent with the deck's geometric aesthetic. Built as inline SVG, no external image file needed.

## 05-six-pieces

**Keep existing HTML as-is.** No changes needed.

Every tool has all of these six components:
- Bullets:
  - LLM backbone — the language model itself; the thing generating text
  - Tool use — the ability to read files, edit them, run commands
  - Agent loop — the software that lets it decide whether to call another tool or finish
  - Project memory — a file the agent reads on startup so it knows about your codebase
  - MCP servers — a standard way to plug in external things like databases, calendars, APIs
  - Skills — reusable procedures for specific kinds of tasks
  - Every feature in every product maps to one of these. Switching tools is a configuration exercise, not a re-learning exercise

## 06-trained-in-vs-prompt

**Keep existing HTML as-is.** No changes needed.

- Key message: Trained in vs. in the prompt.
- Bullets:
  - Trained in: Python, common libraries, general patterns, dialogue format, when to stop
  - In the prompt: your data's quirks, your lab's conventions, your specific goal
  - You control one side of that line. Context engineering is the practice of filling the right side deliberately.
- Note to self: Ground this with a concrete example. "If you ask an agent to query snow depth observations from a database it has never seen, it will guess at table names and column conventions — confidently and incorrectly. That is a prompt problem. The model knows SQL; it does not know your schema. Giving it that schema is context engineering."
Render as two-column layout with the phrase as headline.

## 07-post-training

- Key message: The useful behaviors of an AI assistant — following instructions, knowing when to stop, calling tools — are not built into the base language model. They come from a second training phase called post-training.
- Bullets:
  - Supervised fine-tuning (SFT): human contractors write thousands of examples of ideal conversations, and the model learns the shape of a helpful interaction. This is why the agent follows your instructions.
  - Reinforcement learning from human feedback (RLHF): contractors judge which of two model responses is better, and the model is tuned to produce responses that score well. This is why the agent stops and decides it is done, instead of looping forever.
  - Tool-use fine-tuning: the model is trained on examples of conversations that include tool calls. It learns both the format and the harder meta-skill of knowing when a tool call is needed versus when it can answer from memory. This is how the agent calls a tool instead of just describing what to do.
- Note to self: The reason this matters for the audience is the next point — convergent post-training.

## 08-convergent-training

- Key message: All major AI labs do post-training in roughly similar ways. This is why you can swap Claude for GPT for Gemini in most coding agents and things still mostly work. It is also why investing in concepts (the six pieces, context engineering) rather than a specific product is the right strategy.
- Bullets:
  - Anthropic, OpenAI, Google, and Meta all use SFT + RLHF + tool-use training with different data but similar pipelines.
  - The resulting behaviors converge: all modern models can follow instructions, use tools, and stop when done.
  - The practical implication: your investment in learning how to shape agent behavior (context documents, skills, workflow patterns) transfers across tools. You are not locked in.

## 09-diagnosis-slide

- Key message: When an agent does something surprising or wrong, the first debugging question is: is this a training problem or a prompt problem?
- Diagram: Two-level decision tree as inline SVG. Root question branches into two outcomes; each outcome has a second level. No coda text — the tree fills the slide.
  - Root question: "Does the agent seem unaware of something specific to your work?" This frames context as the diagnostic axis, not prompt phrasing.
  - YES branch → Context problem (gold border — visually emphasized as the more common and actionable case)
    - Four levers listed beneath the box, not as tree nodes. Each lever is a context engineering move, not a prompt tweak:
      1. Load your data schema into context
      2. Add conventions to AGENTS.md
      3. Define what "done" looks like
      4. Write a skill for this task
  - NO branch → Training problem (white border)
    - Sub-question: "Can I restructure the task?"
    - YES leaf: Restructure the task
    - NO leaf: Switch models
- Note to self: This slide sets up the "trained-in or prompt?" interactive exercise if we run it. Use the SnowEx example: "The agent picked the wrong table for snow depth — is that a context problem or a training problem? It is a context problem. Monday afternoon's AGENTS.md tutorial teaches you exactly how to fix that."
- Note to self — "restructure the task": when someone asks what this means, it is a task decomposition move for when more context will not help — the model genuinely cannot do the thing as specified. Concrete examples: if the model struggles to write a complex multi-step analysis in one shot, break it into sequential steps with a separate prompt for each; if it can't reliably produce a specific output format, separate the reasoning step from the formatting step; if it loses track of constraints in a long conversation, scope the task more narrowly so the relevant constraints fit cleanly in a short prompt. The common thread is changing the shape of the problem so it no longer requires the capability the model lacks — not giving it more context, but asking for something different.

## 10-failure-modes

- Key message: When agents go wrong, they tend to go wrong in predictable ways. Naming these patterns now gives you vocabulary you will use all week.
- Bullets:
  - Fabrication (hallucination): the model produces confident, plausible-sounding output that is factually wrong. This is especially dangerous in scientific contexts because the output often looks like it could be correct. "Fabrication" is preferred over "hallucination" because it describes what actually happens without anthropomorphizing the model.
  - Sycophancy: the model agrees with your framing rather than pushing back, even when your framing is wrong. This is a systematic side-effect of RLHF training that rewards responses users rate as helpful.
  - Scope creep: the model does more than you asked — adds type hints, refactors adjacent code, restructures your project. Trained to be maximally helpful, it over-delivers by default.
  - Context exhaustion: as the conversation grows long and the context window fills up, the model loses track of earlier instructions and makes increasingly confused decisions.
- Note to self: These are all prompt problems or architecture problems, not mysteries. The point is to name them so participants can recognize them in their project work this week.

## 11-mapping-exercise

- Key message: Before we go further, let us understand where everyone in this room is starting from. Take three minutes to fill out this survey on your phone.
- Bullets:
  - QR code linking to the Google Form ("Where Does Your Work Sit?")
  - This is not a quiz. There are no wrong answers. "I have not used any AI tools yet" is useful data.
  - Your answers will help us and other instructors this week calibrate tutorials to this specific group.
- Note to self: Project the Google Forms response tab live as results come in. Spend 3–5 minutes after completion reading back patterns and normalizing the range. This is a natural break point at roughly 35 minutes into the session.

## 12-landscape-of-tools

- Key message: Five categories of AI coding tools, mapped by integration depth and privacy control. The right choice depends on the constraints of your work — for most researchers with sensitive data, those two axes dominate the decision.
- Diagram: Scatter plot as inline SVG. Two axes:
  - X-axis: Integration Depth (Low → High). Sub-label: "how connected to your actual workflow"
  - Y-axis: Privacy Ceiling (Low → High). Sub-label: "maximum achievable privacy for this tool category"
  - Five plotted points, each labeled with category name (bold) and example (italic, smaller):
    1. Cloud-hosted assistants (ChatGPT, Claude.ai, Gemini) — low integration, low privacy control. Bottom-left.
    2. IDE-native tools (GitHub Copilot) — high integration, low-medium privacy control. Bottom-right.
    3. AI-native IDEs (Cursor, Windsurf) — medium integration, low-medium privacy control. Center-right.
    4. Open-source options (Aider, OpenCode) — low-medium integration, high privacy control. Top-left.
    5. Command-line agents (Claude Code) — high integration, high privacy control. Top-right. This is the non-obvious finding: pairing a command-line agent with a local model gives you both deep integration and full data control.
  - Light dashed midpoint grid lines divide the plot into four quadrants. No quadrant labels — let the positions speak.
- Note to self: Keep this descriptive not prescriptive. The key insight to name aloud is the command-line agents point in the top-right: most people assume high capability means low privacy control, but that is not true if you choose the model hosting yourself.

## 13-five-axes

- Key message: Five axes for choosing an AI tool for a research task. There is no single best tool — the right choice depends on the constraints of the specific task and the data involved.
- Bullets:
  - Cost: flat subscription, metered by token (pay for every API call), or self-hosted (pay for the compute yourself).
  - Capability: single-file edits vs. multi-file refactors vs. autonomous multi-hour tasks. More expensive tools tend to be more capable, but not always.
  - Integration: how deeply the tool connects to your actual work environment. IDE-native, terminal, cloud-only.
  - Model hosting: where the model runs. Vendor cloud (fastest, most capable, least private), institution's cloud (institutional control), your own hardware (maximum control, least capability).
  - Privacy: what data can leave your machine? Some research data, code, or context can never go to a vendor. This constraint often dominates the other four.
- Note to self: Privacy is the axis most relevant to this NASA audience. It sets up the data-privacy slide and connects forward to Thursday's sandboxing tutorial.

## 14-context-window

- Key message: The model sees exactly what the harness puts into its context, and nothing else. The context window is the total amount of text the model can consider at once. Understanding this single concept explains most of the confusing behavior researchers encounter.
- Bullets:
  - The model has no access to your filesystem, your data, or your project unless the harness explicitly loads it into the context. This is why context engineering matters — it is the only way information reaches the model.
  - Modern context windows range from roughly 100,000 tokens to 1 million tokens (roughly 75,000 to 750,000 words).
  - Every turn of a conversation, the entire history is re-sent to the model. This explains three things:
  - First, cost scales with conversation length. A twenty-turn conversation costs more per turn than turn one.
  - Second, models have no memory between conversations. What looks like memory is the harness reloading context. Close the window, and the model has no idea who you are.
  - Third, context windows fill up. When they do, models get confused, forget instructions, or fail in unexpected ways.
  - The context window is a shared budget: system prompt, project memory, conversation history, tool results, the model's reasoning, and the answer it is writing all compete for the same space.
- Note to self: This is conceptually dense. Let it land. The "shared budget" framing is the key insight that makes all the context engineering tutorials later in the week make sense.

## 15-data-privacy-preview

- Key message: When you use a cloud-hosted AI tool, your data leaves your machine. Where it goes and what happens next depends on your access tier. This week's sandboxing and security tutorial on Thursday will cover this in depth.
- Bullets:
  - Consumer tier (free or personal-paid): prompts are often logged and may be used for training.
  - Enterprise and API tiers: contractual guarantees that prompts are not logged or used for training.
  - Institutional gateways: a controlled proxy your institution runs, adding authentication, budgets, and audit logging.
  - Local models: nothing leaves your machine, but capability is lower.
  - The practical default: match model hosting to data sensitivity. When in doubt, do not send it. A schema description or synthetic sample is often enough.
- Note to self: Do not go deep here. The point is to name the tiers so people know they exist, and to preview Thursday. One slide, one minute of talk time.

## 16-four-surfaces

**Keep existing HTML as-is.** No changes needed.

- Key message: Four Durable Places to Shape Agent Behavior.
- Bullets:
  - Context documents (AGENTS.md) — always loaded on startup; the facts and conventions the agent should always have in hand when working in this project
  - Skills — task-triggered procedures; the agent picks them up when the work matches.
  - Rules — path-scoped constraints that fire based on which files are being touched; hard limits rather than helpful suggestions.
  - Custom agents — distinct personas with their own tool access and voice; useful when you want a narrower, more focused agent for a specific job.
  - Taxonomy is portable across tools; file names differ
- Note to self: This is a preview of what people will learn hands-on in the AGENTS.md and Skills tutorials later today and Tuesday. Name them, don't teach them.

## 17-reproducibility

**Keep existing HTML as-is.** No changes needed.

- Key message: The conversation is scaffolding. The artifact is the science.
- Bullets:
  - LLMs are stochastic; science demands reproducibility. That tension is real.
  - The resolution: the process is not reproducible, however the artifacts are.
  - Your git repo, not your chat log, is the record.
  - You can commit plans, review notes, and validation outputs alongside code. git log docs/ reads like a lab notebook.
  - Log model, version, and date in your methods section, the way you would cite any tool.
  - Pin your dependencies, because AI-generated code often assumes packages it did not declare.

## 18-week-ahead

- Key message: Here is what the rest of this week builds on top of what you just learned.
- Bullets:
  - Monday afternoon: Context engineering — writing an AGENTS.md for a real scientific codebase, and building skills that encode your procedures.
  - Tuesday: MCP servers — giving agents structured access to real systems like NASA Earthdata. Workflow patterns — Research/Plan/Implement as a discipline for complex tasks.
  - Wednesday: Responsible and trustworthy AI discussion. GenAI-ready data.
  - Thursday: Sandboxing, security, and validation — constraining what capable agents can do so capability does not hurt you.
  - Friday: Synthesis and project showcases.
- Note to self: Keep this brisk. The point is to show that everything from today connects forward, and to motivate the afternoon session for people deciding whether to stay.

## 19-closing

- Key message: The six pieces, the trained-in vs. prompt distinction, and the four surfaces are the durable concepts. Tools will change. These will not.
- Bullets:
  - You do not need to pick a tool today. You need to understand the architecture so you can evaluate any tool tomorrow.
  - The researcher's primary lever is what goes into the prompt — context engineering. That is what this week teaches.
  - Questions welcome now. We will be available all week.
- Note to self: End with questions. If the mapping exercise surfaced anything surprising, reference it here.

---
