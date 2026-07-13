# Gen-AI Assisted Scientific Software Research Development
## Comprehensive Topic Landscape — v2

**Purpose:** This document maps the full landscape of what researchers need to know to use generative AI tools effectively, responsibly, and reproducibly in their research work. It is intentionally broader than any single workshop. The goal is to capture everything we *could* teach, so we can make informed decisions about priorities and delivery methods.

---

## Framing Principles

### Context engineering as the core skill
The unifying idea across the entire curriculum: the quality of AI output is determined by the quality of context you provide. Scientists already know how to build context. That's what research methodology is. Applying that same discipline to AI tools is the transferable skill that outlasts any specific product.

### Stochastic vs. deterministic
LLMs are fundamentally stochastic processes, but science demands reproducibility. This tension must be acknowledged honestly and addressed practically as it surfaces in every topic area.

### Authoring surfaces vs. infrastructure
Researchers spend most of their time authoring context, skills, rules, and subagents. MCP servers, models, and harnesses are infrastructure they consume. The curriculum should weight accordingly: teach the authoring surfaces deeply, teach infrastructure at the level of an informed consumer.

### Failure modes trace to training history
Every predictable failure of a coding agent traces to a specific decision in its training pipeline. Understanding the pipeline lets researchers *predict*, rather than memorize, when to distrust output. This framing gives the curriculum a durable epistemic stance that survives specific tools and models.

### Empirical, not provable
These systems work empirically, not provably. Training is the bet that gradient descent finds a useful function and that it generalizes to new inputs. It usually does — but "usually" is why verification, testing, and human judgment matter so much. Appropriate epistemic humility is a curriculum-wide stance.

### The "Before / After / Your judgment" pattern
A useful framework for researchers: "Here's how we used to do this → Here's what's possible now → Here's what your judgment still has to provide." This makes material relatable and avoids both uncritical hype and reflexive skepticism.

### Stability map

**Stabilizing — teach with confidence:**
- The core interaction pattern: describe intent, evaluate output, iterate
- Context engineering as a principle
- The four-surface authoring taxonomy (context / skills / rules / subagents)
- The SKILL.md convention
- The AGENTS.md convention for project memory
- Version control as safety net for AI-assisted work
- Verification, testing, and evals as non-negotiable practice
- RAG as a concept
- MCP as a protocol for tool use
- Convergent post-training as the reason model swaps work
- Responsible use, attribution, and documentation practices

**Maturing rapidly — teach the concept, hold the specifics loosely:**
- Specific coding agents (Claude Code, Copilot, Cursor, OpenCode, Hermes, Pi Coding) — the category is permanent, specific tools will shift
- Specific model names — teach model selection as a skill, not model names as facts
- Plugin marketplaces and ecosystems
- Consumer-facing agent products (browser, spreadsheet, desktop agents)
- Agentic RL as a live frontier driving capability jumps

**Cutting edge — mention, don't build curriculum around:**
- Multi-agent orchestration frameworks
- AI-to-AI protocols (agents calling other agents)
- Local model deployment for individual researchers

**Deprecated or superseded:**
- Elaborate manual prompt templating
- Chain-of-thought as a prompting technique (largely absorbed into reasoning modes)
- "Let's think step by step" as a workaround

---

## Section 1: Foundations — Terms, Tools, and Mental Models

### A shared glossary
A one-page reference of the terms researchers will encounter, delivered as its own artifact: LLM, model vs. harness/client, context window, tokens, agent, skill, rule, subagent, MCP, sandbox, slash command, RAG, eval, harness, gateway/proxy, attention, Transformer.

### How LLMs actually work (organized around four questions)
Rather than a list of facts, organize this around the four questions that agent behavior raises:

- **Why does it follow instructions at all?** → Supervised fine-tuning taught it the format of "user asks, assistant answers."
- **Why does it stop when done instead of looping or rambling?** → RLHF taught it what humans find helpful and when a response is complete.
- **Why does it call tools instead of just describing them?** → Tool-use fine-tuning on trajectories that include tool calls taught both the wire format and the meta-skill of when to call.
- **Why does model swap even work?** → Anthropic, OpenAI, Google, Meta, and DeepSeek all run similar pipelines. Convergent post-training produces convergent behavior.

Also covered here: pre-training as fluent autocomplete, LLM statelessness (the appearance of memory is the harness re-sending the conversation), the empirical-not-provable framing.

