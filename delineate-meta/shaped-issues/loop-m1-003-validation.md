## Create the validation script

**Context:** [PRD M1: The loop executes shaped issues](../prd/002-draft-autonomous-loop.md) — motivated by [The product workflow can't run autonomously](../problems/autonomous-workflow-execution.md). Backpressure that keeps the autonomous loop on track. Without validation, the agent can drift, produce malformed output, or break the workflow structure.

**Description:** Create `delineate/validate.sh` — a script the agent runs after each piece of work to check structural integrity. This is the backpressure mechanism. Start with structural checks (can be automated); content quality checks come later.

Checks to implement:
1. **Template conformance** — do all files in `problems/`, `prd/`, `feedback/`, `decisions/` contain the required sections from their respective templates?
2. **PRD frontmatter** — do all PRDs have valid `status:` frontmatter (draft | active | implemented)?
3. **Milestone status** — do all milestones in PRDs have valid status (draft | active | shipped)?
4. **Link integrity** — do cross-references between files (problem → PRD, shaped issue → PRD) point to files that actually exist?
5. **Shaped issue completeness** — do all shaped issues have Context, Description, Acceptance Criteria, and Out of Scope sections?

**Acceptance Criteria:**
- [ ] `delineate/validate.sh` exists and is executable
- [ ] Returns exit code 0 when all checks pass, non-zero when any fail
- [ ] Outputs clear error messages identifying which file failed which check
- [ ] Runs in under 5 seconds on a repo with 50+ files
- [ ] The loop script calls this after each iteration and stops on failure

**Code Pointers:**
- `delineate/templates/` — the reference structure for each file type
- `delineate/problems/`, `delineate/prd/`, `delineate/shaped-issues/` — files to validate
- `loop.sh` — calls this script as backpressure

**Out of Scope:**
- Content quality checks (is the PRD well-written? Is the problem real?) — that's human judgment
- Linting markdown formatting — structural integrity only
- Checking external links or issue tracker state
