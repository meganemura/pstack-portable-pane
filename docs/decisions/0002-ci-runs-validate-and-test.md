# 0002. CI runs validate and the tests on Claude Code 2.1.295

- Status: accepted
- Date: 2026-10-15

## Context

The other pane mods run three gates in CI: `claude plugin validate`, `tsc`, and `claude plugin test`.
Their `tsc` reads the declarations that `/plugin-types` writes. That command is gone in the Claude Code builds this mod needs.
No command of Claude Code 2.1.295 writes the declarations. The plugin-authoring skill and an interactive session that loads the plugin folder write them.
The dependency rule asks for a version released 7 or more days ago.

## Decision

`.github/workflows/test.yml` installs `@anthropic-ai/claude-code@2.1.295` (released 2026-10-08) and runs two gates: `claude plugin validate plugin` and `claude plugin test plugin`.
`tsc -p plugin/hooks` stays a local gate. AGENTS.md says how to get the declarations.

## Consequences

- A type error that does not change behavior can reach `main` when the local gate is skipped. The tests still run the module.
- On 2026-10-15 both gates passed locally on 2.1.295 and on 2.1.301: 31 tests.
- Revisit when Claude Code ships a command that writes the declarations.
