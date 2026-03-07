# Delineate

A product thinking framework that lives in your repo.

---
status: draft
---

## Vision

Delineate is a structured workflow for going from fuzzy problems and customer feedback to prioritized, well-specified work — using the same process whether a human or an agent is doing it.

It's not an app. It's a set of markdown templates, a directory structure, and an `agents.md` file that you install into your repo. The workflow runs through git and your issue tracker (GitHub Issues, Linear, Jira — whatever you use). The agent reads and writes the same files a human would. The artifacts are version-controlled alongside the code they shape.

The system is built for a world where AI agents do most of the coding, and the bottleneck is knowing the right thing to build — or the right thing to delete.

### Thesis

Most tools in this space solve agent coordination (how to run many agents) or task tracking (how to manage issues). None of them solve the product specification layer — the system that determines *what* to build, *why*, and whether the assumptions behind it still hold.

The specification layer is the highest-leverage problem. If your spec is precise enough that an agent can execute it without questions, the coordination and execution layers become commodity infrastructure. Own the thinking, not the doing.

### Distribution

Delineate installs into your existing repo like a library — but for product thinking. No server, no database, no accounts. Git is the database. Your AI coding agent is the runtime. Fork it, customise it, inspect it. It's just files.

---

## Problems

### 1. Engineering is outrunning product thinking
Engineers with AI are shipping so fast that they regularly run out of work that's been robustly considered and validated from a product perspective. The question has flipped — the bottleneck isn't "can we build this?" but "should we build this?" Teams are flipping the PM-to-engineer ratio on its head — not because they need more process, but because specifying the right thing to build is now harder than building it. The queue drains faster than product can fill it with well-considered work. And even when product thinking does happen, it happens in Slack and memory — invisible, unreusable, and lost within weeks. Three months later, nobody remembers why a feature was scoped a certain way.

### 2. Speed creates regret effort
The cost of building has collapsed — and with it, the friction that used to protect products from building the wrong thing. When engineering is nearly free, every idea gets built because "it only takes a minute." But every feature added increases cognitive load for users, every unvalidated addition taxes future maintenance, and shipping a bloated product obscures which parts actually matter. We acknowledge that iterations have their own efficiency — shipping fast and learning is valuable. But we want to minimise regret effort: the work that exists purely because nobody paused to think before building. The format is part of the problem — PRDs live in Google Docs or Notion, disconnected from the code they describe, unreadable by agents, stale within days. Requirements that can't keep pace with engineering aren't requirements — they're wishes.

### 3. AI supercharges engineers but not product people
AI has transformed how engineers write code. The same transformation hasn't happened for product managers and designers. When PMs spend their weeks vibe-coding prototypes, they're neglecting the higher-leverage work — customer discovery, prioritisation, strategic thinking — that actually determines whether the right thing gets built. We want to supercharge product thinking the same way AI supercharged engineering — not by replacing it, but by giving product people the same force-multiplication that engineers already have. The line between "product" and "engineering" is blurring — everyone is a coder now — and the workflow should reflect that.

### 4. Agents lack a management framework
AI agents are becoming like digital employees — capable, fast, and increasingly autonomous. But most developers report their agents "miss context" — not because the agents are dumb, but because the context doesn't exist in a form they can read. Specifications are vague, requirements are scattered, and the reasoning behind decisions was never written down. Today, using an agent means constantly monitoring progress, reviewing step by step, and hand-holding the work. We need the equivalent of good management practices for agents: clear briefs, defined scope, structured context, and outcomes you can verify — so agents can work autonomously and humans review outputs, not processes.

---

## Principles

### 1. Question, delete, simplify — then build
The agent's first response to any problem is never "let's add a feature." It follows the deletion algorithm: Does this requirement need to exist? What can we remove? What can we simplify? Only after those are exhausted does it propose new work. If you're not adding back 10% of what you deleted, you didn't delete enough.

### 2. Requirements live at the codebase
Code is a creative medium. Product designers need intimate knowledge of it, like a potter knows clay. PRDs belong in the repo, version-controlled alongside the code they shape, readable by the same agents that will write that code. Not in Notion. Not in Google Docs. In the repo.