### The Transformer and attention: why context engineering works
Modern LLMs are built on the Transformer architecture, introduced by Google researchers in 2017 ("Attention Is All You Need"). The key innovation is a mechanism called **attention**, which lets the model, when predicting the next token, weigh the relevance of every other token in its context. This is the causal story for why context engineering is a real skill: when you provide a well-structured prompt, relevant documents, or a good AGENTS.md file, attention is the mechanism that lets those inputs actually shape the model's output. Without attention, "give it more context" wouldn't reliably help.

*Optional deep-dive for technical audiences: Universal Approximation Theorem as the "why any of this is possible at all" aside; "Attention Is All You Need" as recommended reading.*

### Trained in vs. in the prompt
The actionable mental model that ties post-training understanding to daily practice:

- **Trained in (the model already knows):** dialogue format, helpful tone, tool-call wire format, when to stop, knowledge up to training cutoff.
- **In the prompt (you control):** system message, project memory (AGENTS.md), specific tool schemas, current task description, documents you load into context.

When debugging an agent, ask: *is this a training problem or a prompt problem?* The prompt side is the only lever you control.

### The model / harness / interface distinction
Same model, different behavior depending on the harness around it. Why "I'm using Claude" is under-specified — Claude via web app, Claude Code, Claude via API, and Claude in Cursor behave differently because the system prompt, tool access, context management, and defaults differ.

### Anatomy of a coding agent (the six pieces)
LLM backbone, tool use, agent loop, project memory, MCP servers, skills/prompts. This diagram anchors the rest of the curriculum: every feature in every tool maps to one of these six pieces.

### The landscape of AI tools
Framed as a spectrum, not categories. Coding agents (Copilot, Claude Code, Cursor, OpenCode, Hermes, Pi Coding), chat interfaces, autocomplete, and the newer consumer-facing agents (browser, spreadsheet, desktop) that non-coding researchers will increasingly encounter.

### Same six pieces, different wrapper
A cross-tool mapping table showing where each of the six anatomy pieces lives in each major tool (project memory as `AGENTS.md` vs `.github/copilot-instructions.md` vs `.cursor/rules`, etc.). *If you understand the pieces, switching tools is a config exercise.*

### Tokens, cost, and the context window as shared budget
What tokens are, how text maps to them, cost model. The context window is a fixed shared budget every turn: system prompt + AGENTS.md + full conversation history (every turn re-sent) + every tool result + model reasoning + answer. Practical budgeting, free tiers, environmental cost.

### Choosing between tools (five axes)
Cost, capability, integration, model hosting, privacy. The right tool depends on the researcher's constraints, not on benchmarks. Choosing tools is a durable skill; specific tools will change.

### What the AI can and cannot see
The AI sees only what you give it. When data leaves your machine (API calls) vs. stays local (local models). Consumer vs. enterprise/proxy tier data handling: consumer tiers often log and train on prompts; enterprise and proxy tiers usually do not.

### LLM gateways and institutional proxies
An increasingly common pattern in research institutions: a lab- or institution-level proxy that routes requests through a controlled endpoint, handles credentials, enforces budget/rate limits, and provides logging for compliance. A third option between "vendor API" and "local model."

---

## Section 2: Context Engineering

### Why context is everything
The "context ladder": current line → current file → current project → your domain → external systems. Same prompt, different context, dramatically different results. AI struggles with ambiguity; specificity is the lever.

### Prompting techniques (honest about what's being absorbed)
- Few-shot examples for domain-specific input/output patterns
- Constraint specification (libraries, standards, approaches to use or avoid)
- Output format specification
- Note: chain-of-thought as a *manual technique* is being absorbed into reasoning modes; the underlying idea (multi-step reasoning helps on hard problems) is durable.

### Spec-driven development
Writing specification documents before writing code. Using AI to critique specs and find ambiguities.

### The Research/Plan/Implement pattern (and Explore/Plan/Execute variant)
Structured workflow: research the problem → plan the approach → implement step by step. Why jumping straight to code produces worse results. Concrete example: skill-based instantiations of this pattern that produce auditable artifacts at each phase.

### Managing the context window in practice
When to `/clear`, `/compact`, or start a new conversation. Signs the context is getting stale. Problem decomposition. **Handoff artifacts** as a named pattern: a compacted document that lets a fresh session pick up where a full one left off.

