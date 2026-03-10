## Write the README

**Context:** [PRD M1: People can understand what Delineate is and start using the workflow by hand](../prd/001-active-delineate-v1.md#m1) — motivated by [Product specification is now the bottleneck](../problems/product-specification-bottleneck.md). The README is the front door. If it doesn't land, nothing else matters.

**Description:** Write `README.md` at the repo root. Practical-first tone for a mixed audience of product people and developers. It should communicate: what Delineate is, the problem it solves (specification is the bottleneck, not engineering), how the workflow works (Surface > Define > Deliver), and how to start using it by hand today. The README is not the spec — it's the invitation. Keep it short enough to read in under 3 minutes.

The repo already contains working examples of the workflow (a real problem file, a real PRD, shaped issues) — the README should reference these as proof that the workflow works, not just as documentation.

**Acceptance Criteria:**
- [ ] A product person with no prior context can read it and explain what Delineate does in one sentence
- [ ] A developer can read it and start capturing a problem using the template within 5 minutes
- [ ] Communicates the core thesis without requiring the full spec (`delineate.md`) to be read
- [ ] Describes the three workflow modes (Surface, Define, Deliver) concisely
- [ ] Shows the repo structure so users know where things live
- [ ] References the real problem file and PRD as working examples
- [ ] Tone is practical-first — what it does, then why it matters
- [ ] Under 3 minutes reading time (~600-800 words)

**Code Pointers:**
- `delineate.md` for the full spec (draw from, don't duplicate)
- `delineate/problems/product-specification-bottleneck.md` (real example to reference)
- `delineate/prd/001-active-delineate-v1.md` (real example to reference)
- `delineate/templates/` (link to these for getting started)

**Out of Scope:**
- Getting-started guide or tutorial — the README points to templates, doesn't walk through a full workflow
- Installation script or `npx init` — that's M3
- Agent workflow documentation — that's M2
- The full thesis or manifesto — that lives in `delineate.md`