### 3. Start with evidence, not solutions
Problems and user feedback are the raw material. Solutions are derived, never assumed. The agent triages and prioritizes based on input from the human orchestrator, customer feedback, analytics — whatever channels exist. It finds patterns across raw evidence before proposing any response.

### 4. Humans and agents use the same workflow
This isn't an agent tool that humans monitor, or a human tool that agents plug into. It's one workflow where both are participants. A human can capture a problem, write a PRD, and shape issues by hand using the same templates and structure an agent uses. The agent accelerates the workflow; it doesn't gatekeep it.

### 5. Craft is a competitive advantage
As software gets easier and faster to build, functional parity becomes commodity. The returns to beautifully crafted, joyful experiences are increasing — not decreasing. The workflow treats experience quality as a product requirement, not a polish pass. "How does this feel?" is asked during shaping, not after shipping. When two products solve the same problem, users choose the one that sparks delight.

### 6. Every milestone delivers a whole cake
Milestones are not phases of construction — they're increments of value. M1 should deliver a simple, complete version of the thing. M2 adds richness. M3 adds polish. If only M1 ships, users still have something functional and whole. Think of it like a cake: M1 is a simple cake. M2 adds the extra layers. M3 is the decoration. Even if you only finish M1 — you still have a cake. This matters because PRDs are full of uncertainty. If you structure milestones as dependencies ("M1 is the foundation, M2 is the walls, M3 is the roof"), then shipping only M1 delivers a useless foundation. Structure them so each one stands on its own.

---

## The Workflow

Three modes, used by humans or agents interchangeably.

### 1. Surface: Problems + Feedback → Patterns → Priorities

Input enters from two channels:

**Direct input** — the human orchestrator describes business problems, strategic priorities, things that feel wrong. The agent (or human) writes a structured problem file.

**Integrated input** — customer feedback from support tools (Intercom, Zendesk, Plain, etc.) via MCP or CLI. Feedback enters in the customer's own words.

The agent reads all captured problems and feedback, identifies patterns (multiple signals pointing to the same underlying issue), and asks two questions:

1. **What's broken?** — problems to fix, friction to remove, pain to eliminate.
2. **What could be great?** — opportunities for craft and delight, not just function. Where could the experience go from "works" to "feels good"?

It then proposes a prioritized list. It considers the deletion algorithm: which of these problems could be solved by *removing* something? Which by *simplifying* something that already exists? Only after deletion and simplification are exhausted does it propose new work.

When a significant choice is made — meaningful alternatives were evaluated and rejected — a decision record is written to `decisions/`. This captures the reasoning, not just the outcome, so the same investigation doesn't repeat in 3 months.

The human orchestrator reviews, rearranges, and commits.

```
Problems + Feedback
        ↓
Pattern detection
("these 8 items are really 2 problems")
        ↓
Two questions:
"What's broken?" + "What could be great?"
        ↓
Prioritization
(with deletion/simplification considered first)
        ↓
Response: Build / Change / Remove / Do Nothing
(significant choices recorded in decisions/)
```

### 2. Define: Priorities → PRD → Shaped Issues

The agent reads the prioritized problems and drafts a PRD with milestones. The PRD captures: what we're solving, the approach, what's in scope, what's explicitly out of scope, assumptions, and open questions.

The human reviews, edits, and commits with a meaningful message. The PRD is a living document — when requirements change, it's updated with diffs, not replaced. `git log` on the PRD file is the decision history.

Once a PRD milestone is marked `active`, the agent (or human) shapes issues from it — each with description, context linking back to the PRD, acceptance criteria, and code pointers. Issues are created in your tracker: `gh issue create` for GitHub, the Linear API, or manually in whatever tool you use.

```
Prioritized problems
        ↓
PRD drafted (with milestones)
        ↓
Human reviews, edits, commits
        ↓
Issues shaped from active milestones
        ↓
Issues created in tracker
(gh issue create, Linear, Jira, etc.)
```

### 3. Deliver: Issues → Execution → Ship

