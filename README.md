# agent-kickoff

> 整備中のため、ルールは予告なく変わります。

コーディングエージェント（Claude Code など）と一緒に開発を始めるための、共通ルールと GitHub テンプレートです。言語やツールに依存しない内容だけを置いています。

毎回の案件で「進め方・ブランチ・版・文書の置き場所」を決め直さなくて済むように、決まりを 1 か所にまとめ、新しいリポは最初から同じ形で始められるようにしています。

## 考え方

- **相談 → 仕様書 → 実装**：「相談」「ラフ」と頼んだ間、エージェントは実装しません。決まったら仕様書を書き、承認した仕様書にもとづいて PR まで進めます。文書だけの変更は仕様書なしで進めます。
- **書き分けの原則**：コードは How、テストは What、コミットは Why、コードコメントは Why not を書きます。
- **ADR で決定を残す**：技術・構成を選んだ理由と、採らなかった案を残します。エージェントが却下済みの案を蒸し返すのを防ぐためです。
- **日付の版**：版は `YYYY.M.N`（N はその月の何回目か）です。
- **人が最後に決める**：PR の Merge とブランチの削除は人が行います。

詳しくは [doc/rules.md](doc/rules.md)、各ルールの理由は [doc/rules-adr/](doc/rules-adr/README.md) にあります。

## 必要なもの

