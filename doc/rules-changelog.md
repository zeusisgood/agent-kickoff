# ルールの変更履歴

原本（[zeusisgood/agent-kickoff](https://github.com/zeusisgood/agent-kickoff)）のルール版ごとの変更点。新しい版を一番上に足す。見出しは `## YYYY.M.N (YYYY-MM-DD)`。

案件に取り込むときに読むので、各項目は 1 行で、何が変わったかと関係する rules-adr の番号を書く。案件ごとに直しているファイル（`AGENTS.md`・`CLAUDE.md`・`.claude/`・`.devcontainer/` など）の変更は、そのファイル名を書く。

## 2026.10.1 (2026-10-21)

- 仕様書を承認したら、作業の分解 `doc/spec/TASKS_…` を書く。雛形 `doc/spec/_tasks_template.md` を追加（2 章、rules-adr 0014）
- 文書だけの変更は仕様書なしでよい。rules は 300 行までを目安にする（0 章・2 章、rules-adr 0015）
- 既存のリポに入れるとき、既存コードから規約を抜き出して相談する（`KICKOFF.md`）
- Copier などのマージの仕組みは今は使わない、を未決事項として明記（13 章、rules-adr 0013 の注記）
- `AGENTS.md`：要点の 1 行を変更（作業の分解・文書だけの変更）

## 2026.10.0 (2026-10-21)

- 初版。相談 → 仕様書 → 実装の進め方、書き分けの原則、ブランチ・コミット・PR・タグ、日付の版、ADR、役割の分担、devcontainer、安全（rules-adr 0001〜0011）
- 共通ルールとの行き来（上り・下り）とルール版（13 章、rules-adr 0012・0013）
