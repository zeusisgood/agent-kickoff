# 0006. タグは Merge を確かめてから Claude が付け、Release は Actions が作る

- 状態：承認
- 日付：2026-10-21
- 関連：rules 3 章・付録 A-4

## 背景

Merge はユーザーが行う。そのため、Claude がタグを付ける時点で、そのコミットが main に入っているとは限らない。PR の作成とタグ付けは Claude に任せたい。

## 決定

- PR は Claude が作る。Merge とブランチ削除はユーザーが行う。
- タグは、Merge を確かめてから Claude が付ける。確かめるのは「Merge した」と言われたとき、または次の作業を始めるときで、main に入った `Release …` コミットに付けて push する。
- 既存のタグの削除と上書きは、権限設定で禁止する。
- GitHub Release は、タグの push を受けて Actions が作る。本文は CHANGELOG の該当節。

## 採らなかった案

| 案 | 採らなかった理由 |
|---|---|
| PR を出すときにタグを付ける | PR を閉じたり作り直したりすると、取り込まれていないタグが残る |
| Claude はタグを付けない（main への取り込みで Actions が付ける） | タグも Claude に任せたい |
| Release も Claude が作る | 成果物の添付まで含めると手順が重くなる。タグを起点に Actions に任せるほうが確実 |

## 結果

- 良くなること：main にあるコミットにだけタグが付く。Release の作り方が毎回同じになる。
- 引き受けること：
  - Merge の後に一手間増える。
  - CHANGELOG の見出しを `## YYYY.M.N (YYYY-MM-DD)` に固定する必要がある。

## 未決事項

なし

（注: 2026-10-21、[0011](0011-agent-neutral-agent-kickoff.md) でリポ名を `agent-kickoff` に変え、エージェントに依存しない形にした。本文中の `claude-kickoff` は当時の名前。）

（注: 2026-10-21、原本ではタグも Release も作らない。原本の `CHANGELOG.md` は案件向けの空の雛形で、`release.yml` が必ず失敗するため。原本の版は `doc/rules.md` のルール版と `doc/rules-changelog.md` で表す。`doc/upstream-prompt.md` に明記した。）
