# 0001. A repository of its own

- Status: accepted
- Date: 2026-10-15

## Context

The pane was first a third plugin in the pstack-portable marketplace (meganemura/pstack-portable#6).
That marketplace serves Claude Code and Codex, and Codex also lists every plugin in it.
The pane runs in Claude Code only, and only a run through the `poteto-mode-portable` wrapper reaches it.
Upstream pstack runs in Cursor, which does not load Claude Code mods.

## Decision

The pane is its own repository, `meganemura/pstack-portable-pane`, with its own marketplace.
The layout follows the other pane mods of the same owner: the plugin in `plugin/`, the hooks module in `plugin/hooks/mod.ts`, decisions in `docs/decisions/`, and CI that runs the gates.
The plugin, its command and its pane are all named `pstack-portable-pane`.

## Consequences

- pstack-portable does not change, and its release rules (every commit on `main` is a release for Codex) do not apply to the pane.
- The pane reads no pstack-portable file. It depends only on the names that the wrapper and upstream use for skill files and artifacts. A change to those names needs a change to the registry in `plugin/hooks/run.ts`.
