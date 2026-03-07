## Create config.yml for repo and workflow configuration

**Context:** [PRD M2: The agent workflow works](../prd/delineate-v1.md#m2) — agents.md needs to know where things live and how the team works. config.yml is the bridge between the generic workflow and a specific team's setup.

**Description:** Create `delineate/config.yml` with configuration for: Delineate directory paths (defaults that work out of the box), issue tracker settings (which tool, any CLI flags), and the commit model preference (propose vs. commit). Keep it minimal — only settings that the agent actually needs to read. Don't configure things that can be inferred.

**Acceptance Criteria:**
- [ ] `delineate/config.yml` exists with sensible defaults
- [ ] Issue tracker configuration: type (github, linear, jira, manual) and any required flags
- [ ] Commit model: `propose` (default) or `commit`
- [ ] Paths are optional — defaults to the standard `delineate/` structure
- [ ] The file is self-documenting — comments explain each option
- [ ] agents.md references config.yml for team-specific settings

**Code Pointers:**
- `delineate/agents.md` (reads this config)
- `delineate/templates/` (paths referenced in config)

**Out of Scope:**
- Support tool / MCP configuration — that's M3
- Multi-repo configuration — deferred
- Any configuration that requires a build step or tooling
