# Bitwarden Design Tools Plugin

## Overview

Design toolkit for Bitwarden — the non-persona half of the design plugin pair. Six skills covering content style, Figma Dev Mode MCP usage, Bitwarden brand application, design-to-engineering handoff prep, Design System governance, and the Product and Design Jira workflow. Composed by the `bitwarden-designer` agent and usable standalone (designers, design-adjacent engineers, PMs running a handoff).

This plugin ships skills only — no agent. The persona half lives in [`bitwarden-designer`](../bitwarden-designer/), which dispatches into these skills by name.

## Skills

| Skill                               | What It Does                                                                                                                                                                                                                                                                                                                                             |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `content-style-guide`               | Bitwarden's product content style guide for GUI copy — voice, tone, AP-style-with-exceptions grammar, sentence case in UI, no ampersands, and accessibility-first language at a U.S. 7th-grade reading level. Lean SKILL.md with detailed rules split across `references/grammar-mechanics.md` and `references/accessibility-rules.md`.                  |
| `using-figma`                       | Read and inspect Figma designs via the Dev Mode MCP server. Per-job-to-be-done tool selection for read tools (`get_design_context`, `get_metadata`, `get_screenshot`, `get_variable_defs`, `search_design_system`, `get_libraries`), with Code Connect and write tools documented in their own subsections. Foundational — most other skills compose it. |
| `applying-bitwarden-branding`       | Apply Bitwarden brand standards — logo usage, color palette, typography, iconography, and capitalization rules. Grounded in [bitwarden.com/brand](https://bitwarden.com/brand/) and the [bitwarden/brand](https://github.com/bitwarden/brand) repository. Full palette and asset inventory in `references/`.                                             |
| `preparing-design-handoff`          | Prepare a Bitwarden design handoff — the Confluence handoff page (Background, Stakeholders, Userflows, Message Text File, Figma Prototype, Annotated Prototype), the Figma file in Ready-for-Dev state, and the Jira state transitions that go with them. Full template reference in `references/handoff-template.md`.                                   |
| `evolving-design-system-components` | Propose a new UI pattern or modify an existing Component Library component per Bitwarden's published governance process — design-team alignment, Core vs. Recipe/Snowflake with UI Foundation, Figma branching and property conventions, review gates, merge timing. Figma conventions in `references/figma-conventions.md`.                             |
| `navigating-design-jira-process`    | Move design work through Bitwarden's Product and Design Jira workflow — design tasks nested under engineering epics, the 30/60/90 iteration cadence, status transitions across the design and engineering boards, and the one-off engineering story flow.                                                                                                |

## Cross-Plugin Integration

| Plugin                      | How It's Used                                                                                                                                                                                                                                                                                              |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `bitwarden-designer`        | Primary consumer. The designer persona dispatches into every skill here by name. Either plugin works standalone, but the pair is the intended shape.                                                                                                                                                       |
| `bitwarden-atlassian-tools` | Required. The Confluence-grounded skills here (`preparing-design-handoff`, `evolving-design-system-components`, `navigating-design-jira-process`, `facilitating-design-critique` reference, etc.) assume `get_confluence_page` is available to fetch the canonical pages directly when prepping real work. |

All cross-plugin skills are required.

## External Dependency: Figma Dev Mode MCP Server

The `using-figma` skill assumes the user has installed and authenticated Figma's Dev Mode MCP server in their client. This server is **Figma's own product**, not bundled. It comes in two flavors (desktop, which requires a Dev or Full Figma seat on a paid plan, and remote). Setup details live in `skills/using-figma/references/setup.md`.

If the Figma MCP tools aren't available in the session, the `using-figma` skill stops and asks the user to install before continuing. Other skills continue to function — they only compose `using-figma` when a Figma URL is in play.

## Installation

```bash
/plugin install bitwarden-design-tools@bitwarden-marketplace
```

Most users will also want the persona half and the Atlassian access:

```bash
/plugin install bitwarden-designer@bitwarden-marketplace
/plugin install bitwarden-atlassian-tools@bitwarden-marketplace
```

## Usage

The skills here activate based on the task at hand — they can be invoked through the `bitwarden-designer` agent or standalone:

```
Review this copy: "Click here to learn more about export."
```

```
Read this Figma frame and list the variables it uses: <figma URL>
```

```
Is this banner on-brand? #175DDC headline, green CTA, Inter font.
```

```
Walk me through prepping the handoff page for the new vault filter project.
```

```
We keep building variations of this segmented selector — should it become a core component?
```

```
PM created the epic, designs are at 60%. Walk me through the Jira moves so the design board and engineering board stay in sync.
```

## Related Plugins

- **`bitwarden-designer`** — persona half. Dispatches into the skills here.
- **`bitwarden-atlassian-tools`** — required. Confluence access for the canonical pages this plugin's skills reference.

## References

- [bitwarden.com/brand](https://bitwarden.com/brand/) — brand guidelines hub.
- [bitwarden/brand](https://github.com/bitwarden/brand) — brand assets repository.
- [Weekly Design Critique & Etiquette (Quick Guide)](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/2329542659)
- [Product Design Review Guidelines](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/469925913)
- [Creating new design patterns](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/665780251)
- [Modifying an existing Design System component](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/1804206168)
- [Product and Design Jira Process](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/1828094078)
- [Component Library](https://bitwarden.atlassian.net/wiki/spaces/PROD/pages/293109785)
- [Figma Dev Mode MCP Server — Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)
- [Figma Dev Mode MCP Server — Tools and Prompts](https://developers.figma.com/docs/figma-mcp-server/tools-and-prompts/)
