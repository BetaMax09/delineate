---
status: draft
---

# Delineate v1

## Problems this solves
- [Product specification is now the bottleneck, not engineering](../problems/product-specification-bottleneck.md)

Product teams using AI coding agents can build anything in hours — but have no structured system for deciding *what* to build, capturing *why*, and specifying work precisely enough that an agent can execute it without questions. The specification layer between "we have a problem" and "here's a shaped issue" is missing, ad-hoc, or trapped in tools agents can't read.

Engineering speed has outrun product thinking. PRDs live in Notion or Google Docs — disconnected from the codebase, invisible to agents, stale within days. The cost of building has collapsed, removing the friction that used to protect teams from building the wrong thing. Without a structured specification workflow, speed produces regret effort: features nobody needed, rework from unclear requirements, and decisions that can't be traced three months later.

## Approach
Delineate is a structured product thinking workflow that lives in the repo as markdown files and a directory convention. No app, no server, no accounts — git is the database, your AI coding agent is the runtime.

The workflow moves through three modes — **Surface** (problems and feedback become prioritised patterns), **Define** (priorities become PRDs with milestones), and **Deliver** (milestones become shaped issues in your tracker). An `agents.md` file encodes the workflow as instructions any AI agent can follow. Humans use the same templates and structure.

The key insight: if your specification is precise enough that an agent can execute it without questions, the coordination and execution layers become commodity infrastructure. Own the thinking, not the doing.

**Alternatives considered and rejected:**
- **Build an app.** A UI, a database, a SaaS product. Rejected because the value is in the workflow and the proximity to code, not in the interface. An app creates a new silo; files in the repo eliminate one. Apps require adoption friction (accounts, onboarding, pricing); repo files require `git clone`.
- **Build an agent-only tool.** Make it purely an AI workflow that humans monitor. Rejected because the workflow needs to work by hand first — the templates are useful even without an agent. Agent acceleration is a feature, not a requirement.
- **Integrate into existing PM tools.** Build a Notion plugin, a Linear extension. Rejected because these tools are the problem — they keep specifications disconnected from the code. The workflow needs to live where the code lives.

## Experience
Using Delineate should feel like having a sharp, opinionated collaborator who asks better questions than you'd ask yourself. The first instinct is always to question whether work should exist — not to create more of it.

For the product person: it should feel like your thinking has a place to live that doesn't go stale, that your engineering team (and their agents) can actually read and act on, and that the reasoning behind every decision is traceable without asking anyone.

For the developer or agent: it should feel like receiving a brief so clear that you can start working without asking clarifying questions. Context, scope, non-goals, and acceptance criteria — all in one place, linked to the problem that motivated it.

The workflow should never feel like bureaucracy. If capturing a problem takes longer than describing it in Slack, the template is too heavy. If writing a PRD feels like filling out a form, the structure is too rigid. The system should make thinking faster, not slower.

## Non-goals
- **Not replacing project management.** No sprints, velocity, story points, or burndown charts. Delineate owns the specification layer — what to build and why. Your existing tools own execution — how and when.
- **Not automating product decisions.** The agent surfaces patterns, proposes priorities, and drafts specifications. Humans decide. The agent accelerates the workflow; it doesn't own the judgment calls.
- **Not building a UI.** No dashboard, no web app, no visual interface. If a GUI layer proves valuable later, it's a future direction — not a launch requirement.
- **Not solving for large enterprise workflows.** V1 is for small-to-medium product teams (1-10 people) who ship fast and need structure without overhead. Enterprise governance, compliance, and multi-team coordination are out of scope.
- **Not building MCP integrations yet.** Feedback integration with support tools (Intercom, Zendesk, Plain) is a future milestone. V1 focuses on the core workflow — problems, PRDs, and shaped issues — using manual input.

## Milestones
Each milestone delivers a complete, functional increment. M1 is a simple cake. M2 adds layers. M3 adds decoration. If only M1 ships, users still have something whole and useful.

### M1: People can understand what Delineate is and start using the workflow by hand
status: shipped

A README that clearly communicates what Delineate is, who it's for, and the problem it solves — written for a mixed audience of product people and developers. Alongside it, the repo structure and templates exist so anyone can start using the workflow manually with nothing but a text editor and git.

