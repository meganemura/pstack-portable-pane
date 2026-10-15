# AGENTS.md

Context for agents that work in this repository.

## What this is

pstack-portable-pane, a Claude Code mod. Its hooks module watches the tool uses of a session and draws the intermediate artifacts of a poteto-mode-portable run in a pane beside the transcript.
The design is in `docs/design.md`.

The plugin lives in `plugin/`. There is no build step and no runtime package dependency.

## Visibility

The repository is public. Commit messages, comments, README and docs are in English.
Follow ASD-STE100 Simplified Technical English. Test fixtures use invented paths and runs, never a real project's.
`README.ja.md` is the one Japanese file. Keep it in sync with `README.md`, which ends with a link to it.

## Rules

- `plugin/hooks/run.ts` is a pure reducer and the artifact registry. It has no `$` and no I/O. A new artifact name is a new registry row, not a new branch.
- `plugin/hooks/mod.ts` holds every call on `$`. The render hook draws from `$.state` alone and never reads a file or the transcript.
- The transcript is the source of truth. `session.start` and `turn.complete` rebuild the Run from it. `tool.call` folds each finished call between them.
- Every element prop must be one that terminal, desktop and mobile all declare. The `Kit` type in `mod.ts` makes the compiler refuse others.
- Tests are `plugin/tests/*.test.ts`, run with `claude plugin test plugin`. They stub what the module calls beneath it (`session.messages`, `fs.read`, `ui.*`, `store.*`).
- Quality gates, all three before a commit:
  - `claude plugin validate plugin`
  - `npx --yes --package typescript@7.0.2 tsc -p plugin/hooks`
  - `claude plugin test plugin`
- `tsc` reads the API declarations from `plugin/.claude-plugin/types/`, which git ignores. An interactive session that loads `plugin/` with `--plugin-dir` writes them there. Without one, copy `types/claude-code.d.ts` from the plugin-authoring skill of the same Claude Code build to `plugin/.claude-plugin/types/claude-code/index.d.ts`.
- Development loop: `claude --plugin-dir "$PWD/plugin"` in a real terminal, or `CLAUDE_CODE_PLUGIN_DIRS` with `CLAUDE_CODE_PLUGIN_DIR_WATCH=1` for the desktop app.
- Design decisions go to `docs/decisions/` as short numbered notes (Context / Decision / Consequences).
- Commits are semantic units. Comments say why, not what. Each module starts with its responsibility and what it must not know about.
- Adding a dependency: exact pin, released 7 or more days ago with no security fix after it, and ask the owner first with the reason.