### Subagent delegation as a context-management technique
Dispatching sub-tasks to fresh contexts to preserve the main one. Not just for multi-agent orchestration — a routine practical technique for long tasks.

### Token optimization
Being deliberate about what goes into the context window. Concise, structured context documents. When to use a large model with a big context window vs. a smaller model with focused context.

---

## Section 3: Choosing the Authoring Surface

*This section is the structural heart of the curriculum. It sits between "understand the landscape" and "encode your expertise into it."*

### The two-question decision framework
1. Does this need to be always-loaded, task-triggered, or a distinct persona?
2. Am I giving the agent knowledge/a procedure, or restricting what it's allowed to do?

### The four surfaces, side by side
A table comparing:
- **Context documents** (AGENTS.md, nested) — always-loaded facts and conventions
- **Skills** — on-demand procedures, same tool access as the calling agent
- **Rules** — always-on but path-scoped; hard constraints
- **Custom agents / subagents** — distinct persona, potentially restricted tools or different model

### The knowledge-vs-permissions litmus test
The distinction researchers get wrong most often. Different knowledge only → skill. Different permissions, narrower tool list, or genuinely different "voice" → custom agent. Prose constraints (soft, agent may violate) vs. tool-list constraints (hard, agent cannot violate).

### Slash commands as a fifth surface
User-triggered shortcuts that compose with the other four. Where they fit and when to build them.

### The taxonomy is portable; the file formats aren't
Every major ecosystem has these surfaces; the specific file conventions differ. Invest in the knowledge; hold the formats loosely. This is the vendor-lock-in section's thesis expressed once, cleanly.

### 3a. Context documents
- AGENTS.md as the cross-vendor convention; CLAUDE.md as one instance
- What belongs in a context document: project structure, conventions, domain terminology, common pitfalls, coding standards
- Nested context files for large repos
- Pseudo-prompts in image and directory context files
- Team context documents as version-controlled assets, not individual preferences

### 3b. Agent skills
- The SKILL.md convention
- The skill `description` field as the selector: how "Use when..." clauses let agents auto-pick skills
- What makes a good skill: domain-specific terminology, common pitfalls, preferred methods, data format conventions
- Encoding domain expertise: examples from research contexts (e.g., "when working with time series, always check for missing values and irregular sampling")
- Skills vs. plugins; the plugin ecosystem
- Read-only skills as an example of permission-in-prose
- Skills as institutional knowledge that survives personnel turnover
- Creating custom skills for your lab or domain

### 3c. Rules
- Path-scoped constraints; glob-based activation
- Expressing hard constraints vs. soft guidance
- Rules for reproducibility (e.g., "code in `analysis/` must have accompanying tests")
- Rules as a mechanism for encoding review policies

### 3d. Custom agents and subagents
- Restricted-tool personas: schema auditors, migration agents, review agents
- Different-model personas: smaller/cheaper for narrow tasks
- Parallel subagents for exploration and context preservation
- When to reach for this vs. a skill (back to the litmus test)

---

## Section 4: MCP and Tool Use

*MCP is infrastructure. Most researchers will consume MCP servers; a smaller number will design them.*

### What makes an agent different from a chat session
Agents can take actions: read files, run code, call APIs, modify projects. The spectrum from "quick answer" (chat) to "help me build this feature" (agent).

### MCP as a protocol
A standardized way to connect AI to external tools. How MCP works: tool definitions, input schemas, responses. Broad industry adoption.

### Consuming MCP servers (the majority use case)
Connecting to existing MCP servers. Querying real data through natural language. Verifying MCP-retrieved results.

### Designing MCP servers (advanced)
When to build one. Wrapping databases and APIs. Authentication, error handling, security. Flagged as advanced content; not for every researcher.

### Permissions and the approval habit
What have you granted the AI permission to do? Read vs. write, file system, network, credentials. The approval habit: read what the agent proposes before accepting.

---

## Section 5: Sandboxing, Containerization, and Safe Execution

*A standalone section because agent safety is genuinely distinct from other topics.*

### Why sandboxing matters more with agents
Human-written code is bounded by human intent; agent-executed code isn't.

### The two riskiest tool categories
File-editing tools and shell-execution tools are the two categories most worth constraining. Sandboxing means gating these specifically.

### The permission model
Read vs. write, filesystem, network, credentials. What you're granting when you accept a tool call.