This is the minimum viable whole cake: someone discovers the repo, understands the concept, and can immediately start capturing problems and writing PRDs using the templates.

**Scope:**
- README.md — practical, clear explanation of what Delineate is, the workflow, and how to start using it by hand
- Repo structure: `delineate/` directory with `problems/`, `prd/`, `feedback/`, `decisions/`, `templates/`
- All five templates: problem, feedback, PRD, decision, shaped issue
- This PRD and its source problem file — dogfooding the workflow from day one

**Acceptance criteria:**
- [ ] A product person with no prior context can read the README and explain what Delineate does in one sentence
- [ ] A developer can clone the repo and start capturing a problem using the template within 5 minutes
- [ ] The README communicates the core thesis (specification is the bottleneck) without requiring the full spec to be read
- [ ] The tone is practical-first — what it does, then why it matters
- [ ] The repo contains a real problem file and a real PRD (this one) as working examples of the workflow

**Open questions:**
- How much of the workflow detail belongs in the README vs. a separate getting-started guide?
- Should the README include a quick visual (ASCII diagram) of the Surface > Define > Deliver flow?

### M2: The agent workflow works
status: shipped

`agents.md` is written and an AI coding agent can run the three workflow modes: `delineate:surface`, `delineate:define`, `delineate:shape`. The agent reads existing context (problems, feedback, PRDs) before writing. The agent considers deletion and simplification before proposing new work.

This milestone turns Delineate from "templates you fill in by hand" to "a workflow where an agent does the heavy lifting and a human reviews and decides." The human can still do everything manually — the agent makes it faster.

**Scope:**
- `agents.md` with instructions for all three workflow modes
- `config.yml` for pointing to product repo paths and issue tracker
- Agent can read all problems and feedback, identify patterns, and propose priorities
- Agent applies the deletion algorithm: question > delete > simplify > build
- Agent can draft a PRD from prioritised problems
- Agent can shape issues from an active PRD milestone
- Agent creates issues in the team's tracker (GitHub Issues via `gh issue create` as the first supported target)

**Acceptance criteria:**
- [ ] An agent can run `delineate:surface` and produce a prioritised pattern list from existing problem and feedback files
- [ ] An agent can run `delineate:define` and draft a PRD with milestones from prioritised problems
- [ ] An agent can run `delineate:shape` and produce well-formed issues with context, acceptance criteria, and code pointers from an active PRD milestone
- [ ] The human reviews and approves at each stage — the agent proposes, never commits unilaterally
- [ ] Issues created by the agent link back to the PRD section and problem that motivated them

**Open questions:**
- How prescriptive should `agents.md` be? Too rigid and it breaks across different agents; too loose and output quality varies.
- Should the agent commit files directly or propose them for human review via a diff?

### M3: Feedback integration and distribution
status: draft

Customer feedback flows into the workflow from at least one support tool. Anyone can install Delineate into their repo with a single command. Documentation, examples, and an init script exist.

**Scope:**
- MCP server or CLI hook for at least one support tool (Intercom, Zendesk, or Plain)
- Feedback files auto-created from support conversations in `delineate/feedback/`
- Agent reads feedback alongside problems when surfacing patterns
- `npx delineate init` (or equivalent) scaffolds the directory structure into any repo
- Getting-started guide with examples
- Works with any git repo and any issue tracker

**Acceptance criteria:**
- [ ] Customer feedback from a real support tool flows into the repo as structured markdown without manual copy-paste
- [ ] The agent's pattern detection works across both direct input (problems) and integrated input (feedback)
- [ ] A team that has never seen Delineate can install it and run the workflow within 30 minutes
- [ ] `config.yml` is documented with all options

**Open questions:**
- Which support tool to integrate first? Likely whichever has the best MCP server or API.
- How to handle high-volume feedback without overwhelming the repo with files?

## Open questions
- **Template rigidity vs. flexibility.** The templates are opinionated. Will teams need to customise them heavily, or does the structure work broadly? Start rigid, loosen based on feedback.
- **PRD authoring quality.** The workflow assumes someone (human or agent) can write a PRD precise enough to shape issues from. The templates help, but the skill gap may be the real bottleneck. How much can the agent compensate?
- **Multi-repo support.** If a team has multiple product repos, does Delineate live in one of them or in a standalone repo? Defer to M3 or later.
