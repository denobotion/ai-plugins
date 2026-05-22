# Changelog

All notable changes to the `bitwarden-design-tools` plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-05-22

### Added

- Initial release. `bitwarden-design-tools` is the toolkit half of the design plugin pair — non-persona skills for the design lifecycle, composed by the `bitwarden-designer` agent and usable standalone.
- Six skills:
  - `content-style-guide` — Bitwarden's product content style guide for GUI copy. Ported from the `designer-agent-skills` branch in `bitwarden/clients`, with progressive disclosure into `references/grammar-mechanics.md` and `references/accessibility-rules.md`.
  - `using-figma` — read and inspect Figma designs via the Dev Mode MCP server. Per-job-to-be-done tool selection across the Figma MCP, with progressive disclosure into `references/figma-mcp-tools.md` and `references/setup.md`.
  - `applying-bitwarden-branding` — apply Bitwarden brand standards (logo, color, typography, iconography, capitalization) grounded in [bitwarden.com/brand](https://bitwarden.com/brand/) and the [bitwarden/brand](https://github.com/bitwarden/brand) repository. Full palette and asset inventory in `references/color-palette.md` and `references/brand-assets.md`.
  - `preparing-design-handoff` — prepare the Confluence handoff page, Figma Ready-for-Dev state, and Jira transitions. Full handoff template field reference in `references/handoff-template.md`.
  - `evolving-design-system-components` — propose new patterns or modify existing components per the published governance process. Figma conventions in `references/figma-conventions.md`.
  - `navigating-design-jira-process` — design tasks nested under engineering epics, the 30/60/90 iteration cadence, status transitions, and the one-off engineering story flow.
- Required cross-plugin dependency on `bitwarden-atlassian-tools` for Confluence access to the canonical design-team process pages.