Shaped issues are picked up by humans or agents. The execution layer is whatever your team already uses — GitHub PRs, Linear cycles, Jira sprints. Delineate doesn't orchestrate execution — your existing tools do.

The workflow's value is upstream: by the time an issue reaches execution, it's well-specified enough that an agent can execute it without questions, and a human can execute it without asking for clarification.

```
Issue (well-specified)
        ↓
Branch + code + PR (human or agent)
        ↓
Review + merge
        ↓
PRD milestone updated: shipped
```

---

## Repo Structure

Installed into your existing repo:

```
your-repo/
├── delineate/
│   ├── agents.md              # Workflow instructions for any AI agent
│   ├── config.yml             # Repo paths, support tool config
│   ├── problems/
│   │   ├── _patterns.md       # Pattern clusters across problems + feedback
│   │   └── *.md               # Individual problem files
│   ├── feedback/
│   │   └── *.md               # Structured customer feedback
│   ├── prd/
│   │   └── *.md               # Living PRDs with milestone status
│   ├── decisions/
│   │   └── *.md               # Records of significant choices and rejected alternatives
│   └── templates/
│       ├── problem.md
│       ├── feedback.md
│       ├── prd.md
│       ├── decision.md
│       └── shaped-issue.md
└── ... (your existing code)
```

### Problem template

```markdown
# [Problem title]

## Who it affects
[User segment or internal role]

## Evidence
- [Source]: [what was observed]
- [Source]: [what was observed]

## Impact
[High / Medium / Low — with reasoning]

## Frequency
[How often this occurs, or how many users are affected]

## Related
- [Links to other problems or feedback files]
```

### Feedback template

```markdown
# "[Customer's exact words]"

## Source
[support-tool:conversation:id]

## Customer
[Segment, context — what they were trying to do]

## Their words
[Full quote in customer language, before any product translation]

## Frequency
- [N similar conversations in last N days]
- [Tags if available]

## Related
- [Links to other feedback or problem files]
```

### PRD template

```markdown
---
status: [draft | active | implemented]
---

# [Project name]

## Problems this solves
- [Link to problem files]

## Approach
[How we're solving it — and what alternatives were considered and rejected]

## Experience
[What should this feel like? Concrete experiential intent — not aesthetics for aesthetics' sake, but the quality of the interaction we're aiming for.]

## Non-goals
[What we're explicitly choosing not to solve, and why]

## Milestones
Each milestone delivers a complete, functional increment. M1 is a simple cake. M2 adds layers. M3 adds decoration. If only M1 ships, users still have something whole and useful.

### M1: [Name]
status: [draft | active | shipped]

[Scope, assumptions, open questions]

### M2: [Name]
status: [draft | active | shipped]

...

## Open questions
- [Unresolved decisions that need evidence or discussion]
```

### Decision template

```markdown
# [Decision title]

## Context
[What prompted this decision — link to problem, feedback, or PRD section]

## Options considered
1. **[Option A]** — [tradeoffs]
2. **[Option B]** — [tradeoffs]
3. **[Do nothing]** — [tradeoffs]

## Decision
[What we chose and why]

## Consequences
[What this enables, what it closes off, what we'll need to revisit]
```

### Shaped issue template

Used when creating issues in your tracker. The format adapts to whatever tool you use — the structure is what matters.

```markdown
## [Issue title]

**Context:** [Link to PRD section and problem that motivated this]

**Description:** [What needs to be done and why]

**Acceptance Criteria:**
- [How we know this is done]

**Code Pointers:**
- [Relevant files, functions, modules]

**Out of Scope:**
- [What this issue explicitly does not cover]
```

---

## PRD Lifecycle

PRDs are version-controlled documents. They don't get replaced — they get updated, with diffs tracked via git commits.

```
draft → active → implemented
           ↑          |
           └──────────┘
         (requirements change,
          new commits with diffs)
```

**Draft:** Being written. Not guiding work yet. The agent can help author it but won't shape issues from it.

**Active:** Guiding current work. Issues are shaped from its milestones. When requirements change, the PRD is *edited* — the commit message explains why. Milestones within the PRD transition independently: `draft → active → shipped`.

