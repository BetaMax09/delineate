## Write the build prompt

**Context:** [PRD M1: The loop executes shaped issues](../prd/002-draft-autonomous-loop.md) — motivated by [The product workflow can't run autonomously](../problems/autonomous-workflow-execution.md). The build prompt is the entry point for autonomous execution. It tells the agent: here's where you are, here's how to figure out what to do next, here's how to do it.

**Description:** Create `PROMPT_build.md` at the repo root. This is the file that gets piped into the agent on each loop iteration. It should:

1. Orient the agent: read `delineate/agents.md` for the workflow, read `delineate/config.yml` for settings
2. Assess state: read `delineate/prd/*.md`, find milestones marked `active`, read `delineate/shaped-issues/` for work to do
3. Pick the next issue: select the first unfinished shaped issue for the active milestone
4. Execute: do the work described in the shaped issue
5. Validate: check acceptance criteria, run `./delineate/validate.sh` if it exists
6. Commit: if `commit_model: commit`, stage and commit with a descriptive message referencing the shaped issue
7. Signal completion: update the shaped issue or mark it done so the next iteration doesn't pick it up again

The prompt must work with a fresh context window each iteration — no memory between runs. All state comes from disk.

**Acceptance Criteria:**
- [ ] `PROMPT_build.md` exists at repo root
- [ ] An agent reading only this file can orient itself, find work, and execute it
- [ ] The prompt references `agents.md` for principles and workflow rules
- [ ] The prompt handles the case where no active milestones or unfinished issues exist (graceful stop)
- [ ] Each iteration is self-contained — no dependency on previous context windows

**Code Pointers:**
- `delineate/agents.md` — workflow instructions the prompt references
- `delineate/config.yml` — commit model and tracker settings
- `delineate/prd/` — where the agent finds active milestones
- `delineate/shaped-issues/` — where the agent finds work to do

**Out of Scope:**
- The loop script itself (separate issue)
- Validation script (separate issue)
- Planning mode prompt — this is build-only
