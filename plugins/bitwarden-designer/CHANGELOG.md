# Changelog

All notable changes to the `bitwarden-designer` plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-05-22

### Added

- Initial release. `bitwarden-designer` is a product designer agent that grounds design work in the Bitwarden design team's Code of Conduct, the 30/60/90 critique framework, and the product content style guide — and in the documented processes around design review, design-to-engineering handoff, Design System evolution, and the Product and Design Jira workflow.
- `bitwarden-designer` agent with stage-aware critique dispatch and explicit boundaries against engineering-side counterparts (tech lead, shepherd).
- Seven skills:
  - `content-style-guide` — Bitwarden's product content style guide for GUI copy. Ported verbatim from the `designer-agent-skills` branch in `bitwarden/clients`.
  - `design-review` — Code of Conduct combined with the 30/60/90 critique framework. Ported verbatim from the `designer-agent-skills` branch in `bitwarden/clients`.
  - `using-figma` — read and inspect Figma designs via the Dev Mode MCP server. Per-job-to-be-done tool selection across the Figma MCP surface (read tools, design-system search, Code Connect, write tools), with progressive disclosure into `references/figma-mcp-tools.md` and `references/setup.md`.
  - `facilitating-design-critique` — run or participate in a Bitwarden design critique (weekly team critique or Product Design Review). Grounded in the Weekly Design Critique & Etiquette quick guide and the Product Design Review Guidelines.
  - `preparing-design-handoff` — prepare the Confluence handoff page, Figma Ready-for-Dev state, and Jira transitions. Includes the full handoff template field reference in `references/handoff-template.md`.
  - `evolving-design-system-components` — propose new patterns or modify existing components per the published governance process. Includes Figma conventions reference in `references/figma-conventions.md`.
  - `navigating-design-jira-process` — design tasks nested under engineering epics, the 30/60/90 iteration cadence, status transitions, and the one-off engineering story flow.
- Cross-plugin integration with `bitwarden-atlassian-tools` (required for Confluence access to the canonical design-team process pages).