**Implemented:** All milestones shipped. The PRD now describes current state — it's documentation of *why the code is the way it is.* When new requirements emerge for the same area, the PRD moves back to `active`, gets updated, and new milestones are added.

The git history tells the full story. `git log delineate/prd/funnel-v2.md` shows every scope change, when it was made, and why. For significant strategic choices where meaningful alternatives were evaluated — "we chose batch over realtime CDR processing" — a decision record in `decisions/` captures the options considered, tradeoffs weighed, and reasoning. Commits capture *what changed*. Decision records capture *what was considered*.

### How agents distinguish future state from current state

The agents.md instruction:

> When reading PRDs, check milestone status. Only shape issues from milestones marked `active`. Milestones marked `shipped` describe current state — reference them for context but do not create work from them. Milestones marked `draft` are not yet approved for work.

---

## agents.md (The Workflow Engine)

The `agents.md` file encodes the workflow as instructions any AI coding agent can follow — Claude Code, Cursor, Copilot, Windsurf, or whatever comes next. It defines three commands:

### `delineate:surface`
Read all problems and feedback. Identify patterns — multiple signals pointing to the same underlying issue. For each pattern, consider the deletion algorithm: can this be solved by deleting a feature? By simplifying an existing flow? Only propose new work after deletion and simplification are exhausted. Present a prioritized list with reasoning, confidence levels, and proposed response type (build / change / remove / do nothing).

### `delineate:define`
Read the prioritized problems. Draft a PRD with milestones, non-goals, and open questions. Each milestone should deliver a complete, functional increment — not a phase of construction. Present to the human for review. After approval, shape issues from active milestones using the shaped issue template, created in the team's tracker (e.g., `gh issue create` for GitHub, Linear API, or manual entry).

### `delineate:shape`
Read a specific active PRD milestone and the surrounding context (full PRD, related problems, related feedback). Produce one or more issues, each with: description, context linking to the PRD section, acceptance criteria, code pointers, and out-of-scope notes. Create them in the team's issue tracker.

A human can run any of these modes manually using the same templates. The agent accelerates the process — it doesn't own it.

---

## Feedback Integration

Customer feedback enters via MCP servers or CLI tools connected to support platforms. The integration is intentionally simple: structured feedback files in `delineate/feedback/`, one per conversation or ticket.

Supported input channels (via MCP/CLI):
- **Intercom** — conversation summaries with customer quotes
- **Zendesk** — ticket data with tags and frequency
- **Plain** — thread summaries
- **Manual** — paste a quote, the agent structures it

The agent doesn't need to understand every support tool's API. It needs structured markdown files with: who said it, what they said (in their words), how often it happens, and what they were trying to do. The MCP integration produces these files. The workflow consumes them.

---

## What This Isn't

- **Not an app.** No server, no database, no UI. It's files in a repo with a workflow encoded in `agents.md`.
- **Not a project management tool.** No story points, sprints, velocity charts, or burndown. No Gantt charts. No status meetings.
- **Not a wiki.** PRDs live next to the code they shape, versioned with meaningful commit messages, readable by agents.
- **Not agent-only.** Every step works by hand. The templates are useful even without an AI agent. The agent makes the workflow faster, not possible.
- **Not additive-only.** The workflow's first instinct is to question whether work should exist, not to create more of it.

---

## Success Metrics

### Does the workflow produce better outcomes?

| Metric | What It Proves | How to Measure |
|--------|---------------|----------------|
| **First-pass shippability** | Issues shaped through the workflow are precise enough to execute without clarification | % of shaped issues that ship without rework or scope questions |
| **Decision traceability** | Anyone can find *why* something was built | Time to trace any shipped feature back to the problem and PRD section that motivated it |
| **Deletion rate** | The workflow actually considers removal and simplification | % of surfaced problems where the response was "remove" or "simplify" rather than "build" |
| **Feedback-to-action time** | Customer problems reach product decisions | Time from feedback pattern identified to PRD updated or decision recorded |
| **Spec quality over time** | The workflow improves as the repo accumulates context | First-pass shippability trending upward as PRDs and problems accumulate |