| もの | 用途 |
|---|---|
| GitHub のアカウント | テンプレートからリポを作る |
| [Docker](https://docs.docker.com/get-docker/) と [VS Code](https://code.visualstudio.com/)、[Dev Containers 拡張](https://code.visualstudio.com/docs/devcontainers/containers) | 開発環境をコンテナで揃える |
| コーディングエージェント | 既定は [Claude Code](https://code.claude.com/docs/en/overview)。ほかのエージェントでも `AGENTS.md` を読めれば使える |
| チャットで相談できる AI | キックオフの相談に使う（`KICKOFF.md` を読ませる） |
| （任意）[GitHub CLI](https://cli.github.com/)（`gh`） | シークレットの登録など |

Dev Containers は、リポに置いた設定ファイルから開発用のコンテナを作り、VS Code をその中で動かす仕組みです。エージェントが実行するコマンドも、手元の PC ではなくコンテナの中で動きます。

## 使い方（新しい案件）

### 1. チャットで相談する

チャットの AI に、このリポの [`KICKOFF.md`](KICKOFF.md) を読ませてから、作りたいものを相談します。

```text
https://github.com/zeusisgood/agent-kickoff の KICKOFF.md に従って、新しい案件のキックオフをしたいです。
作りたいもの：（ここに書く）
```

相談が終わると、仕様書・ADR・`AGENTS.md`・devcontainer の設定などのファイルと、エージェントへの最初の指示文を受け取れます。

### 2. テンプレートからリポを作る

GitHub でこのリポを開き、「Use this template」→「Create a new repository」を選びます（[GitHub の説明](https://docs.github.com/ja/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)）。作ったリポを手元に clone します。

### 3. ファイルを置く

1. 1 で受け取ったファイルを、同じパスに置きます（上書きします）。
2. `KICKOFF.md` を削除します。
3. `LICENSE` を案件のライセンスに置き換えます。1 で受け取っていればそれを置き、ライセンスを付けないなら削除します。そのままにすると、案件が CC0-1.0 になります。`.claude/skills/*/LICENSE` は同梱のスキルのものなので、消さずに残します。
4. Claude Code を使わない場合は、`CLAUDE.md`・`.claude/`・`.github/workflows/claude.yml` を削除します。
5. 最初のコミットを `main` に push します（この最初の 1 回だけは直接 push してよいです）。

### 4. （任意）PR のコメントで Claude を呼べるようにする

PR や issue のコメントに `@claude` と書くと、Claude が答えるようにできます。Claude のサブスクリプション（Pro・Max など）の範囲で動き、API の従量課金はかかりません。

1. 最初の 1 回だけ、手元でトークンを作ります：`claude setup-token`
2. リポごとに、シークレットとして登録します：`gh secret set CLAUDE_CODE_OAUTH_TOKEN`（実行するとトークンの入力を求められます）
3. [Claude の GitHub App](https://github.com/apps/claude) をリポにインストールします。

### 5. コンテナを開いてエージェントを起動する

1. VS Code でリポを開き、「Reopen in Container」を選びます。初回はコンテナの作成に数分かかります。
2. ターミナルでエージェントを起動します（Claude Code なら `claude`）。初回はログインが必要です。ログイン状態は、コンテナを作り直しても残ります。
3. 1 で受け取った最初の指示文を貼ります。

あとはエージェントが実装し、PR を作ります。

## 使い方（既存のリポ）

テンプレートは新しいリポにしか使えないので、次のファイルをこのリポからコピーします。既にあるファイルは、内容をまとめてください。

- `AGENTS.md`・`CLAUDE.md`（Claude Code を使う場合）
- `doc/rules.md`・`doc/rules-adr/`・`doc/rules-changelog.md`・`doc/upstream-prompt.md`・`doc/spec/`・`doc/adr/`・`doc/architecture.md`・`doc/TODO.md`
- `.claude/`（Claude Code を使う場合）・`.devcontainer/`・`.github/workflows/`
- `.gitignore`・`.editorconfig`・`.gitattributes`

`LICENSE` はコピーしません（案件のライセンスを使います）。

そのうえで、チャットでの相談（1）から始めます。相談の前に、相手のエージェントが既存のコードから今の規約（命名・構成・テストの書き方など）を抜き出し、ルールと食い違う所をどちらに揃えるか相談します。

## 日々の流れ

| 段階 | 人 | エージェント |
|---|---|---|
| 相談 | 「相談」「ラフ」と付けて頼む。決める | 案を比べ、おすすめと質問を返す。実装しない |
| 仕様書 | 読んで「実装」と承認する | 仕様書と、必要なら ADR を書く。承認後に作業の分解（チェックリスト）を書く |
| 実装 | 待つ | ブランチを切り、テスト・実装・図の更新・レビューをして PR を作る |
| 確認 | PR を見て、成果物を試す | 聞かれたら CI の結果を確かめ、赤なら直す |
| 取り込み | Merge し、ブランチを消す | 消すブランチの候補とコマンドを渡す |
| リリース | 「Merge した」と伝える | タグを付けて push する。GitHub Release は Actions が作る |

エージェントは、承認済みの決定に反する変更が必要なときや、仕様の意図が分からないときには、push せずに止まって相談します。

## 中身

| ファイル | 内容 |
|---|---|
| [doc/rules.md](doc/rules.md) | 開発の共通ルール（本体） |
| [doc/rules-adr/](doc/rules-adr/README.md) | 共通ルールを決めた理由と採らなかった案（ADR） |
| [doc/rules-changelog.md](doc/rules-changelog.md) | 共通ルールの変更履歴（ルール版ごと） |
| [doc/upstream-prompt.md](doc/upstream-prompt.md) | 案件で生まれたルールを原本に入れるときのプロンプトの雛形 |
| [LICENSE](LICENSE) | このリポのライセンス（CC0-1.0）。案件では置き換える |
| [KICKOFF.md](KICKOFF.md) | キックオフで相談相手のエージェントが従う手順 |
| `AGENTS.md` | エージェントの入口。案件ごとに書き換える |
| `CLAUDE.md` | Claude Code の入口（`AGENTS.md` を取り込む） |
| `doc/spec/` | 仕様書・作業の分解の雛形と一覧 |
| `doc/adr/` | 案件の ADR の雛形と一覧 |
| `doc/architecture.md` | 仕組みと図（Mermaid）の雛形 |
| `.devcontainer/` | slim イメージ＋`vscode` ユーザー＋Claude Code（入れないこともできる） |
| `.claude/agents/` | Claude Code のサブエージェント（探索・ログ要約・レビュー） |
| `.claude/settings.json` | Claude Code に禁止する操作（force push・Merge など） |
| `.claude/skills/` | Claude Code のスキル（外部から写した security-audit・ponytail。出どころは中の `README.md`） |
| `.github/workflows/` | `@claude` の呼び出し・タグからの Release 作成 |

## カスタマイズ

- **言語に合わせる**：`.devcontainer/devcontainer.json` の `BASE_IMAGE` を、言語の公式 slim イメージ（例：`golang:1-trixie`・`rust:slim-trixie`・`python:3-slim-trixie`）に変えます。追加の道具は `Dockerfile` の `apt-get install` の行に足します。
- **案件の性質に合わせる**：rules の付録 A（通信・多言語・設定ファイル・CI）のうち、該当するものを `AGENTS.md` に書きます。
- **別のエージェントを使う**：`AGENTS.md` と rules だけで動きます。権限設定などの専用ファイルが要るときは、rules の付録 B に節を足してください。

## 共通ルールと案件の行き来

ルールには版（ルール版、`doc/rules.md` の冒頭）があり、変更点は [doc/rules-changelog.md](doc/rules-changelog.md) に書いています。詳しい手順は rules の 13 章です。

- **原本の更新を案件に取り込む**：案件の中の版が正なので、このリポを更新しても自動では反映されません。代わりに、エージェントがセッションの最初に原本の版を確かめます。新しければ手を止め、変更点の要約を見せて相談します。取り込むと決めたら、案件内の PR で揃えます。「後で」と答えれば、`doc/TODO.md` に控えて元の作業に戻ります。
- **案件で生まれたルールを原本に入れる**：どの案件にも使えそうなルールが出てくると、エージェントが提案し、`doc/TODO.md` に控えます。原本への PR は、はっきり頼んだときだけ出します。作業中の環境から原本に PR を出せない場合は、エージェントが [doc/upstream-prompt.md](doc/upstream-prompt.md) の形でプロンプトを作ります。それを、PR を出せる環境のエージェントに貼ってください。

## ライセンス

[CC0-1.0](LICENSE) です。著作権を放棄しているので、表示を残す必要はなく、自由に複製・改変して使えます。ただし `.claude/skills/` の外部のスキルは元のライセンス（MIT）のままで、各ディレクトリの `LICENSE` を残す必要があります（[ADR 0018](doc/rules-adr/0018-bundle-third-party-skills.md)）。テンプレートから作った案件には、好きなライセンスを付けてください（理由は [ADR 0016](doc/rules-adr/0016-cc0-license.md)）。
