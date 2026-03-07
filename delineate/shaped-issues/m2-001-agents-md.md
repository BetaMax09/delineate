## Write agents.md — the workflow engine

**Context:** [PRD M2: The agent workflow works](../prd/delineate-v1.md#m2) — motivated by [Product specification is now the bottleneck](../problems/product-specification-bottleneck.md). This is the file that turns Delineate from templates into a workflow. Without it, Delineate is a folder of markdown files. With it, any AI coding agent can run the Surface/Define/Shape workflow.

**Description:** Write `delineate/agents.md` using the structured intent approach — define the workflow steps, expected inputs and outputs, and principles to follow, but let the agent reason about how. The file defines three commands (`delineate:surface`, `delineate:define`, `delineate:shape`) that any AI agent can follow.

The file should:
- Open with Delineate's core principles (deletion algorithm, evidence before solutions, whole-cake milestones)
- Define each workflow mode with: when to use it, what to read, what to produce, what format to output
- Include the commit model as configurable: agent can propose changes for human review (default) or commit directly, based on team preference
- Reference the templates so the agent knows the expected structure
- Be agent-agnostic: works with Claude Code, Cursor, Copilot, Windsurf, or any agent that reads markdown instructions

**Acceptance Criteria:**
- [ ] `delineate:surface` — agent reads `problems/` and `feedback/`, identifies patterns, applies deletion algorithm, outputs a prioritised list with evidence, response type (build/change/remove/do nothing), and confidence
- [ ] `delineate:define` — agent reads prioritised problems, drafts a PRD using `templates/prd.md` structure, with milestones that each deliver a whole cake
- [ ] `delineate:shape` — agent reads a specific active PRD milestone plus full context (PRD, problems, feedback), produces shaped issues using `templates/shaped-issue.md` structure
- [ ] Each mode states what the agent reads, what it produces, and what the human reviews
- [ ] Commit model is configurable (propose vs. commit)
- [ ] Principles section encodes: question > delete > simplify > build
- [ ] The file works as a standalone instruction — an agent reading only agents.md and the templates can run the workflow

**Code Pointers:**
- `delineate/templates/` — all five templates the agent references
- `delineate/problems/` and `delineate/prd/` — existing examples of the workflow in action
- README.md — workflow description (agents.md should be consistent but more detailed)

**Out of Scope:**
- MCP integration or feedback auto-ingestion — that's M3
- Agent-specific instructions (Claude Code flags, Cursor rules) — agents.md is agent-agnostic
- Issue tracker API calls — the agent uses whatever CLI the team has (e.g. `gh issue create`), not a built-in integration
