# The product workflow can't run autonomously

## Who it affects
Product teams and developers using Delineate with AI coding agents. Specifically, anyone who has shaped issues ready for execution and wants the agent to work through them without constant prompting.

## Evidence
- Internal: Delineate now has agents.md with three workflow modes — but each mode requires a human to manually invoke the agent, point it at the right files, and prompt it with the right command. The workflow is defined but not operational.
- Internal: Building Delineate itself required manual orchestration at every step — "now write the templates", "now write the README", "now shape the issues." The shaped issues had clear acceptance criteria, but the agent couldn't pick them up and execute them without being told.
- External (Ralph Wiggum pattern): The loop mechanism — a script that repeatedly invokes the agent with a prompt, letting it read state from disk between iterations — demonstrates that autonomous execution is possible when the specification is clear enough. The loop is dumb; the prompt is smart.
- External: Agentic coding is moving from "agent does one task" to "agent works continuously for hours" — but only when the agent has persistent state, clear task boundaries, and backpressure mechanisms to catch drift.

## Impact
High — this is the difference between "a workflow the agent follows when prompted" and "a workflow that runs." Without autonomous execution, Delineate requires the same hand-holding it was designed to eliminate. The specification layer is only valuable if an agent can consume it and execute against it without constant human intervention. Surface and Define are inherently human-in-the-loop (judgment calls), but Shape and Deliver should be autonomous once the decisions are made.

## Frequency
Every time someone has a PRD with active milestones and shaped issues. The manual prompting overhead scales linearly with the number of issues — the more shaped work exists, the more painful the lack of autonomy becomes.

## Related
- delineate/problems/product-specification-bottleneck.md
- delineate/prd/002-draft-autonomous-loop.md
