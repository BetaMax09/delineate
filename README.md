# Delineate

A product thinking framework that lives in your repo.

---

## The problem

AI has made engineering fast. The bottleneck has flipped — the hard part isn't building, it's knowing the right thing to build. Specifying the right thing to build is now harder than building it.

When building is nearly free, every idea gets built. PRDs live in Notion or Google Docs — disconnected from the code, unreadable by agents, stale within days. Decisions happen in Slack and memory, lost within weeks. Three months later, nobody remembers why a feature was scoped a certain way.

The specification layer is missing. Delineate is that layer.

## What it is

Delineate is a structured workflow for going from fuzzy problems to well-specified, shaped issues — using the same process whether a human or an agent is doing it.

It's not an app. It's a set of markdown templates, a directory structure, and a workflow you install into your repo. Git is the database. Your AI coding agent is the runtime. Fork it, customise it, inspect it. It's just files.

If your spec is precise enough that an agent can execute it without questions, the coordination and execution layers become commodity infrastructure. Own the thinking, not the doing.

## The workflow

Three modes, used by humans or agents interchangeably.

**Surface** — Problems and feedback become patterns, then priorities. The first instinct is always to question whether work should exist: can this be solved by removing something? By simplifying something that already exists? Only after deletion and simplification are exhausted does it propose new work.

**Define** — Priorities become a PRD with milestones. Each milestone delivers a complete, functional increment — a whole cake, not a foundation waiting for walls. The PRD is a living document, updated with diffs, not replaced. `git log` on the PRD file is the decision history.

**Deliver** — Active milestones become shaped issues with context, acceptance criteria, and code pointers. Issues go into your tracker — GitHub Issues, Linear, Jira, whatever you use. By the time an issue reaches execution, it's well-specified enough that an agent can execute it without questions.

```
Problems + Feedback
        ↓
   Surface: find patterns, prioritise
   (delete/simplify before building)
        ↓
   Define: PRD with milestones
   (human reviews, edits, commits)
        ↓
   Deliver: shaped issues in your tracker
   (well-specified, ready for execution)
```

## Repo structure

Install into your existing repo:

```
your-repo/
└── delineate/
    ├── problems/       # Structured problem files
    ├── feedback/       # Customer feedback in their own words
    ├── prd/            # Living PRDs with milestone status
    ├── decisions/      # Records of significant choices
    ├── shaped-issues/  # Issues shaped from active milestones
    └── templates/      # Templates for all of the above
```

## Getting started

1. Copy the `delineate/` folder into your repo.
2. Capture a problem: copy `templates/problem.md`, fill in the brackets.
3. Write a PRD: copy `templates/prd.md`, link it to your problem, define milestones.
4. Shape issues: copy `templates/shaped-issue.md`, write issues from your active milestone.
5. Create the issues in your tracker and build.

No agent required. The templates work by hand with a text editor and git. When you're ready for agent acceleration, add an `agents.md` file — the agent uses the same workflow you do.

## Principles

**Question, delete, simplify — then build.** The first response to any problem is never "let's add a feature." If you're not adding back 10% of what you deleted, you didn't delete enough.

**Requirements live at the codebase.** PRDs belong in the repo, version-controlled alongside the code they shape, readable by the same agents that will write that code.

**Start with evidence, not solutions.** Problems and feedback are the raw material. Solutions are derived, never assumed.

**Humans and agents use the same workflow.** The agent accelerates the workflow; it doesn't gatekeep it.

**Craft is a competitive advantage.** "How does this feel?" is asked during shaping, not after shipping.

**Every milestone delivers a whole cake.** M1 is a simple cake. M2 adds layers. M3 adds decoration. If only M1 ships, users still have something whole.

## What this isn't

- **Not an app.** No server, no database, no UI. Files in a repo.
- **Not project management.** No story points, sprints, velocity charts, or burndown.
- **Not agent-only.** Every step works by hand. The agent makes it faster, not possible.
- **Not additive-only.** The workflow's first instinct is to question whether work should exist.

## See it in action

This repo uses Delineate to build itself. See the [first problem](delineate/problems/product-specification-bottleneck.md), the [first PRD](delineate/prd/delineate-v1.md), and the [shaped issues](delineate/shaped-issues/) that came from it.

---

*Product thinking that lives where the code lives.*
