# AGENTS.md

<!-- キックオフ時に、案件固有の内容で書き換える。エージェント固有の指示は CLAUDE.md などの入口ファイルに書く。 -->

このリポが原本（zeusisgood/agent-kickoff）なら、この文書の「要点」ではなく、[doc/upstream-prompt.md](doc/upstream-prompt.md) の「原本を直すときの注意」に従う。

## 最初に読むもの

| 目的 | 文書 |
|---|---|
| 作業のルール（必ず守る） | [doc/rules.md](doc/rules.md) |
| 仕組みと図 | [doc/architecture.md](doc/architecture.md) |
| 仕様書の一覧 | [doc/spec/README.md](doc/spec/README.md) |
| この案件の決定（ADR） | [doc/adr/README.md](doc/adr/README.md) |
| 共通ルールの理由（ADR） | [doc/rules-adr/README.md](doc/rules-adr/README.md) |
| 共通ルールの変更履歴 | [doc/rules-changelog.md](doc/rules-changelog.md) |
| 後回しの作業 | [doc/TODO.md](doc/TODO.md) |

## 要点

- 「相談・ラフ・整理・計画」では実装しない。
- 承認済みの仕様書があれば、作業の分解（`TASKS_…`）を書いてから、実装から PR まで進める。Merge はユーザー。文書だけの変更は仕様書なしでよい。
- PR の前に、書いた文脈から切り離したレビューを通す。
- 承認済みの ADR に反する変更が必要なら止まる。
- セッションの最初の作業では、原本のルール版を確かめる。新しければ止めて相談する（rules 13 章）。
- `doc/rules.md` と `doc/rules-adr/` は直接直さない。共通にしたいルールは `doc/TODO.md` の「原本へ提案」に控えて相談する。
- コードは How、テストは What、コミットは Why、コメントは Why not。

## この案件について

- 概要：（1〜2 行）
- 言語・ツール：
- ライセンス：
- 該当する付録 A：（通信 / 多言語 / 設定ファイル / CI）

## 版を書く所

版を上げるときは、ここに挙げた所をすべて揃える。

| ファイル | 場所 |
|---|---|
| `CHANGELOG.md` | 一番上の節 |
| （例：ビルド設定） | |

## コマンド

| 目的 | コマンド |
|---|---|
| ビルド | |
| テスト | |
