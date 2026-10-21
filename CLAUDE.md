@AGENTS.md

## Claude Code の場合

- 役割の分担（rules 8 章）は `.claude/agents/` のサブエージェントを使う。
  - 探索は `Explore`、ログが長くなりそうなコマンドは `log-summarizer`。
  - PR の前に `reviewer` を必ず通す。`/ponytail-review` は任意の追加で、`reviewer` の代わりにしない。
- `Explore` は `CLAUDE.md` も `AGENTS.md` も読まない。守らせたい規則は依頼文に書く。
- ブランチ名は `claude/<内容が分かる英語>`。
- `.claude/skills/` の `ponytail` は、ユーザーが `/ponytail` と打ったときだけ使う。rules と食い違うときは rules に従う。
