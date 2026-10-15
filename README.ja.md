# pstack-portable-pane

[English](README.md)

[poteto-mode-portable](https://github.com/meganemura/pstack-portable) の run が作る中間成果物を、トランスクリプトの横のペインに表示する Claude Code の mod です。

poteto-mode の run は、playbook の手順をタスクリストに写し、subagent を起動し、判断ログ、plan、Orchestrate の store などのファイルを書きます。
このペインは、それらを 1 か所に集めます。

## 表示するもの

- **Run.** 入口のスキル、選ばれた playbook、run が読んだ upstream のスキル。
- **Steps.** タスクリスト。`[x]` は完了、`[>]` は進行中、`[ ]` は未着手です。
- **Delegates.** 各 subagent の状態、説明、エージェントの種類。
- **Artifacts.** 既知の成果物ファイル。新しいものが上です。押すと一覧の下にプレビューが出ます。TSV は表、Markdown は Markdown、それ以外はコードとして表示します。

既知の成果物は、判断ログ（`decisions.tsv`、`.audit/*.tsv`）、Orchestrate の store のファイル（`preferences.md`、`status.md`、`gates.md`、`units.tsv`、`ledger.tsv`、`frontier.json`、`overview.md`）、plan、resume note、arena と swarm の出力です。

セッションで poteto-mode の run が始まると、ペインは最初の 1 回だけ自動で開きます。
`/pstack-portable-pane` で表示を切り替えます。mod はその選択を覚えます。
ペインを隠している間は、ステータスラインに run の名前と成果物の数が出ます。
ペインを描けない場所（`claude -p`、VS Code）では、`/pstack-portable-pane` がテキストの要約を返します。

## 必要なもの

- Claude Code 2.1.295 以降。
- ターミナルのセッション、Claude Code Desktop の Code タブ、またはモバイルアプリ。
- [pstack-portable](https://github.com/meganemura/pstack-portable) の `poteto-mode-portable` を通した run。upstream の pstack は Cursor で動き、Cursor は Claude Code の mod を読み込みません。

## 入れる

ターミナルのセッションのプロンプトで:

```
/plugin install pstack-portable-pane --marketplace meganemura/pstack-portable-pane
```

シェルから:

```
claude plugin install pstack-portable-pane --marketplace meganemura/pstack-portable-pane
```

`/plugin` が動かないデスクトップアプリでは、プロンプト欄の横の + から Plugins を開き、Add marketplace で `meganemura/pstack-portable-pane` を追加してから Add plugin を選びます。

## 開発する

[AGENTS.md](AGENTS.md) を見てください。設計は [docs/design.md](docs/design.md) にあります。

## ライセンス

[MIT](LICENSE)