### "Proceed-in-sandbox" as a pattern
Auto-approve inside a boundary, require confirmation to cross it. The workflow this enables and the boundaries worth setting.

### Containers for agent work
Docker for general-purpose isolation; Apptainer/Singularity for research computing environments. Tradeoffs.

### Credential hygiene
What should never be in an agent's context. Environment variables, secrets, tokens.

### Prompt injection as a first-class risk
Agents follow instructions in everything they read — and can't fully distinguish your instructions from instructions buried in the content they process. Attack surfaces include READMEs, docstrings, comments in collaborator repos, web pages, API responses, and *data files themselves* (CSV headers, cells, PDFs, downloaded datasets). Mitigations: read-only skills for untrusted data, don't auto-approve, treat agent output as untrusted until reviewed.

### Redaction and synthetic samples as a privacy technique
Instead of sending sensitive data, send a schema, a redacted excerpt, or a synthetic example preserving the shape of the problem. Often sufficient for the agent to help.

---

## Section 6: Working With AI-Generated Code

### The evaluate-iterate loop
Describe intent → generate → evaluate → refine. Reading AI-generated code critically. Common failure modes: silently wrong results, plausible-but-incorrect logic, inappropriate method selection.

### Reading code is a first-class skill
When agents write most of the code, reading it fluently becomes more important, not less. The single most valuable exercise: give researchers an AI-generated analysis containing a plausible-looking but wrong result and ask them to find the bug.

### Debugging and error interpretation
One of the highest-value, lowest-risk applications. Pasting tracebacks. Understanding unfamiliar codebases or inherited scripts. A good entry point for skeptics.

### Working with existing codebases
Using AI to understand, refactor, or extend. "Explain what this function does." Refactoring legacy notebooks into proper packages. Distinct from starting from scratch.

### "Read the diff, not the chat"
The agent's summary is a claim; the diff and re-run results are evidence.

### "Agents are coworkers, not magic"
Coworkers get pushback. Researchers are often reluctant to interrupt, disagree, or re-run because they treat the agent as an oracle. Explicit permission to push back is worth teaching.

### Git practices for AI-assisted work
- Commit before you start (clean tree makes `git diff` show exactly what the agent touched; `git restore .` is a one-command undo)
- Commit per phase (bad later phases roll back cleanly)
- Commit artifacts alongside code (docs, plans, validation outputs — the auditability trail)
- Branch-based agent work and worktrees for parallel exploration attempts

---

## Section 7: Verification, Testing, and Evals

### Why testing matters more with AI-generated code
"You used to test your own code because you knew where you cut corners. Now you test AI code because you don't know where it did."

### Test-first workflows with agents
Designing test cases before asking AI to generate code. Using AI to enumerate edge cases. Instructing AI to document its changes to facilitate human review.

### Evals as a distinct practice from unit tests
Scored test suites for agent or skill behavior on your domain. The reproducible artifact that makes agent-assisted work defensible. Distinct from testing the code the agent produced — this tests the agent's behavior itself.

### LLM-as-judge and judge models
Using one model to grade another's output against a rubric. The mechanism behind modern eval pipelines. Concrete example: a validation skill that re-runs an analysis's numbers and checks the draft's claims against them.

### Automated vs. manual success criteria
Agents can check some things automatically (numbers match, tests pass) but not others (design appropriateness, domain judgment). Being explicit about which is which in the plan is a discipline.

### The [CITATION NEEDED] pattern
For high-hallucination-risk domains (references, statistics, dates), have the agent emit explicit "needed" markers rather than fake content. Trains researchers to look for the *absence* of the marker as the failure signal.

### CI as a reproducibility guardrail
Continuous integration catches AI-generated code that passes a quick local check but breaks in a clean environment. AI-generated code often assumes packages or versions that aren't in the dependency spec — CI surfaces this immediately.

### Verification loops
Using rules and tests as agent-visible boundary conditions the agent must satisfy.

---

## Section 8: RAG and Grounding

### Why LLMs get your domain wrong
Hallucination, knowledge cutoff, domain underrepresentation. The AI's predictions are only as good as its training data.

### RAG concepts
Retrieve relevant documents, then generate an answer grounded in those documents. What kinds of documents work well. What the AI gets and doesn't when you use RAG.

### Building a knowledge base
Preparing documents. Chunking strategies for scientific content. Embedding models and vector databases (conceptual level). Privacy considerations.

