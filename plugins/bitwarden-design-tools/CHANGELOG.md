# Changelog

All notable changes to the Bitwarden Design Tools Plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-05-22

### Added

- New `applying-bitwarden-branding` skill that applies Bitwarden's canonical brand identity (palette, Inter, official logo lockup, 36px radius foundation) to standalone HTML deliverables — recaps, dashboards, mockups, one-pagers, slides. The skill is explicit about the boundary between **canonical** brand guidance (lifted from `bitwarden.com/brand`) and **pragmatic** deliverable choices the brand site is silent on (surface mode, heading scale, code font, component shapes, voice/tone, accessibility specifics).
- Reference docs: `color-palette.md`, `typography.md`, `logo-usage.md`.
- Assets: `bitwarden-tokens.css` (palette + radius + Inter only — nothing opinionated) and `bitwarden-shield.svg` (small inline shield for chip-scale use).
- Example: `on-brand-one-pager.html` demonstrating both a **light surface** and a **dark surface** composition. The dark surface is labeled pragmatic and derives the background from `--bw-deep-blue` rather than introducing a new neutral. Explicitly not a prescribed component vocabulary.
