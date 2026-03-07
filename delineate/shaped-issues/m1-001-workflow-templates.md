## Create the four remaining workflow templates

**Context:** [PRD M1: People can understand what Delineate is and start using the workflow by hand](../prd/delineate-v1.md#m1) — templates are the core of the manual workflow. Without them, there's nothing for a user to start with.

**Description:** Create the problem, feedback, PRD, and decision templates as files in `delineate/templates/`. The shaped issue template already exists. These templates are defined in `delineate.md` (the spec) — pull them from there, but they live as standalone files a user can copy and fill in. The templates should work as-is: a user copies one, fills in the brackets, and has a well-structured artifact.

**Acceptance Criteria:**
- [ ] `delineate/templates/problem.md` exists with structured fields: title, who it affects, evidence, impact, frequency, related
- [ ] `delineate/templates/feedback.md` exists with customer-language-first structure: source, customer context, their words, frequency, related
- [ ] `delineate/templates/prd.md` exists with frontmatter status, problems this solves, approach, experience, non-goals, milestones with status, open questions
- [ ] `delineate/templates/decision.md` exists with context, options considered, decision, consequences
- [ ] Each template is self-explanatory — placeholder text in brackets explains what goes there

**Code Pointers:**
- Template definitions in `delineate.md` lines 174-293
- `delineate/templates/shaped-issue.md` (already created, use as reference for format)

**Out of Scope:**
- Template customisation or configuration — start rigid, loosen later
- Any tooling to auto-generate from templates — that's M2 (agents.md)