### Using RAG effectively
Evaluating RAG-augmented answers: did it actually use your documents? Needle-in-a-haystack. When RAG helps and when it doesn't. Combining RAG with other context engineering.

### Semantic search as a component
Building semantic search and providing it to users as a tool.

---

## Section 9: Data for AI-Assisted Research

*A new section. Distinct from RAG; this is about structured data.*

### AI-ready datasets
What makes structured data legible to agents. Distinct from preparing documents for RAG.

### Documentation and metadata conventions
Schema documentation, data dictionaries, metadata that agents can read. What "self-describing data" means in an agent context.

### File layouts and naming conventions
Directory structures that reduce agent confusion. Naming patterns that let agents locate relevant files without brute-force search.

### Data-side complement to context engineering
The same discipline of "reducing ambiguity so the model can do its job" applies to how you organize data, not just how you write prompts.

---

## Section 10: Reproducibility in an AI-Assisted World

### The fundamental tension
Science demands reproducibility; LLMs are stochastic. "I used AI to help write my analysis" is not a reproducible methods description.

### Process reproducibility vs. output reproducibility
The AI-assisted process (conversations, iterations) is NOT reproducible. The artifacts produced (code, documents, analysis) ARE reproducible once committed. The Git repo — not the AI conversation — is the reproducible record.

### The auditability trail: docs alongside code
Per-phase markdown artifacts (profile, plan, exploration, test, draft, validation) committed alongside code become a dated record of *why* you ran an analysis and what you checked. `git log docs/` as a reviewable lab notebook.

### Documenting your AI environment
Pinning and reporting model, version, and approximate date. A durable citation *pattern* rather than a specific model name that will rot in months. Conversation logs and prompt histories as supplementary materials.

### The provenance chain
Prompt → AI response → human review → human edits → tested code → committed artifact → published result.

### Determinism when you need it
Temperature and seed parameters via the API. Why chat interfaces don't offer this. When determinism matters and when it doesn't.

### Model drift and long-running projects
Models change between versions; today's prompt may produce different results next year. Strategies: capture outputs not just prompts; pin model versions where possible; use RAG to ground outputs in stable documents.

### Prompt and conversation history as research artifacts
Should you save AI conversations? Treating prompt logs like lab notebooks. Practical tools for archiving. What to include in supplementary materials.

### Pinning dependencies alongside AI-generated code
Requirements files, lock files, environment specs are part of the reproducible artifact. AI-generated code often assumes packages that aren't in your spec.

---

## Section 11: Failure Modes — Predicting When to Distrust Output

*Restructured from the previous "When NOT to use AI." Every failure traces to a specific post-training decision, which lets researchers predict rather than memorize.*

### The failure-mode-to-training-history taxonomy

| Failure | Traces to | Mitigation lives in |
|---|---|---|
| Context exhaustion (forgets mid-task) | Limited context window | Section 2 (handoff, decomposition) |
| Looping | RL on short trajectories | Section 3d (subagent delegation) |
| Niche hallucination | Domain underrepresented in training | Sections 3b, 8 (skills, RAG) |
| Confident wrong answers | RLHF over-tuned for confidence | Section 7 (evals, judge models) |
| Tool misuse (edits when should ask) | RLHF made it action-biased | Section 5 (permissions, read-only skills) |
| Scope creep (does more than asked) | "Be helpful" taught too eagerly | Sections 2, 3 (tight scope, plans) |
| Sycophancy (agrees with your framing) | Preference learning side-effect | Sections 6, 7 (pushback, external validation) |

### The consolidated decision framework
A flowchart or checklist for "should I use AI here?" that references the taxonomy above rather than duplicating it.

### Knowing when to stop
Diminishing returns are real. Token cost as a natural brake. The goal is augmented productivity, not AI-assisted perfectionism.

### Autonomous pipelines without human checkpoints as a live risk
Not just a frontier to admire — a temptation researchers face now. Recent empirical evidence (agents authoring >99% of code in 40%+ of sessions, asking clarifying questions <2% of turns, with less than half of output surviving into commits) supports the argument that collaborative human-agent sessions are more effective than full autonomy.

### Attribution and citation implications
Covered further in Section 12.

---

## Section 12: Responsible Use, Ethics, and Institutional Practice

### Drawing your own lines — personal AI use policy
Where your values draw the line. Drafting a personal policy. Revisiting as you gain experience. Environmental impact as a factor for some researchers.

