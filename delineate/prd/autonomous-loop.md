---
status: draft
---

# Autonomous Execution Loop

## Problems this solves
- [The product workflow can't run autonomously](../problems/autonomous-workflow-execution.md)

Delineate defines a structured workflow (Surface > Define > Shape > Deliver) and agents.md encodes it as instructions any agent can follow. But the agent can't run the workflow without constant human prompting. Each step requires manual invocation — "now read the problems", "now draft the PRD", "now shape the issues." The specification is clear enough for autonomous execution; the mechanism to run it doesn't exist.

## Approach
A loop mechanism inspired by the Ralph Wiggum pattern: a simple script repeatedly invokes the agent with a build prompt, each iteration in a fresh context window. The agent reads Delineate's own state from disk (PRDs, shaped issues, acceptance criteria), picks the next piece of work, executes it, validates the output, and commits. The loop is dumb; the prompt is smart.

The key insight: Surface and Define are judgment calls — they stay human-in-the-loop. Shape and Deliver are execution — once a milestone is `active` and issues are shaped, the agent should be able to work through them autonomously. Backpressure (validation, acceptance criteria checks) catches drift.

**Alternatives considered and rejected:**
- **Build a custom orchestrator.** A daemon or service that watches the repo and dispatches agent tasks. Rejected — too much infrastructure for the value. A bash loop with a smart prompt does the same thing with zero dependencies.
- **Rely on the agent's own session memory.** Let a single long-running agent session work through all issues. Rejected — context windows fill up, quality degrades, and a crash loses all state. Fresh context per iteration with state on disk is more resilient.
- **Make all modes autonomous.** Let the agent run Surface and Define without human review. Rejected — these are the highest-leverage decisions in the workflow. Automating judgment calls defeats the purpose of Delineate.

## Experience
Running the loop should feel like delegating to a capable junior who reads the brief, does the work, and checks their own output. You kick it off, check in periodically, and review the commits. When it stops — either because work is done or validation failed — you know exactly where it got to and why.

It should not feel like babysitting. If you're watching every iteration, the loop isn't working.

## Non-goals
- **Not orchestrating multiple agents.** One agent, one loop, sequential execution. Parallelism is a future direction.
- **Not automating Surface or Define.** Human-in-the-loop for what to build and why. The loop only handles execution of already-shaped work.
- **Not building a daemon or service.** It's a script you run. When it's done, it's done.
- **Not agent-specific.** The loop script invokes a command. Claude Code first, but the design should work with any CLI-invokable agent.

## Milestones

### M1: The loop executes shaped issues
status: draft

The build prompt, loop script, and validation exist. An agent can pick up shaped issues from an active milestone, execute them sequentially, validate output, and commit — without human prompting between iterations.

**Scope:**
- `PROMPT_build.md` — bootstraps the agent into Delineate context each iteration
- `loop.sh` — invokes the agent repeatedly with fresh context
- `delineate/validate.sh` — structural checks as backpressure (template conformance, link integrity, frontmatter validity)
- Shaped issue lifecycle: a convention for marking issues as done so the next iteration doesn't re-pick them

**Acceptance criteria:**
- [ ] An agent can pick up a shaped issue, execute it, and commit — without human prompting
- [ ] The loop continues across multiple issues until the milestone is complete or validation fails
- [ ] Each iteration starts with a fresh context window and reads state from disk
- [ ] Backpressure catches malformed files, missing template sections, and broken cross-references
- [ ] The loop stops gracefully when no unfinished issues remain or when validation fails
- [ ] Works with Claude Code as the first target

**Open questions:**
- What convention marks a shaped issue as "done"? Options: move to a `done/` folder, add a `status: done` frontmatter, or delete the file after the corresponding tracker issue is created.
- How to handle failures mid-loop — retry the same issue, skip it, or stop and alert?
- Should the loop log to a file or to stdout?

### M2: Configurable autonomy boundaries
status: draft

The team can configure which workflow stages run autonomously and which pause for human review. The defaults are safe (Surface and Define pause, Shape and Deliver run), but teams can adjust.

**Scope:**
- `config.yml` additions: `autonomy` settings per workflow mode
- The build prompt respects these settings — pauses when configured to
- Human notification mechanism when the loop pauses (could be as simple as printing to stdout)

**Acceptance criteria:**
- [ ] `config.yml` has clear autonomy settings per mode
- [ ] The loop pauses at the right checkpoints based on configuration
- [ ] Default configuration is safe: judgment calls require human review
- [ ] Overriding to full autonomy is a conscious team decision, not a default

**Open questions:**
- Is `config.yml` the right place for this, or should it be flags on the loop script?

## Open questions
- **Shaped issue lifecycle.** How do we track which issues the loop has completed? The repo state needs to clearly distinguish "to do" from "done" for the agent to pick up the right work.
- **Error recovery.** When the agent produces bad output and validation catches it, what's the recovery path? Retry risks infinite loops on genuinely hard problems. Stop-and-alert is safest but requires human attention.
- **Testing the loop.** How do we validate that the loop itself works, separate from testing the agent's output quality? May need a "dry run" mode.
