## Create the loop script

**Context:** [PRD M1: The loop executes shaped issues](../prd/002-draft-autonomous-loop.md) — motivated by [The product workflow can't run autonomously](../problems/autonomous-workflow-execution.md). The mechanism that keeps the agent running. Simple as possible — the intelligence is in the prompt and agents.md, not in the script.

**Description:** Create `loop.sh` at the repo root. A bash script that repeatedly invokes the AI agent with `PROMPT_build.md`, giving each iteration a fresh context window. The script should:

1. Check that `PROMPT_build.md` exists
2. Invoke the agent (Claude Code as first target: `cat PROMPT_build.md | claude`)
3. Wait for completion
4. Check exit status — if the agent signals "no more work" or hits a validation failure, stop
5. Otherwise, loop

Keep it minimal. The Ralph Wiggum insight applies: the loop is dumb, the prompt is smart.

**Acceptance Criteria:**
- [ ] `loop.sh` exists at repo root, is executable
- [ ] Invokes the agent with the build prompt on each iteration
- [ ] Each iteration gets a fresh context window
- [ ] Stops gracefully when the agent signals completion (no active milestones or no unfinished issues)
- [ ] Stops on validation failures (non-zero exit from the agent or validation script)
- [ ] Logs each iteration (timestamp, which issue was worked on, outcome)

**Code Pointers:**
- `PROMPT_build.md` — the input to each iteration
- Ralph Wiggum pattern: `while :; do cat PROMPT.md | claude ; done` as the starting point

**Out of Scope:**
- Parallel agent execution — one agent at a time for now
- Planning mode loop — this only handles build mode
- Agent-specific flags or configuration beyond the basic invocation