### Data privacy and institutional compliance
Web interface vs. API vs. local model vs. institutional gateway. IRB-covered data, FERPA, pre-publication data, NDA-covered data. Provider retention and training policies (vary by provider and tier — consumer often trains on prompts, enterprise/proxy usually does not). When to use which.

### Licensing and intellectual property
Who owns AI-generated code? Training data licensing concerns. Review AI-generated code as if a collaborator wrote it.

### Citation and attribution
Evolving journal policies. AI as tool citation vs. co-authorship (no). What to include in a methods section. AI-assisted vs. AI-generated work.

### Bias, representational harms, and equity of access
- Literature bias (predominantly English-language training data)
- Demographic bias (assumptions about gender, race, age, geography)
- Domain skew (popular fields get better AI performance)
- Sycophancy as a training artifact (systematic across models, not fixable by prompting alone)
- Equity of access (paid tiers, institutional agreements, GPU resources unevenly distributed)
- Practical mitigation: cross-check with domain experts, especially when outputs touch populations different from training data's center of gravity

### Vendor lock-in and portability
The taxonomy is portable; specific file formats and tools are not. Invest in the knowledge you're capturing; hold the specific format loosely. Keep AI-assisted artifacts independent of the tool that helped create them.

---

## Section 13: Collaborative and Team Workflows

### Shared context across a team
Consistency depends on shared context, not shared conversations. Project-level context documents as team assets, version-controlled with code. Establishing shared conventions.

### Code review when everyone is using AI
What AI catches well vs. what it misses. AI as first-pass reviewer to free humans for domain judgment. The risk of rubber-stamping when both author and reviewer use AI. What's the minimum understanding required before submitting a PR — full comprehension or general understanding of the approach?

### PR practices for AI-assisted work
Requiring tests alongside AI-generated code. Flagging sections the author hasn't fully verified. Reading the diff, not the chat summary.

### Sharing and standardizing tooling in a group
Agreeing on tools, plugins, and MCP configurations across a lab or project team. Shared skill libraries as institutional expertise. Version-controlling tool configurations. Handling different comfort levels.

### Knowledge management and institutional memory
AI-assisted work can be opaque: if a postdoc leaves, can the next person understand the pipeline? Documentation practices: what was intent, what did the AI contribute, what did the human verify? Skills and context documents as institutional memory.

---

## Further Study — Advanced Technical Content

Pointers rather than curriculum:

**Foundational reading:** "Attention Is All You Need" (Vaswani et al., 2017) for researchers who want to understand the Transformer architecture. Universal Approximation Theorem as the "why any of this is possible" mathematical foundation.

**Building RAG systems from components:** LangChain, vector databases (Qdrant, Chroma), embedding model selection, hybrid search with reranking, agentic RAG, document ingestion pipelines.

**Running local models:** Open-source models (OLMo, Llama, Mistral, Qwen), quantization, Ollama and llama.cpp, GPU/CPU tradeoffs.

**Building MCP servers:** Protocol specification, wrapping databases and APIs, authentication and security.

**AI-orchestrated workflows:** Agentic frameworks (pydantic-ai, LangGraph, CrewAI), multi-agent system design, hooks, sub-agents, deployment.

**Building your own agent harness:** For researchers who want to understand the loop from primitives — deliberately flagged as an optional deep-dive rather than main-line content, since most researchers benefit more from understanding the concepts verbally than from writing tool-dispatch code.

---

## Delivery Method Notes

*For team discussion — not prescriptive.*

Options for delivery:
- **5-day workshop** — focused subset with hands-on exercises
- **Standalone seminars** (1–2 hours) — individual topics as eScience seminars or lunch talks
- **Self-paced Jupyter Book** — full landscape as a reference resource
- **Office hours integration** — specific topics as researchers encounter them
- **Advanced workshop** — orchestration and infrastructure track for experienced users

**Pedagogical patterns worth naming across delivery methods:**

- **Same task, two ways:** show polished tool alongside minimal reproduction so researchers see the harness is not magic.
- **Plausible-but-wrong demos:** build exercises around outputs that would pass casual review, not obviously-wrong ones. Teaches distrust of surface plausibility.
- **Slow demo as pedagogy:** when a demo takes time to run, use the interval to teach failure modes and mitigations.
- **Demystification without the code tax:** for non-developer researchers, describe the harness verbally rather than requiring them to read Python. The concept is what matters; the implementation is optional.