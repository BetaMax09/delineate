# Product specification is now the bottleneck, not engineering

## Who it affects
Product teams — product managers, designers, and engineering leads — working with AI coding agents (Claude Code, Cursor, Copilot, Windsurf, etc.) or in any environment where engineering capacity now outpaces product specification capacity.

## Evidence
- Andrew Ng (Lenny's Podcast / No Priors, 2025): "Engineers are 10x faster. Product managers haven't sped up at the same rate. Now they're the bottleneck." His teams are flipping the PM-to-engineer ratio — proposing 2 PMs per engineer instead of 1 PM per 4 engineers, because specification is now harder than implementation.
- Boris Cherny (Claude Code creator), via Addy Osmani: When AI handles code generation, the engineer's value shifts to the decisions above the code — what to build, why, for whom, and how it fits together. The bottleneck was always judgment, taste, and systems thinking.
- Agentic coding research (Anthropic 2026 report, Andrew Crookston): 65% of developers report AI "misses context." Experienced developers using AI tools work 19% slower on their own repos — because the AI lacks the specification and documentation context to work effectively. Specs are the bottleneck, not code.
- Vibe coding discourse (5D Vision, Bryce York, Saeed Khan, 2025-2026): Vibe coding is resurrecting the feature factory. The friction that used to protect products from building the wrong thing — the cost of engineering — has disappeared. Without a structured specification layer, teams default to building everything rather than the right thing.
- Direct observation: PRDs live in Google Docs or Notion, disconnected from the code they describe, unreadable by agents, stale within days. Requirements that can't keep pace with engineering aren't requirements — they're wishes.

## Impact
High — this is the defining product problem of the agentic coding era. Teams with fast agents but no specification discipline will produce more regret effort, not less. The zero-marginal-cost trap means every unvalidated idea gets built because "it only takes a minute" — but every feature added increases cognitive load, maintenance burden, and validation noise. Speed without direction is waste.

## Frequency
Continuous. Every product team using AI coding tools hits this daily. The problem compounds — each unspecified feature creates more surface area to maintain, more decisions to untangle, and more distance between what was built and why.

## Related
- delineate/prd/delineate-v1.md
