# pstack-portable-pane

[![test](https://github.com/meganemura/pstack-portable-pane/actions/workflows/test.yml/badge.svg)](https://github.com/meganemura/pstack-portable-pane/actions/workflows/test.yml)

A Claude Code mod that shows the intermediate artifacts of a [poteto-mode-portable](https://github.com/meganemura/pstack-portable) run in a pane beside the transcript.

A poteto-mode run copies its playbook steps into the task list, starts subagents, and writes files such as a decision trail, a plan, or an Orchestrate store.
This pane collects them in one place.

## What it shows

- **Run.** The entry skill, the selected playbook, and the upstream skills the run read.
- **Steps.** The task list: `[x]` done, `[>]` in progress, `[ ]` pending.
- **Delegates.** Each subagent with its state, description, and agent type.
- **Artifacts.** Each known artifact file, newest first. Press one to preview it below the list: a TSV file as a table, Markdown as Markdown, anything else as code.

The artifacts it knows are the decision trail (`decisions.tsv`, `.audit/*.tsv`), the Orchestrate store files (`preferences.md`, `status.md`, `gates.md`, `units.tsv`, `ledger.tsv`, `frontier.json`, `overview.md`), plans, resume notes, and arena and swarm output.

The pane opens by itself the first time a session starts a poteto-mode run.
`/pstack-portable-pane` hides and shows it, and the mod remembers that choice.
While the pane is hidden, the status line names the run and its artifact count.
Where no pane can be drawn (`claude -p`, VS Code), `/pstack-portable-pane` answers with a text summary.

## Requirements

- Claude Code 2.1.295 or later.
- A terminal session, the Code tab of Claude Code Desktop, or the mobile app.
- A run through `poteto-mode-portable` from [pstack-portable](https://github.com/meganemura/pstack-portable). Upstream pstack runs in Cursor, which does not load Claude Code mods.

## Install

At the prompt of a terminal session:

```
/plugin install pstack-portable-pane --marketplace meganemura/pstack-portable-pane
```

From a shell:

```
claude plugin install pstack-portable-pane --marketplace meganemura/pstack-portable-pane
```

In the desktop app, where `/plugin` does not run: click + next to the prompt box, then Plugins, Add marketplace with `meganemura/pstack-portable-pane`, then Add plugin.

## Develop

See [AGENTS.md](AGENTS.md). The design is in [docs/design.md](docs/design.md).

## License

[MIT](LICENSE)