---

## Milestones

### M1: The workflow works by hand
status: draft

The repo structure, templates, and issue template exist. A human can capture problems, write PRDs, and shape issues using the templates without any agent involvement. The workflow is usable on day one, before any agents.md is written.

- [ ] Repo structure: `delineate/` directory with all subdirectories
- [ ] Problem template with structured fields
- [ ] Feedback template with customer-language-first structure
- [ ] PRD template with milestone status and frontmatter
- [ ] Shaped issue template
- [ ] README explaining the workflow and how to use it manually
- [ ] First real problem captured using the template
- [ ] First real PRD written from that problem

**Done when:** A human can go from "here's a problem" to "here's an issue ready for execution" using only the templates and git.

### M2: The agent workflow works
status: draft

agents.md is written. An agent can run the three modes: surface, define, shape. The agent reads existing context before writing. The agent considers deletion and simplification before proposing new work.

- [ ] agents.md with all three workflow modes
- [ ] Agent can read all problems and feedback, identify patterns, and propose priorities
- [ ] Agent applies the deletion algorithm: question → delete → simplify → build
- [ ] Agent can draft a PRD from prioritized problems
- [ ] Agent can shape issues from an active PRD milestone and create them in the team's tracker
- [ ] Agent reads full PRD context before shaping individual issues
- [ ] config.yml for pointing to product repo paths

**Done when:** An agent can go from "read the problems" to "here are 3 well-shaped issues" with the human reviewing and approving at each stage.

### M3: Feedback integration
status: draft

MCP server or CLI hook connects at least one customer support tool. Feedback flows into `delineate/feedback/` as structured markdown. The agent can read feedback alongside problems when surfacing patterns.

- [ ] MCP server spec for support tool integration (Intercom, Zendesk, or Plain)
- [ ] Feedback files auto-created from support conversations
- [ ] Agent reads feedback + problems together when surfacing patterns
- [ ] Pattern detection works across both input channels

**Done when:** Customer feedback from a real support tool flows into the repo and influences problem prioritization without manual copy-paste.

### M4: Distribution
status: draft

Anyone can install Delineate into their repo. Documentation, examples, and an init script exist.

- [ ] `npx delineate init` (or equivalent) scaffolds the directory structure
- [ ] Example problems, feedback, and PRD for reference
- [ ] README with getting-started guide
- [ ] config.yml documented with all options
- [ ] Works with any git repo and any issue tracker

**Done when:** A team that has never seen Delineate can install it and run the workflow within 30 minutes.

---

## Open Questions

1. **Template evolution.** The templates are opinionated. Will teams need to customise them heavily, or does the structure work broadly? Start rigid, loosen based on feedback.

2. **Pattern detection quality.** Can agents reliably identify patterns across problems and feedback, or do they surface spurious connections? The quality of the Surface mode depends on this.

3. **PRD authoring quality.** The workflow assumes someone (human or agent) can write a PRD precise enough to shape issues from. Writing good PRDs is hard — the templates help, but the skill gap may be the real bottleneck.

4. **Feedback volume.** High-volume support teams may produce hundreds of feedback files. How does the agent handle scale? May need summarisation or sampling before pattern detection.

5. **Multi-repo support.** If a team has multiple product repos, does Delineate live in one of them or in a standalone repo? The config.yml should support pointing to multiple codebases, but the workflow may need adjustment.

---

## Future Directions

If the workflow proves valuable:

1. **Analytics integration** — agent monitors metrics and surfaces when PRD assumptions go stale. Enables a Detect loop: live data triggers PRD review.
2. **Structured ontology** — business context (user segments, metrics definitions, constraints) as a structured layer that agents read before shaping work.
3. **Agent learning loop** — track which agent proposals get accepted/rejected, feed back into prompt quality over time.
4. **GUI layer** — a lightweight visualisation of the workflow state. The workflow already works without it; the GUI makes it spatial.
5. **Review intelligence** — risk-score shaped issues based on scope, affected code, and test coverage.

---

*Delineate: product thinking that lives where the code lives.*
