# Design Handoff Page Template — Field Reference

The Bitwarden Product and Design space follows a consistent handoff template across every
recent project. Use this reference when drafting a new handoff page. The Bulk Management
handoff page (ID `387350548`) is a clean working example to read alongside this reference via
`get_confluence_page`.

Field order below matches the template. Italic notes are the in-template prompts that appear
in the actual Confluence template — preserve them when starting a new page so future
maintainers can see the field intent.

## Product Initiative Confluence Page

A link to the PRD-equivalent document — the initiative-level page that defines the _why_. If
the initiative spans multiple handoffs, link to the section relevant to this handoff.

## Design Confluence Page

The current page itself. Self-reference. (`[current page]` in the template.)

## Link to Development Epics

Engineering epic(s) in Jira. If the design supports multiple epics, link all of them.

## Designer

Mention the assigned designer using Confluence's @-mention so the page surfaces in their
notifications and the design board correctly identifies ownership.

## Design Status

A status macro reading `DESIGN DONE` once handoff is real. Before that, `IN DESIGN` or `IN
PROGRESS` per the design Kanban board. The status macro is the engineering team's primary
signal that this design is ready to pick up.

## Product Initiative

> _If applicable include the link to the product initiative document_

Repeat the initiative link at the section level. Yes, duplicated with the header — the
template intentionally exposes it twice because some readers scroll, some search.

## Background

> _Brief overview of project purpose, goals and solution_

Write for someone reading cold. They didn't attend critique. They might not know the product
area well. The strongest backgrounds are 3-5 short paragraphs:

1. The problem in the user's terms.
2. Why current behavior doesn't solve it.
3. The shape of the solution at the design level.

Avoid lifting verbatim from the PRD — it usually has too much business context and not enough
design framing.

## Stakeholders & Team

> _List any relevant stakeholders to be included in the handoff process_

- **Primary Stakeholders:** PM, designer, EM. The people accountable for the outcome.
- **Secondary Stakeholders:** Research, marketing, partner engineering teams, anyone whose
  surface the design touches.

If engineering isn't in the primary list, the handoff hasn't been socialized — fix that
before publishing.

## Jira/Asana Tickets

> _Link to the Epic or Story level tickets related to the project_

Epic links at minimum. Story links if they exist. If stories haven't been created yet,
that's fine — engineering creates them during technical breakdown — but link the epic.

## Design Documents

> _Should include any design related documents including research and a file containing the
> source of truth for the project background and rationale behind design decisions_

Research findings, prior design pages, the source-of-truth design rationale. This is where a
reader goes when they want to understand _why_ a specific choice was made. Don't make them
hunt.

## Userflows

> _Includes the happy path and potential edge cases_

A flow diagram (FigJam or Figma) showing the happy path and at minimum the edge cases that
required design decisions. Edge cases that engineering will discover late if missed: empty
states, error states, partial-success states, offline / no-network states, premium-gating
states, multi-account states.

## Message Text File

> _Messages in the form of toasts, notifications, form verifications, email body copy, etc._

A table. Every user-visible string in the design, numbered to match the Figma frames. This
is the most-skipped field and the one engineering will ask for first when it's missing. The
template's columns:

| Number (matches figma/userflow) | Title   | Format             | Text |
| ------------------------------- | ------- | ------------------ | ---- |
| 1.0                             | Success | Toast Notification | ...  |
|                                 | Warning | Toast Notification | ...  |
|                                 | Error   | Toast Notification | ...  |

Walk every row through the `content-style-guide` skill before publishing. The Message Text
File is the highest-leverage place to fix content-style issues — once these strings hit i18n
files, changes get expensive.

## Figma Prototype

> _Link to a high-fidelity prototype that solves the problems outlined in the product
> initiative and/or design documents._

Link directly to the prototype frame, not the file root. Engineering should land on the
starting screen, not the page selector.

## Annotated Prototype

> _Visit this link to learn more around the annotation process_

A separate annotated version of the prototype with design rationale, interaction notes, and
state callouts inline on the frames. Bitwarden has a published annotation process; link to it
when teaching a new designer this field rather than rebuilding the convention from scratch.

## Field-by-field readiness check

Before changing the Design Status macro to `DESIGN DONE`:

- [ ] Every section has content (not blank, not "TBD").
- [ ] Background reads cleanly to someone outside the project.
- [ ] Userflows include the edge cases — empty, error, partial-success, offline.
- [ ] Message Text File table is populated and walked through `content-style-guide`.
- [ ] Figma Prototype link lands on the start screen.
- [ ] Annotated Prototype exists.
- [ ] Engineering is in Primary Stakeholders.
- [ ] Jira epic exists and is linked.
- [ ] The Figma file has Ready-for-Dev sections matching the expected engineering stories.

If any item fails, the handoff is not ready — back to In Design.
