# ルールの変更履歴

原本（[zeusisgood/agent-kickoff](https://github.com/zeusisgood/agent-kickoff)）のルール版ごとの変更点。新しい版を一番上に足す。見出しは `## YYYY.M.N (YYYY-MM-DD)`。

案件に取り込むときに読むので、各項目は 1 行で、何が変わったかと関係する rules-adr の番号を書く。案件ごとに直しているファイル（`AGENTS.md`・`CLAUDE.md`・`.claude/`・`.devcontainer/` など）の変更は、そのファイル名を書く。

## 2026.10.4 (2026-10-21)

- ブランチ名は作業を始める前に提案し、ユーザーの了承を得てから切る。依頼文で指定されていれば提案は要らない（3 章、rules-adr 0017）

## 2026.10.3 (2026-10-21)

- `.devcontainer/Dockerfile`：基盤イメージに UID・GID 1000 の利用者（`node`・`ubuntu` など）がいれば消してから `vscode` を作る。別の UID で作られて、ワークスペースに書き込めなかった
- `AGENTS.md`：原本ではこの文書ではなく `doc/upstream-prompt.md` に従う、の 1 行を冒頭に足す（案件では当てはまらない）
- 原本ではタグも Release も作らない、を `doc/upstream-prompt.md` に明記（rules-adr 0006）

## 2026.10.2 (2026-10-21)

- 原本のライセンスを CC0-1.0 にした。テンプレートの `LICENSE` は案件のライセンスに置き換える（README・`KICKOFF.md`、rules-adr 0016）。既存の案件では、原本の `LICENSE` を取り込まない

## 2026.10.1 (2026-10-21)

- 仕様書を承認したら、作業の分解 `doc/spec/TASKS_…` を書く。雛形 `doc/spec/_tasks_template.md` を追加（2 章、rules-adr 0014）
- 文書だけの変更は仕様書なしでよい。rules は 300 行までを目安にする（0 章・2 章、rules-adr 0015）
- 既存のリポに入れるとき、既存コードから規約を抜き出して相談する（`KICKOFF.md`）
- Copier などのマージの仕組みは今は使わない、を未決事項として明記（13 章、rules-adr 0013 の注記）
- `AGENTS.md`：要点の 1 行を変更（作業の分解・文書だけの変更）

## 2026.10.0 (2026-10-21)

- 初版。相談 → 仕様書 → 実装の進め方、書き分けの原則、ブランチ・コミット・PR・タグ、日付の版、ADR、役割の分担、devcontainer、安全（rules-adr 0001〜0011）
- 共通ルールとの行き来（上り・下り）とルール版（13 章、rules-adr 0012・0013）
