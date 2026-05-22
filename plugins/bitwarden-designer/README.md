# Bitwarden Designer Plugin

## Overview

Product designer agent for Bitwarden. Grounds design work in the team's Code of Conduct, the 30/60/90 critique framework, and the product content style guide — and in the documented processes for design review, design-to-engineering handoff, Design System evolution, and the Product and Design Jira workflow. Treats content as first-class design and Figma as a first-class read surface via the Dev Mode MCP server.

This plugin is the design-side counterpart to the engineering-facing plugins in this marketplace. The substance of _what_ makes a design good (Code of Conduct, 30/60/90, content style guide) and the choreography of _how_ design work flows through Bitwarden (critique, handoff, Design System governance, Product and Design Jira) live here. Framework-bound code generation from designs (e.g., Figma to Angular) lives in the repos that consume it.

## Agent

| Agent                | What It Does                                                                                                                                                                                                                                                                                                                                                                                          |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `bitwarden-designer` | Bitwarden product designer. Critiques designs against the Code of Conduct and 30/60/90 framework, evaluates GUI copy against the product content style guide, reads and inspects Figma files via the Dev Mode MCP server, and walks the documented design-team processes for critique facilitation, design-to-engineering handoff, Design System evolution, and the Product and Design Jira workflow. |

## Skills

| Skill                               | What It Does                                                                                                                                                                                                                                                                                                                       |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `content-style-guide`               | Bitwarden's product content style guide for GUI copy — voice, tone, AP-style-with-exceptions grammar, sentence case in UI, no ampersands, and accessibility-first language at a U.S. 7th-grade reading level. Triggered for copy review, copy rewrite, and as a composed skill inside design review and design-to-code generation. |
| `design-review`                     | The design team's Code of Conduct combined with the 30/60/90 critique framework. Stage-appropriate critique, product-not-designer focus, content evaluated alongside visual design at 60% and 90%. Triggered for design critique requests.                                                                                         |
| `using-figma`                       | Read and inspect Figma designs via the Dev Mode MCP server. Per-job-to-be-done tool selection (`get_design_context`, `get_metadata`, `get_screenshot`, `get_variable_defs`, `search_design_system`, `get_libraries`, the Code Connect tools, and the write tools). Foundational — most other skills compose it.                    |
| `facilitating-design-critique`      | Run or participate in a Bitwarden design critique — both the weekly team critique and one-off Product Design Reviews. Roles (presenter, facilitator, participants), session arc, etiquette, and the common participation traps to catch.                                                                                           |
| `preparing-design-handoff`          | Prepare a Bitwarden design handoff — the Confluence handoff page (Background, Stakeholders, Userflows, Message Text File, Figma Prototype, Annotated Prototype), the Figma file in Ready-for-Dev state, and the Jira state transitions that go with them.                                                                          |
| `evolving-design-system-components` | Propose a new UI pattern or modify an existing Component Library component per Bitwarden's published governance process — design-team alignment, Core vs. Recipe/Snowflake with UI Foundation, Figma branching and property conventions, review gates, merge timing.                                                               |
| `navigating-design-jira-process`    | Move design work through Bitwarden's Product and Design Jira workflow — design tasks nested under engineering epics, the 30/60/90 iteration cadence, status transitions across the design and engineering boards, and the one-off engineering story flow.                                                                          |

## Cross-Plugin Integration

| Plugin                      | How It's Used                                                                                                                                                                                                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `bitwarden-atlassian-tools` | Required. Skills here reference canonical Confluence pages (Weekly Design Critique & Etiquette, Product Design Review Guidelines, Creating new design patterns, Modifying an existing component, Product and Design Jira Process) and assume `get_confluence_page` is available to fetch them directly when prepping real work. |
| `bitwarden-tech-lead`       | Counterpart on the team-side engineering surface. When design questions touch team-scope architecture (component build plans, recipe ownership, technical breakdown), surface the touchpoint and hand off to the tech lead rather than absorbing it.                                                                            |
| `bitwarden-shepherd`        | Counterpart on the cross-team initiative surface. When design questions touch initiative shaping across teams (handoff coordination for a multi-team initiative, design-system evolution that crosses team boundaries), surface the touchpoint.                                                                                 |

All cross-plugin skills are required because the plugin relies on Atlassian access for its source-of-truth Confluence pages.

## External Dependency: Figma Dev Mode MCP Server

The `using-figma` skill assumes the user has installed and authenticated Figma's Dev Mode MCP server in their client. This server is **Figma's own product**, not bundled with this plugin. It comes in two flavors (desktop, which requires a Dev or Full Figma seat on a paid plan, and remote). Setup details live in `skills/using-figma/references/setup.md`.

If the Figma MCP tools aren't available in the session, the `using-figma` skill stops and asks the user to install before continuing. Other skills continue to function — they only compose `using-figma` when a Figma URL is in play.

## Installation

```bash
/plugin install bitwarden-designer@bitwarden-marketplace
```

Install `bitwarden-atlassian-tools` alongside it (the Confluence access the skills rely on lives there):

```bash
/plugin install bitwarden-atlassian-tools@bitwarden-marketplace
```

## Usage

The designer agent activates when reviewing or critiquing a design, evaluating GUI copy, reading or inspecting a Figma file without code generation, facilitating a design review, preparing a design handoff, proposing or modifying a Design System component, or navigating the design side of an engineering epic:

```
Critique the 60% draft of the device-trust onboarding screen. Figma URL: ...
```

```
Take a pass on these strings — buttons, the empty state, and the toast on save failure.
```

```
Read this Figma frame and tell me which spacing values aren't bound to the library.
```

```
I'm facilitating critique this week and presenting two screens of my own. How do I set the room up and frame what I want feedback on?
```

```
Help me prep the handoff page for the new vault filter project — Figma file is here, engineering epic is PM-XXXX.
```

```
We keep building variations of this segmented selector — should it become a core component or stay a recipe?
```

```
PM created the epic, designs are at 60%. Walk me through the Jira moves so the design board and engineering board stay in sync.
```

## Related Plugins

- **`bitwarden-atlassian-tools`** — required. Provides Confluence access for the canonical pages this plugin's skills reference.
- **`bitwarden-tech-lead`** — engineering counterpart on the team-scope surface. Use when design questions cross into team-scope architecture.
- **`bitwarden-shepherd`** — engineering counterpart on the cross-team initiative surface.

## References

- [Weekly Design Critique & Etiquette (Quick Guide)](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/2329542659)
- [Product Design Review Guidelines](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/469925913)
- [Creating new design patterns](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/665780251)
- [Modifying an existing Design System component](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/1804206168)
- [Product and Design Jira Process](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/1828094078)
- [Component Library](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/293109785)
- [Figma Dev Mode MCP Server — Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)
- [Figma Dev Mode MCP Server — Tools and Prompts](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
