# Changelog

Notable changes to **this template**. Format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versions track the template's
own `package.json`.

This file documents the template itself — `npm run init` removes it so each module
generated from the template starts its own history.

## [0.1.0] — 2026-08-22

First release. Forked from `runegoblin-foundrytemplate` (the PF2e template) at `c7ab8d5`,
carrying over the whole stack — v14-only TypeScript + Svelte 5 + Vite, the Svelte-in-
ApplicationV2 shell, the compendium-pack and Adventure build, `npm run init` / `setup` /
`deploy`, the two-tier vitest + Playwright harness, and the tag-driven release workflow.

### Changed

- **Types are `fvtt-types`** (`@league-of-foundry-developers/foundry-vtt-types`, pinned to
  an exact v14 beta and aliased to `fvtt-types`) in place of the `foundry-pf2e` typedefs.
  It models Foundry's lifecycle, so `game` is a union that narrows through `game.ready`
  rather than being unconditionally populated, and `game.settings` keys are checked against
  a declared `SettingConfig`.
- **No system coupling.** `module.json` drops the `relationships.systems` entry; the e2e
  harness no longer asserts a `pf2e` world, taking an optional `TEST_SYSTEM` env var instead
  and defaulting `TEST_WORLD` to `foundry-test`.
- `npm run setup` resolves a **game system source** — pick one of the systems installed in
  your Foundry data dir, or point at a checkout — instead of cloning `foundryvtt/pf2e`. The
  reference symlink is `_system-source` (was `_pf2e-source`).
- The bundled Claude Code skill is `foundry-module` (was `foundry-pf2e`), rewritten
  system-agnostic and documenting the fvtt-types lifecycle and settings patterns.
- `LICENSE` and the README's license section generalize the Paizo/PF2e notices to any game
  system's content.

### Added

- `src/fvtt-config.d.ts` — the `fvtt-types/configuration` augmentation point. It declares
  `core.adventureImports` (which fvtt-types doesn't list) and is where a module declares
  its own settings keys and document types.
